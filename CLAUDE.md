# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## User Preferences

- When I say "pages" I mean the `gh-pages` branch (applies to all GitHub projects)

## Project Overview

Pushup Challenge is a mobile-first PWA that tracks a daily pushup challenge where you do N pushups on day N of the year. By year end, you've done 1+2+...+365 = 66,795 pushups.

## Development

**No build system** - This is a static HTML site.

- **To develop:** Run `python3 -m http.server 8001` and open http://localhost:8001
- **To deploy:** Push to `gh-pages` branch for GitHub Pages hosting
- **Live site:** https://davidgedye.github.io/onemoreday/

## Features

- Shows remaining pushups for today (big number)
- Tracks cumulative year total in localStorage
- Missed days carry over (not reset daily)
- "Catch Up" button marks all days through today as complete
- "Ahead" state shows when you've done extra (blue number)
- Installable as PWA on iOS/Android home screens

## Files

- **index.html** - The entire app (HTML + CSS + JS in one file)
- **manifest.json** - PWA manifest for installation
- **sw.js** - Service worker for offline caching
- **icon-180.png** - App icon (180x180 PNG with pushup silhouette)
- **pushup.png** - Pushup line drawing displayed on the page

## Key Logic

**Remaining calculation:**
```javascript
requiredSoFar = dayNum * (dayNum + 1) / 2  // Gauss' formula
remaining = requiredSoFar - yearTotal
```

**State (localStorage):**
```javascript
{ yearTotal: number, year: number }
```

- `yearTotal` - cumulative pushups done this year
- `year` - resets yearTotal when a new year starts

## Service Worker Caching

Cache version is in `sw.js` as `CACHE_NAME`. Bump the version number when deploying changes to ensure users get updates.
