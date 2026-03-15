# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Smith Legacy** is a classroom gamification/achievement system for "Mr. Smith's" class. Students sign up, claim achievements, and get ranked on a leaderboard. Moderators review and approve/deny achievement claims.

## Architecture

This is a **single-file application** — all HTML, CSS, and JavaScript live in `index.html`. There is no build process, no package manager, and no separate files.

**Stack:**
- Vanilla JS + HTML/CSS (no frameworks)
- Firebase Firestore (compat SDK v8) for the database and real-time updates
- No authentication library — custom username + 4-digit PIN login

**Firestore Collections:**
- `users` — accounts with fields: `pass` (PIN string), `isMod` (bool), `period` (string), `claims` (map of `achId → "verified"|"pending"`)
- `claims` — pending approval requests with fields: `user`, `achId`, `time`

## Key Concepts

**Achievements** are defined as a hardcoded JS array inside `index.html`. Each has an `id`, `name`, `desc`, and `rarity` (`"easy"`, `"normal"`, `"hard"`, `"extreme"`).

**Views** are toggled by showing/hiding `<div>` sections — there is no router. The main views are: login, signup, student dashboard, moderator dashboard, leaderboard.

**Moderator accounts** are identified by `isMod: true` in Firestore. The `milesthegoat` account has special permission to delete student accounts.

## Development

Open `index.html` directly in a browser or serve it with any static file server:
```
npx serve .
# or
python -m http.server
```

No build, no lint, no tests.
