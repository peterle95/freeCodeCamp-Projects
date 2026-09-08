---
type: project-guide
title: Binary Converter
description: Recursive decimal-to-binary converter with an educational call-stack animation.
tags: [browser, recursion, dom]
---

# Binary Converter

`BinaryConverter/index.html` loads `styles.css` and `script.js`; the script owns `number-input`, `convert-btn`, `result`, and `animation-container`. CSS presents the converter and `.animation-frame` stack cards. There is no persistence or external dependency.

`decimalToBinary(input)` returns `String(input)` for 0/1; otherwise it recurses on `Math.floor(input / 2)` and appends `input % 2`. `checkUserInput` uses `parseInt`, so fractional text such as `5.9` becomes 5, and strings with a numeric prefix may be accepted; a very large value can lose integer precision and recursion is not designed for arbitrary bounds. Blank, `NaN`, and negative parsed values alert `Please provide a decimal number greater than or equal to 0` and return. Valid non-5 inputs render the conversion and clear `numberInput.value`; invalid input is not cleared. Click and Enter keydown (only `e.key === "Enter"`) call the same function.

Input 5 intentionally takes `showAnimation`, without clearing the input. Its fixed `animationData` inserts frames for 5 at 1000 ms, 2 at 1500 ms, and 1 at 2000 ms; it replaces their text with explanatory messages at 15000, 10000, and 5000 ms, removes them at 20000, 15000, and 10000 ms, and writes the final `decimalToBinary(5)` result at 20000 ms. The IDs `1`, `2`, and `5` are therefore timer lookup contracts. Repeated submissions can schedule overlapping callbacks that address the same IDs, remove nodes before another callback expects them, or overwrite the result; there is no cancellation or submission lock. The animation demonstrates the recursive call stack rather than dynamically deriving frames for arbitrary input.

Validate 0, ordinary integers, fractional/prefix text, large values, blank/non-numeric/negative input, Enter, and the full 20-second 5 animation. Also test repeated 5 submissions to expose timer overlap. There is no automated test or build command.
