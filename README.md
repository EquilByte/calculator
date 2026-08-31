# Calculator

A lightweight, dependency-free calculator built with HTML, CSS, and vanilla JavaScript. The application runs entirely in the browser and provides a compact, glass-style interface for basic arithmetic.

## Table of contents

- [Overview](#overview)
- [Features](#features)
- [Technology](#technology)
- [How it works](#how-it-works)
- [Project structure](#project-structure)
- [Getting started](#getting-started)
- [Usage](#usage)
- [Calculation behavior](#calculation-behavior)
- [Customization](#customization)
- [Known limitations](#known-limitations)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository contains a single-page calculator that does not require a package manager, build process, framework, or backend. The interface is defined in `caculator.html`, styled by `main.css`, and powered by `script.js`.

The calculator keeps the current input in a buffer, stores a running total, and applies the selected operator when the next operation is requested. All interaction currently takes place through the on-screen buttons.

## Features

- Addition, subtraction, multiplication, and division
- Number entry using digits from 0 through 9
- Clear button for resetting the current calculation
- Backspace button for removing the most recently entered digit
- Equals button for displaying the result
- Sequential calculations using a stored running total
- Scrollable result display for values that exceed the visible width
- Centered, glass-style user interface
- Hover and active states for calculator buttons
- No external libraries or runtime dependencies

## Technology

| Technology | Purpose |
| --- | --- |
| HTML5 | Defines the calculator display and button layout |
| CSS3 | Provides sizing, spacing, colors, glass effects, and interaction states |
| JavaScript | Handles input, operator selection, arithmetic, and display updates |

## How it works

The JavaScript implementation uses three pieces of state:

| Variable | Responsibility |
| --- | --- |
| `buffer` | Holds the number currently shown on the calculator display |
| `runningTotal` | Stores the accumulated result while a calculation is in progress |
| `previousOperator` | Records the arithmetic operator that should be applied next |

A click listener is attached to the calculator button container. Each button's visible text is passed to `buttonClick()`, which routes numeric input to `handleNumber()` and symbols to `handleSymbol()`.

Arithmetic is performed by `flushOperation()`. When an operator is selected, the current buffer is converted to an integer and either stored as the initial running total or combined with the existing total. The display is refreshed after every button click.

## Project structure

```text
calculator/
├── LICENSE
├── caculator.html
├── main.css
└── script.js
```

### File responsibilities

- **`caculator.html`** contains the document structure, calculator screen, button rows, stylesheet reference, and script reference.
- **`main.css`** defines the centered layout, translucent calculator panel, display, button sizing, colors, and interactive states.
- **`script.js`** manages calculator state, input routing, arithmetic operations, clearing, backspacing, and display updates.
- **`LICENSE`** contains the BSD 3-Clause license terms.

> The HTML entry file is currently named `caculator.html`. Use that exact spelling when opening the application.

## Getting started

### Prerequisites

You only need:

- A modern web browser
- Git, if you want to clone the repository

There are no packages to install and no build command to run.

### Clone the repository

```bash
git clone https://github.com/EquilByte/calculator.git
cd calculator
```

### Run the calculator

Open `caculator.html` in a web browser. Because the project uses only local HTML, CSS, and JavaScript files, it can run directly from the cloned directory.

You can also download the repository as a ZIP archive from GitHub, extract it, and open `caculator.html`.

## Usage

1. Select one or more digit buttons to enter the first number.
2. Select an arithmetic operator: `+`, `−`, `×`, or `÷`.
3. Enter the next number.
4. Select `=` to display the result, or select another operator to continue the calculation.
5. Use `←` to remove the last digit from the current input.
6. Use `C` to reset the display and running total to zero.

### Controls

| Control | Action |
| --- | --- |
| `0`–`9` | Appends a digit to the current input |
| `+` | Selects addition |
| `−` | Selects subtraction |
| `×` | Selects multiplication |
| `÷` | Selects division |
| `=` | Applies the pending operation and displays the result |
| `←` | Removes the last digit, or returns a one-digit input to zero |
| `C` | Clears the current input and running total |

## Calculation behavior

The calculator processes operations sequentially rather than applying mathematical operator precedence.

For example, entering:

```text
2 + 3 × 4 =
```

first calculates `2 + 3`, then multiplies that running total by `4`.

Numeric input is parsed with JavaScript's `parseInt()`, so the interface is designed for whole-number entry. Division may still produce a decimal result. After a completed calculation, selecting `C` returns both the display and the running total to `0`.

## Customization

The project is intentionally small, so its appearance and behavior can be changed directly in the source files.

### Interface styling

Edit `main.css` to adjust:

- The page background
- Calculator dimensions
- Panel transparency and blur
- Button and display colors
- Border radius and shadows
- Font sizes
- Hover and active states

The main layout selectors are:

- `body` for page alignment and background
- `.wrapper` for the calculator container
- `.screen` for the display
- `.calc-button-row` for button rows
- `.calc-button`, `.calc-button-double`, and `.calc-button-triple` for button sizing

### Calculator behavior

Edit `script.js` to change calculation rules or add input methods. The main functions are:

| Function | Purpose |
| --- | --- |
| `buttonClick(value)` | Routes each clicked value and refreshes the screen |
| `handleSymbol(symbol)` | Processes clear, equals, backspace, and operator symbols |
| `handleMath(symbol)` | Stores an operator and manages the running total |
| `flushOperation(intBuffer)` | Applies the pending arithmetic operation |
| `handleNumber(numberString)` | Adds a digit to the current buffer |
| `init()` | Registers the calculator's click listener |

When changing button labels in the HTML, keep the matching symbols in `handleSymbol()` and `flushOperation()` synchronized because the event handler uses each button's visible text.

## Known limitations

The current implementation is deliberately focused on basic arithmetic:

- Input is limited to whole numbers because values are parsed with `parseInt()`.
- There is no decimal-point button.
- Negative numbers cannot be entered directly, although subtraction can produce a negative result.
- Operations are evaluated from left to right without operator precedence.
- Input is handled through on-screen clicks; keyboard controls are not implemented.
- The project does not include automated tests.
- Division by zero follows JavaScript number behavior and is not handled with a custom error message.
- Very large or unusual results are displayed without custom formatting.

## Contributing

Contributions can be made by forking the repository and proposing changes through a pull request.

A focused contribution workflow is:

1. Fork the repository.
2. Create a branch for the change.
3. Update the relevant HTML, CSS, or JavaScript file.
4. Open `caculator.html` in a browser and test the affected controls.
5. Commit the change with a clear message.
6. Open a pull request describing the problem and the solution.

Useful areas for improvement include keyboard input, decimal support, clearer division-by-zero handling, responsive sizing, accessibility attributes, and automated tests. Any new behavior should be documented in this README and tested across the calculator controls it affects.

## License

This project is distributed under the BSD 3-Clause License. See [LICENSE](LICENSE) for the complete terms.
