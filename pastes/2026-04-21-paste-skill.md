---
title: "paste skill"
date: 2026-04-21 16:36:37 +0000
author: pinky
---

## SKILL.md

```yaml
---
name: paste
description: >
  Commit markdown content to the narfman0/scratchpad GitHub Pages pastebin and return a shareable URL.
  Use when: (1) user types /paste [title], (2) user says "paste this", "share this as a paste", or "send to scratchpad",
  (3) a bot response exceeds ~1500 characters and a persistent link would be useful — proactively offer to paste in that case.
  Runs silently via GitHub API; no local git clone needed.
---

# paste

Commit a markdown file to `narfman0/scratchpad` and return its GitHub Pages URL.

## Quick usage

```bash
# Pipe content
echo "# Hello" | bash scripts/paste.sh --title "My Note"

# Inline content
bash scripts/paste.sh --title "Design Doc" --content "$(cat design.md)"

# With custom author
bash scripts/paste.sh --title "Bot Response" --content "..." --author "pinky"
```

## Process

1. **Slug**: `YYYY-MM-DD-kebab-title` (e.g. `2026-04-21-design-doc`)
2. **File**: Jekyll front-matter + content → `pastes/<slug>.md`
3. **Commit**: `gh api repos/narfman0/scratchpad/contents/pastes/<slug>.md --method PUT` with base64-encoded body
4. **Return**: `https://narfman0.github.io/scratchpad/pastes/<slug>/`

## Script

`scripts/paste.sh` — accepts `--title`, `--content`, `--author`; content may be piped via stdin. Outputs the URL on success, error message to stderr on failure.

## Notes

- GitHub Pages rebuilds in ~30s after each push; share the URL immediately, it will be live shortly.
- If a paste with the same slug already exists, append a short timestamp suffix (e.g. `-1430`) to the slug.
- Default author: `pinky`. Default title: `Paste YYYY-MM-DD HH:MM`.
- The site index at `https://narfman0.github.io/scratchpad/` lists all pastes automatically.
```

## scripts/paste.sh

```bash
#!/usr/bin/env bash
# Commits a markdown paste to narfman0/scratchpad and returns the GitHub Pages URL.
# Usage: paste.sh [--title "My Title"] [--content "..."] [--author "name"]
# Content may also be piped via stdin.

set -euo pipefail

TITLE=""
CONTENT=""
AUTHOR="pinky"

while [[ $# -gt 0 ]]; do
  case "$1" in
    --title)   TITLE="$2";   shift 2 ;;
    --content) CONTENT="$2"; shift 2 ;;
    --author)  AUTHOR="$2";  shift 2 ;;
    *) echo "Unknown argument: $1" >&2; exit 1 ;;
  esac
done

# Read from stdin if content not supplied
if [[ -z "$CONTENT" ]] && ! [ -t 0 ]; then
  CONTENT="$(cat)"
fi

if [[ -z "$CONTENT" ]]; then
  echo "Error: no content provided (use --content or pipe via stdin)" >&2
  exit 1
fi

# Default title to timestamp
if [[ -z "$TITLE" ]]; then
  TITLE="Paste $(date -u '+%Y-%m-%d %H:%M')"
fi

# Generate slug: date + kebab-cased title
DATE_PREFIX="$(date -u '+%Y-%m-%d')"
SLUG_TITLE="$(echo "$TITLE" | tr '[:upper:]' '[:lower:]' | sed 's/[^a-z0-9]/-/g' | sed 's/--*/-/g' | sed 's/^-//;s/-$//')"
SLUG="${DATE_PREFIX}-${SLUG_TITLE}"
TIMESTAMP="$(date -u '+%Y-%m-%d %H:%M:%S')"

# Build Jekyll front-matter markdown
FILE_CONTENT="---
title: \"${TITLE}\"
date: ${TIMESTAMP} +0000
author: ${AUTHOR}
---

${CONTENT}"

# Base64-encode (no line wrapping)
ENCODED="$(printf '%s' "$FILE_CONTENT" | base64 -w 0)"

# Commit via GitHub API
RESPONSE="$(printf '{"message":"add paste: %s","content":"%s"}' "$TITLE" "$ENCODED" | \
  gh api "repos/narfman0/scratchpad/contents/pastes/${SLUG}.md" \
    --method PUT \
    --input - 2>&1)"

if echo "$RESPONSE" | grep -q '"html_url"'; then
  echo "https://narfman0.github.io/scratchpad/pastes/${SLUG}/"
else
  echo "Error committing paste:" >&2
  echo "$RESPONSE" >&2
  exit 1
fi
```