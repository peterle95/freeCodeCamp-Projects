---
type: project-guide
title: Spam Filter
description: Client-side deny-list classifier for common spam phrases and obfuscated money language.
tags: [browser, regex, validation]
---

# Spam Filter

`SpamFilter/index.html` provides `message-input`, `check-message-btn`, and `result`; `styles.css` controls the form and feedback presentation. `script.js` defines five case-insensitive regexes (`helpRegex`, `dollarRegex`, `freeRegex`, `stockRegex`, `dearRegex`) in `denyList`, and `isSpam(msg)` returns whether any matches.

The click handler rejects an empty message with an alert; otherwise it writes the spam/not-spam message and clears the field. The regex list is the extension seam: add a tested pattern to `denyList` while preserving boundary checks that prevent accidental substring matches. This is a heuristic classifier, not a complete spam detector or server-side security control.

Validate each current phrase, capitalization and common leetspeak variants, a clean message, and empty submission. There is no persistence, external service, test suite, or build command.
