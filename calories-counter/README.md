# Calorie Counter

A web-based calorie tracking application that helps users monitor their daily caloric intake and exercise. Users can set a daily calorie budget, add food entries for different meals, log exercise activities, and calculate remaining calories.

## What I Learned

### 1. Template Literals
Template literals (using backticks `) allow for multi-line strings and string interpolation:
```javascript
const HTMLString = `
  <label for="${entryDropdown.value}-${entryNumber}-name">Entry ${entryNumber} Name</label>
  <input type="text" id="${entryDropdown.value}-${entryNumber}-name" placeholder="Name" />
  <label for="${entryDropdown.value}-${entryNumber}-calories">Entry ${entryNumber} Calories</label>
  <input
    type="number"
    min="0"
    id="${entryDropdown.value}-${entryNumber}-calories"
    placeholder="Calories"
  />`;
```

### 2. Event Listeners
Event listeners handle user interactions and form submissions:
- **Click events**: `addEntryButton.addEventListener("click", addEntry)` and `clearButton.addEventListener("click", clearForm)`
- **Form submission**: `calorieCounter.addEventListener("submit", calculateCalories)`

### 3. DOM Manipulation
- **Querying elements**: `document.getElementById()`, `document.querySelector()`, `document.querySelectorAll()`
- **Dynamic HTML insertion**: `insertAdjacentHTML()` to add new form fields
- **Class manipulation**: `classList.add()`, `classList.remove()` for showing/hiding elements

### 4. Form Handling
- **Preventing default behavior**: `e.preventDefault()` to stop form submission
- **Input validation**: Regex patterns to check for invalid inputs like scientific notation
- **Dynamic form generation**: Creating new input fields based on user selections

### 5. Array Methods
- **Array.from()**: Converting NodeList to Array for easier manipulation
- **forEach loops**: Iterating through form inputs to calculate totals

### 6. CSS Variables
Using CSS custom properties for consistent theming:
```css
:root {
  --light-grey: #f5f6f7;
  --dark-blue: #0a0a23;
  --fcc-blue: #1b1b32;
  /* ... more variables */
}
```

### 7. Responsive Design
- Mobile-first approach with viewport meta tag
- Flexible container widths using percentages and max-width
- CSS Grid and Flexbox for layout

## Key Features

- **Daily Calorie Budget**: Set your target daily calorie intake
- **Meal Tracking**: Log breakfast, lunch, dinner, and snacks
- **Exercise Logging**: Track calories burned through exercise
- **Dynamic Form Fields**: Add multiple entries for each meal
- **Real-time Calculation**: Calculate remaining calories instantly
- **Clear Functionality**: Reset all form data with one click
- **Input Validation**: Prevents invalid inputs and provides user feedback

## How to Run

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- No additional software installation required

### Steps
1. **Download/Clone** the project files to your local machine
2. **Navigate** to the project directory in your file explorer
3. **Open** `index.html` in your web browser
   - Double-click the file, or
   - Drag and drop it into your browser window, or
   - Right-click and select "Open with" → your preferred browser

### Alternative: Using a Local Server
If you prefer to run it on a local server:

1. **Using Python** (if installed):
   ```bash
   python -m http.server 8000
   ```
   Then open `http://localhost:8000` in your browser

2. **Using Node.js** (if installed):
   ```bash
   npx serve .
   ```

3. **Using VS Code**: Install the "Live Server" extension and right-click `index.html` → "Open with Live Server"

## File Structure

```
calorieCounter/
├── index.html      # Main HTML structure
├── styles.css      # CSS styling and layout
├── script.js       # JavaScript functionality
└── README.md       # This file
```

## Browser Compatibility

This application works in all modern browsers that support:
- ES6+ JavaScript features
- CSS Grid and Flexbox
- CSS Custom Properties (variables)

## Future Enhancements

- Local storage to persist data between sessions
- Food database with common items and calorie counts
- Progress tracking over time
- Export functionality for meal plans
- Mobile app version
