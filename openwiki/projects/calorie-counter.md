---
type: project-guide
title: Calorie Counter
description: Form-driven calorie budget, meal, snack, and exercise calculator with dynamic entries.
tags: [browser, forms, calculations]
---

# Calorie Counter

`calories-counter/index.html` defines the budget form, meal sections `breakfast`, `lunch`, `dinner`, `snacks`, and `exercise`, plus `entry-dropdown`, `add-entry`, `clear`, and `output`. `styles.css` uses CSS variables, Grid/Flexbox, percentage/max-width containers, and a mobile-first viewport design. The README recommends modern ES6+/Grid/Flexbox/custom-property browsers, direct opening, or `python -m http.server 8000` / `npx serve .`; it also records that persistence and food-database features are not implemented.

`addEntry` appends paired name/calorie controls to the selected section, deriving the next number from existing text inputs; the generated `type="number"` controls are then found by each section selector in `calculateCalories`. `cleanInputString` removes every `+`, `-`, and whitespace character before `Number` conversion, so signs are not preserved. `isInvalidInput` matches digit-plus-`e`-plus-digit forms case-insensitively; `getCaloriesFromInputs` alerts on the first match, sets shared `isError`, returns `null`, and stops that collection. Blank values become `Number("")` (zero), while non-numeric values not caught by the regex can become `NaN`; negative HTML input values are not separately rejected by JavaScript, and the cleaner strips their minus sign. Form submission calls `calculateCalories`, which prevents navigation, resets `isError`, and returns before rendering whenever any collection raised an error. On success, consumed calories are the four food sections; remaining is exactly `budget - consumed + exercise`. The current conditional labels negative remaining `Surplus` and non-negative remaining `Deficit`, then displays the absolute value. `clearForm` removes all dynamic fields, clears budget and output text, and adds `hide`; a successful calculation removes `hide`.

The HTML IDs and section classes are the change surface; preserve their alignment with the selectors. Validate by adding multiple entries in each category, calculating ordinary and invalid values, confirming the alert/error path, and clearing the form at desktop and mobile widths.
