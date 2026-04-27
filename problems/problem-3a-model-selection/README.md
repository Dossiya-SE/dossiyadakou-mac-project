# Homework M13 - Object-Oriented Calculator System

## Files
- `HW_M13.py` main Python script
- `figures/` optional saved graph outputs
- `results/` optional saved console outputs or screenshots
- `README.md` project description

## Summary
This project implements an object-oriented calculator system in Python. It includes a basic calculator, a scientific calculator, a graphical calculator, and a GUI for the basic calculator.

The project demonstrates inheritance, mathematical function implementation, plotting, input validation, and event-driven GUI programming using `tkinter`.

## Components
- `DossiyaBasicCalc` performs addition, subtraction, multiplication, and division.
- `DossiyaScientificCalc` extends the basic calculator with logarithm, exponent, sine, and cosine.
- `DossiyaGraphicalCalc` extends the scientific calculator with plotting functionality.
- `CalculatorGUI` provides an interactive GUI for the four basic operations.

## Mathematical Focus
The code enforces key mathematical constraints:
- Division is undefined when the denominator is zero.
- Logarithm is only defined for positive inputs.
- Trigonometric functions use radians.
- The graphical calculator plots a function over a fixed domain from `0` to `4π`.

## Execution Flow
1. The program prints one sample output for the basic calculator.
2. The program prints one sample output for the scientific calculator.
3. The program displays one graphical calculator plot.
4. After the plot is closed, the GUI opens.

## Main Result
The project shows how object-oriented programming can organize mathematical computation, visualization, and user interaction into a clean engineering workflow.
