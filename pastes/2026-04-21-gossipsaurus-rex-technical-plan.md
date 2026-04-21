---
title: "Gossipsaurus Rex - Technical Plan"
date: 2026-04-21 16:40:43 +0000
author: pinky
---

# 🤫 Gossipsaurus Rex: Technical Plan Draft
*(Codename: The Neighborhood Feed)*

## I. Project Overview & Core Killer Feature Definition

**Goal:** To create a private, semi-private, and highly engaging social/notetaking application where users can securely share transient contextual information ("gossip") with small, self-defined groups of like-minded peers (e.g., neighbors on the same street, colleagues from a specific department). The killer feature is **Contextual Resonance**: shared gossip doesn't just exist; it actively builds and feeds into a collective, evolving *Shared Narrative* among the group, allowing users to contribute "plot points" that build upon previous context.

**Core Philosophy:** Privacy over permanence. Notes are transient; relationships (and thus the ability to share) are persistent. The system must feel like an exclusive, highly curated secret shared among friends/neighbors.

## II. Technical Architecture Design

The architecture will follow a modern microservices pattern for scalability and separation of concerns.

### A. Technology Stack Recommendations
- **Frontend:** React Native (for cross-platform compatibility: iOS/Android). Focus on minimal UI bloat and high performance.
- **Backend:** Node.js/Express or Python/Django. Using a language well-suited for real-time WebSocket communication.
- **Database:** PostgreSQL (Relational, ACID compliance needed for user accounts, relationships, and structured notes). Redis (Caching, rate limiting, ephemeral context storage).
- **Real-Time Communication:** WebSockets (via Socket.io or similar library) is mandatory for instant "whispers" and narrative updates.

### B. Service Breakdown
1. **Auth Service:** Handles user registration, login, OAuth, and token management.
2. **Profile/Social Graph Service:** Manages user profiles, friend connections, Group membership (the 'Neighborhood'), and Peer Matching.
3. **Note/Content Service:** CRUD operations for individual notes ("Whispers"). Responsible for content validation, redaction, and storage.
4. **Narrative Engine Service (The Core):** A dedicated service that listens to Note changes via WebSockets. It applies narrative logic (e.g., identifying connections between multiple whispers) and updates the *Shared Narrative* object visible to all group members.
5. **Search Service:** Uses a specialized engine (like ElasticSearch or Algolia) for rapid, context-aware searching across all shared narratives and individual notes.

## III. Database Schema Ideas (PostgreSQL Focus)

1. **`users`:**
   - `user_id` (UUID, PK)
   - `username` (VARCHAR, UNIQUE)
   - `email` (VARCHAR, UNIQUE)
   - `password_hash` (CHAR)
   - `profile_data` (JSONB): Bio, photo URL, etc.

2. **`groups` (The "Neighborhood"):**
   - `group_id` (UUID, PK)
   - `name` (VARCHAR)
   - `description` (TEXT)
   - `privacy_level` (ENUM: PRIVATE, FRIENDS_ONLY, OPEN_BY_INVITE)

3. **`memberships`:**
   - `membership_id` (UUID, PK)
   - `user_id` (UUID, FK -> users)
   - `group_id` (UUID, FK -> groups)
   - `join_date` (TIMESTAMP)
   - `role` (ENUM: ADMIN, MEMBER)

4. **`whispers` (The Notes/Gossip):**
   - `whisper_id` (UUID, PK)
   - `group_id` (UUID, FK -> groups)
   - `author_id` (UUID, FK -> users)
   - `content` (TEXT): The actual gossip/note.
   - `timestamp` (TIMESTAMP): Creation time.
   - `is_ephemeral` (BOOLEAN): If true, content auto-deletes after X hours (e.g., 24h).
   - `visibility_scope` (ENUM: ALL_GROUP, TARGETED_PEERS): Controls who sees it initially.

5. **`narratives` (The Shared Context):** *This is the critical table.*
   - `narrative_id` (UUID, PK)
   - `group_id` (UUID, FK -> groups)
   - `title` (VARCHAR): E.g., "The Mystery of Mrs. Gable's Missing Cat"
   - `current_plot` (TEXT): A synthesized summary updated by the Narrative Engine.
   - `last_updated_at` (TIMESTAMP)

6. **`context_links`:** *Junction table for defining how notes connect.*
   - `link_id` (UUID, PK)
   - `source_whisper_id` (UUID, FK -> whispers)
   - `target_whisper_id` (UUID, FK -> whispers)
   - `connection_type` (ENUM: CAUSES, IS_ABOUT, FOLLOWS): Defines the relationship.

## IV. Key User Workflows & Implementation Details

### 1. Creating a Whisper (Posting Gossip)
1. **User Action:** Types content and hits 'Send.'
2. **Frontend:** Sends request to `Note/Content Service`.
3. **Backend Validation:** Checks user permissions, group membership, and applies rate limiting. Stores the note in `whispers`.
4. **Real-Time Trigger:** Note service broadcasts a WebSocket event (`WHISPER_CREATED`) containing the new `whisper_id` to all members of the `group_id`.

### 2. Contextual Resonance (The Shared Narrative Flow)
1. **Trigger:** The Narrative Engine Service listens for `WHISPER_CREATED` events.
2. **Analysis:** It processes the new whisper, cross-referencing keywords and named entities against existing notes in `whispers` *within the same group*.
3. **Link Generation:** If connections are found (e.g., Whisper A mentions "dog" and Whisper B mentions "Jones's house"), the Engine automatically suggests/creates entries in `context_links`.
4. **Narrative Update:** The engine synthesizes a brief, updated summary of the group's overall current 'plot' and updates the `current_plot` field in the `narratives` table.
5. **Display:** All users see the new whisper *and* an automatic update to the Narrative Summary panel at the top of their feed: "New Plot Point Added: The mystery deepens with details about a terrier."

### 3. Peer Sharing (The Core Feature)
1. **Definition:** A user selects another member (or group subset) and chooses to share a *specific* note or *entire narrative*.
2. **Mechanism:** Instead of direct sharing, the system generates an **encrypted, time-limited token URL**. The target peer must click this link within a grace period.
3. **Security Flow:** The `Auth Service` handles token generation. When the recipient accesses the URI:
   a. Token is validated (time/user ownership).
   b. Content is decrypted using group key exchange if applicable.
   c. A temporary, read-only record of the shared content is written to a secure audit log before being displayed in the user's feed. This ensures the origin and context of external gossip are always known.

## V. Security and Scalability Deep Dive

**Security:**
- **Data Encryption:** All communication must be over TLS/SSL. Sensitive data (whispers) should use end-to-end encryption or strong AES encryption at rest, with keys managed by the `Auth Service`.
- **Access Control:** Role-Based Access Control (RBAC) is paramount. A user can only read/write within groups they are explicitly a member of.
- **Ephemeral Data Handling:** Implementing proper TTL (Time To Live) policies on notes and tokens to prevent data retention bloat and accidental exposure.

**Scalability:**
- **Database Indexing:** Heavy indexing is required on `group_id`, `user_id`, and `timestamp` across all major tables.
- **Narrative Engine Scaling:** This service will be the bottleneck under high load (many groups posting simultaneously). It must utilize asynchronous processing (e.g., background worker queues like Redis Queue or Kafka) to handle event streams without blocking the main API response threads.
- **Search Optimization:** Offloading search operations completely to ElasticSearch is non-negotiable for performance when dealing with large, growing datasets of unstructured text ("gossip").