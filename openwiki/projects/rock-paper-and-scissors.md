---
type: project-guide
title: Rock Paper Scissors
description: Best-of-three-rounds game with random computer choice, score display, and reset lifecycle.
tags: [browser, game, state]
---

# Rock Paper Scissors

`Rock-Paper-and-Scissors-Game/index.html` provides `rock-btn`, `paper-btn`, `scissors-btn`, `player-score`, `computer-score`, `results-msg`, `winner-msg`, `reset-game-btn`, and `.options-container`; CSS controls the layout and terminal visibility. The page loads `./script.js` and needs only browser APIs.

`getRandomComputerResult` returns one case-sensitive move. `hasPlayerWonTheRound` defines exactly: Rock beats Scissors, Scissors beats Paper, and Paper beats Rock. Thus each player move wins against that one computer move, ties against itself, and loses against the remaining move; `getRoundResults` increments `playerScore` only for the win, `computerScore` only for the loss, and neither for a tie. It returns the corresponding exact message (`Player wins! ...`, `It's a tie! ...`, or `Computer wins! ...`).

Each option listener passes its literal move to `showResults`. That function writes the round message to `results-msg`, writes both numeric scores to their spans, and when either reaches 3 writes `Player has won the game!` or `Computer has won the game!`, displays `reset-game-btn`, and hides `.options-container`. There is no input parser or invalid-move UI: only the three static buttons can provide valid values. The listeners remain attached after the terminal display, so programmatic or keyboard activation of hidden buttons could still mutate scores; normal browser interaction cannot see them. `resetGame` restores scores to `0`, hides reset, shows options, and clears winner/result text.

The three button IDs and exact move strings are the extension surface. Validate all nine player/computer combinations, three-point completion for either side, result/score text after each round, hidden options and visible reset at completion, and reset. There is no automated suite or build command.
