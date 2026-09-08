---
type: project-guide
title: Football Team Cards
description: Static Argentina 1986 team directory with rendered player cards and filters.
tags: [browser, rendering, filtering]
---

# Football Team Cards

`Football-Team-Cards/index.html` supplies team metadata fields, the `players` select, and `player-cards`; `styles.css` controls the team header and card grid. `script.js` owns the frozen `myFavoriteFootballTeam` object: Argentina, Football, 1986, coach Carlos Bilardo, and 22 players with `name`, `position`, `number`, `isCaptain`, and nullable `nickname`.

The script destructures metadata into the header, and `setPlayerCards(arr = players)` maps records to cards, showing `(Captain)` and `N/A` for absent nicknames. The select change handler clears the container and filters by nickname presence or the exact positions `forward`, `midfielder`, `defender`, and `goalkeeper`; the default restores all players. `Object.freeze` protects only the top-level team object, so data changes belong in the canonical literal and must preserve the rendering fields.

The DOM IDs and position option values are the public internal surface. On every dropdown change, the listener first sets `playerCards.innerHTML = ""`; `setPlayerCards` then appends the selected cards with `innerHTML +=`, so repeated filtering does not accumulate stale cards. To add a filter, add its option value in `index.html` and a matching `case` that passes a filtered player array; an unsupported value falls through to the default `setPlayerCards()` and restores the full roster. Validate initial 22-card rendering, each filter, captain/nickname display, repeated filter changes, and return to the default selection in a browser; there are no tests or build scripts.
