---
type: architecture-guide
title: Repository architecture and maintenance
description: Runtime model, project boundaries, history, validation, and the OpenWiki automation that maintains this documentation.
tags: [architecture, maintenance, operations]
---

# Repository architecture and maintenance

## Runtime model

The root contains eight unrelated static browser applications. Each project has an `index.html` composition root, local `styles.css`, and a page-loaded `script.js`; there is no package manifest, shared module, server API, database, migration, build command, or automated test suite. HTML IDs/classes are implicit internal APIs. JavaScript executes after the markup because the script tags are at the end of each body. The only runtime dependencies beyond browser APIs are Music Player’s Google Fonts styling and remote MP3 URLs.

| Project | Script entrypoint | Required static DOM contract | Main dynamic surface | Failure if renamed |
|---|---|---|---|---|
| BinaryConverter | `BinaryConverter/index.html` → `script.js` | `number-input`, `convert-btn`, `result`, `animation-container`; input/button/result controls | timed `.animation-frame` nodes with IDs `1`, `2`, `5` | null access/listener failure or animation lookup/removal failure |
| calories-counter | `calories-counter/index.html` → `./script.js` | `calorie-counter`, `budget`, `entry-dropdown`, `add-entry`, `clear`, `output`, sections `breakfast`, `lunch`, `dinner`, `snacks`, `exercise`, each `.input-container` | generated name/calorie inputs inside section containers | listener failure, missing section query, or no output |
| Football-Team-Cards | `Football-Team-Cards/index.html` → `script.js` | `team`, `sport`, `year`, `head-coach`, `player-cards`, `players` select | `.player-card` markup | header assignment/listener/render failure |
| Music-Player | `Music-Player/index.html` → `script.js` | `playlist-songs`, `play`, `pause`, `next`, `previous`, `shuffle`, `player-song-title`, `player-song-artist` | playlist `<li>`/buttons and optional Reset Playlist | listener/display/render failure; inline ID lookup failure |
| Rock-Paper-and-Scissors-Game | `Rock-Paper-and-Scissors-Game/index.html` → `./script.js` | `rock-btn`, `paper-btn`, `scissors-btn`, `player-score`, `computer-score`, `results-msg`, `winner-msg`, `reset-game-btn`, `.options-container` | visibility and text only | listener/property failure or terminal UI failure |
| RolePlayGame | `RolePlayGame/index.html` → `script.js` | `button1`–`button3`, `text`, `xpText`, `healthText`, `goldText`, `monsterStats`, `monsterName`, `monsterHealth` | button handlers and text/state updates | initial handler/property failure or invisible/missing combat UI |
| SpamFilter | `SpamFilter/index.html` → `./script.js` | `message-input`, `result`, `check-message-btn` | result text | click listener or result update failure |
| Todo-App | `Todo-App/index.html` → `script.js` | `task-form`, `confirm-close-dialog`, `open-task-form-btn`, `close-task-form-btn`, `add-or-update-task-btn`, `cancel-btn`, `discard-btn`, `tasks-container`, `title-input`, `date-input`, `description-input` | task cards with inline `editTask`/`deleteTask` handlers | initialization failure; missing card parent IDs break edit/delete |

| Project | Script entrypoint | Required static DOM contract | Main dynamic surface | Failure if renamed |
|---|---|---|---|
| BinaryConverter | `BinaryConverter/index.html` → `script.js` | `number-input`, `convert-btn`, `result`, `animation-container` | timed `.animation-frame` nodes with IDs `1`, `2`, `5` |
| calories-counter | `calories-counter/index.html` → `./script.js` | `calorie-counter`, `budget`, `entry-dropdown`, `add-entry`, `clear`, `output`, sections `breakfast`, `lunch`, `dinner`, `snacks`, `exercise` | generated name/calorie inputs inside section `.input-container`s |
| Football-Team-Cards | `Football-Team-Cards/index.html` → `script.js` | `team`, `sport`, `year`, `head-coach`, `player-cards`, `players` | `.player-card` markup |
| Music-Player | `Music-Player/index.html` → `script.js` | playlist, `play`, `pause`, `next`, `previous`, `shuffle`, `player-song-title`, `player-song-artist` | playlist `<li>`/buttons and optional Reset Playlist |
| Rock-Paper-and-Scissors-Game | `Rock-Paper-and-Scissors-Game/index.html` → `./script.js` | `rock-btn`, `paper-btn`, `scissors-btn`, `player-score`, `computer-score`, `results-msg`, `winner-msg`, `reset-game-btn`, `.options-container` | visibility and text only |
| RolePlayGame | `RolePlayGame/index.html` → `script.js` | `button1`–`button3`, `text`, `xpText`, `healthText`, `goldText`, `monsterStats`, `monsterName`, `monsterHealth` | button handlers and text/state updates |
| SpamFilter | `SpamFilter/index.html` → `./script.js` | `message-input`, `result`, `check-message-btn` | result text |
| Todo-App | `Todo-App/index.html` → `script.js` | task form/buttons, `confirm-close-dialog`, title/date/description inputs, `tasks-container` | task cards with inline `editTask`/`deleteTask` handlers |

Renaming any listed required element causes `getElementById`/`querySelector` to return null and later listener/property access to fail; renaming dynamic classes or IDs breaks CSS, lookup, or delegated inline handlers. Keep select option values and script-relative paths synchronized. Project READMEs generally permit opening `index.html` directly; `calories-counter/README.md` explicitly offers `python -m http.server 8000`, `npx serve .`, or VS Code Live Server and lists modern ES6+, Grid/Flexbox, and CSS custom properties. Music’s external fonts/audio may require network access.

## History and provenance

Git history shows incremental, independently added projects (`projects`, Todo App, Football Team Cards, Music Player, and the later SpamFilter commit) rather than a shared product migration. That provenance is a maintenance boundary: attribute changes to the affected project, do not infer cross-project APIs, and use `git log` when a README or implementation rationale is ambiguous. Preserve the standalone layout unless a deliberate cross-project architecture is introduced.

## OpenWiki operational workflow

`.github/workflows/openwiki-update.yml` runs manually or daily at `0 8 * * *` on Ubuntu with Node 22. It has content and pull-request write permission, checks out full history (`fetch-depth: 0`) because OpenWiki compares against prior documented commits, installs pinned `openwiki@0.3.3`, `mermaid@11.16.0`, and `jsdom@29.1.1`, then runs `openwiki code --update --print`. `OPENWIKI_PROVIDER`, `OPENWIKI_MODEL_ID`, and `OPENWIKI_LANGSMITH_API_KEY` configure the run; `LANGSMITH_API_KEY`, `LANGCHAIN_PROJECT`, and `LANGCHAIN_TRACING_V2` enable optional tracing. Credentials are repository secrets and must never be copied into wiki prose. The create-pull-request step includes `openwiki`, `AGENTS.md`, `CLAUDE.md`, and the workflow itself, using branch `openwiki/update` and the `docs: update OpenWiki` commit/title. Checkout depth, pinned versions, secrets, and generated paths are operational invariants.

## Validation

Open a changed project in a modern browser and exercise its focused flow and failure cases from the project page. For external audio, confirm network access. There is no repository-wide test command. Documentation changes are validated by the OpenWiki workflow and its Mermaid/jsdom tooling.
