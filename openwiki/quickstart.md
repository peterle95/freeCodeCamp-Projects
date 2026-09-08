---
type: quickstart
title: freeCodeCamp Projects Wiki
description: Navigation guide for eight standalone browser projects, their runtime contracts, workflows, and maintenance boundaries.
tags: [repository, browser, navigation]
---

# freeCodeCamp Projects Wiki

This repository is a set of independent HTML/CSS/JavaScript learning projects, not a monorepo application. Start with [architecture and maintenance](architecture/overview.md), then route directly to the relevant project page:

- [Binary Converter](projects/binary-converter.md) — recursive conversion and timed call-stack animation.
- [Calorie Counter](projects/calorie-counter.md) — dynamic meal forms and calorie arithmetic.
- [Football Team Cards](projects/football-team-cards.md) — frozen team data, cards, and filters.
- [Music Player](projects/music-player.md) — audio/playlist state and CDN assets.
- [Rock Paper Scissors](projects/rock-paper-and-scissors.md) — first-to-three game lifecycle.
- [Role Play Game](projects/role-play-game.md) — location state machine and combat.
- [Spam Filter](projects/spam-filter.md) — deny-list regex classification.
- [Todo App](projects/todo-app.md) — localStorage task lifecycle.

## Task routing

| Intent | Canonical page and source entrypoints | Focused validation |
|---|---|---|
| Change a project UI or layout | Project page; `index.html`, `styles.css`, referenced DOM IDs/classes | Open page at desktop/mobile widths and exercise affected controls |
| Change project behavior | Project page; `script.js` symbols listed there | Run the page’s listed happy path, edge cases, and reset/error path |
| Add persistence or browser state | [Todo App](projects/todo-app.md); `taskData`, `localStorage`, `reset` | Reload, edit, delete, discard, and inspect stored JSON |
| Change audio/catalog behavior | [Music Player](projects/music-player.md); `userData`, `Audio`, render/navigation functions | Test play/pause boundaries, deletion, shuffle, empty reset, and CDN availability |
| Change game transitions | [Role Play Game](projects/role-play-game.md) or [Rock Paper Scissors](projects/rock-paper-and-scissors.md) | Exercise every route and terminal state; account for randomness |
| Change validation/classification | [Calorie Counter](projects/calorie-counter.md) or [Spam Filter](projects/spam-filter.md) | Test accepted, rejected, empty, and obfuscated inputs |
| Maintain generated documentation | [Architecture](architecture/overview.md), `/openwiki`, and `.github/workflows/openwiki-update.yml` | Run the documented OpenWiki workflow with credentials available |

## Common operating model

There are no package manifests, build commands, server APIs, migrations, or automated tests. Each page loads local CSS and JavaScript directly. Use a modern browser; a local server is optional and useful for projects with external assets or browser restrictions. Preserve HTML IDs and option values when changing JavaScript because they are the implicit module boundary.

## Scope boundary

The wiki documents source behavior and current caveats, including known implementation limitations. It does not claim backend security, production accessibility certification, or automated coverage where the repository provides none.
