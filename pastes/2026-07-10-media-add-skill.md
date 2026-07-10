---
title: "media-add skill"
date: 2026-07-10 12:20:58 +0000
author: pinky
---

---
name: media-add
description: "Add movies or TV shows to the media stack via natural language. Use when the user says things like 'add Severance', 'download Dune', 'grab the new Mission Impossible', 'add season 3 of The Bear', or asks to queue/add any specific movie or show. Movies go to Radarr; TV shows go to Sonarr."
---

# media-add Skill

Add **movies** via Radarr and **TV shows** via Sonarr using their APIs.

## Config

```bash
CONFIG=$(cat ~/.openclaw/workspace/skills/media-add/config.json)
RADARR_URL=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['radarr']['url'])")
RADARR_KEY=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['radarr']['apiKey'])")
RADARR_QP=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['radarr']['defaultQualityProfileId'])")
RADARR_ROOT=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['radarr']['rootFolderPath'])")
SONARR_URL=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['sonarr']['url'])")
SONARR_KEY=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['sonarr']['apiKey'])")
SONARR_QP=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['sonarr']['defaultQualityProfileId'])")
SONARR_ROOT=$(echo "$CONFIG" | python3 -c "import sys,json; c=json.load(sys.stdin); print(c['sonarr']['rootFolderPath'])")
```

---

## Movies → Radarr

### Step 1 — Search

```bash
curl -s "$RADARR_URL/api/v3/movie/lookup?term=<TITLE>" \
  -H "X-Api-Key: $RADARR_KEY" | python3 -c "
import sys, json
results = json.load(sys.stdin)
for i, m in enumerate(results[:5]):
    print(f\"{i}: {m['title']} ({m.get('year','?')}) — tmdbId={m['tmdbId']} status={m.get('status','?')}\")
"
```

Pick best match. If ambiguous, show top 3–5 to the user and ask.

### Step 2 — Add (use defaults from config)

```bash
MOVIE_JSON=$(curl -s "$RADARR_URL/api/v3/movie/lookup?term=<TITLE>" \
  -H "X-Api-Key: $RADARR_KEY" | python3 -c "
import sys, json
m = json.load(sys.stdin)[0]
m['qualityProfileId'] = $RADARR_QP
m['rootFolderPath'] = '$RADARR_ROOT'
m['monitored'] = True
m['addOptions'] = {'searchForMovie': True}
print(json.dumps(m))
")

curl -s -X POST "$RADARR_URL/api/v3/movie" \
  -H "X-Api-Key: $RADARR_KEY" \
  -H "Content-Type: application/json" \
  -d "$MOVIE_JSON"
```

Check response for `id` field → success. Report: "Added **{title} ({year})** to Radarr — searching now."

If error contains "already exists" → tell user it's already in the library.

---

## TV Shows → Sonarr

### Step 1 — Search

```bash
curl -s "$SONARR_URL/api/v3/series/lookup?term=<TITLE>" \
  -H "X-Api-Key: $SONARR_KEY" | python3 -c "
import sys, json
results = json.load(sys.stdin)
for i, r in enumerate(results[:5]):
    print(f\"{i}: {r['title']} ({r.get('year','?')}) — tvdbId={r.get('tvdbId')} status={r.get('status','?')}\")
"
```

### Step 2 — Add

```bash
SERIES_JSON=$(curl -s "$SONARR_URL/api/v3/series/lookup?term=<TITLE>" \
  -H "X-Api-Key: $SONARR_KEY" | python3 -c "
import sys, json
s = json.load(sys.stdin)[0]
s['qualityProfileId'] = $SONARR_QP
s['rootFolderPath'] = '$SONARR_ROOT'
s['monitored'] = True
s['addOptions'] = {'searchForMissingEpisodes': True, 'monitor': 'all'}
print(json.dumps(s))
")

curl -s -X POST "$SONARR_URL/api/v3/series" \
  -H "X-Api-Key: $SONARR_KEY" \
  -H "Content-Type: application/json" \
  -d "$SERIES_JSON"
```

Check response for `id` field → success. Report: "Added **{show name}** to Sonarr — searching for episodes now."

If error contains "already exists" → already in library.

---

## Disambiguation

- **Movie**: any standalone film → Radarr
- **TV show / series / season**: anything episodic → Sonarr
- If unclear (e.g. "add Severance" could be either), check both search APIs and let context decide — Severance is a TV show.

## Error Handling

- **Connection refused / DNS failure**: `srv` unreachable — tell user.
- **401**: API key wrong — tell user to verify.
- **No results**: Try alternate terms (drop "The", add year, etc.).