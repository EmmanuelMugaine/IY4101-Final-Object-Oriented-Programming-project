# Shape Management System
 
A Java console application that models geometrical shapes (Rectangle, Square,
Circle, Triangle) using object-oriented principles, and lets a user add,
remove, inspect, translate, and scale a list of shapes through a menu.
 
## Overview
 
This program was built for IY4101 Practical Programming Assignment 2. It
demonstrates:
 
- Abstract classes and method overriding (**Shape**)
- Inheritance across a class hierarchy (**Rectangle, Square, Circle,
  Triangle** *all extend* **Shape**)
- Composition (**Shape** has a **Coordinates** object rather than extending it)
- Polymorphism (**ShapeList** stores and operates on **Shape** references without
  knowing the concrete subclass)
- Defensive programming (bounds-checking on list positions so invalid input
  does not crash the program)

 ### Requirements

- Java JDK 17 or later
- Command line or IDE (IntelliJ IDEA, Eclipse or VS Code)
## Features

- Add Rectangle, Square, Circle and Triangle objects
- Display information about individual or all shapes
- Calculate area and perimeter
- Translate all shapes by a specified distance
- Scale all shapes by multiplication or division
- Remove shapes by list position
- Input validation and graceful error handling

## Class structure
 
| Class | Purpose |
|---|---|
| **Coordinates** | Represents an (x, y) point; provides distance, translate, scale, display |
| **Shape** (abstract) | Base class for all shapes; holds a position and side count; declares `getArea()`, `getPerimeter()`, `display()` as abstract |
| **Rectangle, Square, Circle** | Concrete shapes; each overrides `getArea()`, `getPerimeter()`, `scale()`, `display()` |
| **Triangle** | Concrete shape with three vertices; overrides `translate()` and `scale()` in addition to the above, since it must move/scale all three points |
| **ShapeList** | Stores shapes in an `ArrayList<Shape>`; provides add/remove/get/area/perimeter/translate/scale/display operations, with bounds-checking on position-based methods |
| **ShapeManagement** | Console entry point; runs the menu loop and calls the appropriate `ShapeList` method for each option |

## How to compile and run
 
From the project root (where the `Final_Assessment` package folder lives):
 
```bash
javac Final_Assessment/*.java
java Final_Assessment.ShapeManagement
```
 
## Menu options
 
1. Add a shape
2. Remove a shape by position
3. Get information about a shape by position
4. Area and perimeter of a shape by position
5. Display information of all shapes
6. Translate all shapes
7. Scale all shapes
0. Quit program

## Notes

- When adding a shape (option 1), you will be asked to choose a shape type
(Rectangle, Square, Circle, or Triangle) and then enter its coordinates and
dimensions.
 
- Positions in the list are zero-indexed (the first shape added is position 0).

## Design decisions
 
- **Scaling uses integer division for coordinates.** Following the assignment
  specification, Coordinates.scale() truncates when dividing (e.g. 7 / 2 =
  3), because x and y are stored as int.
- **Circle's `sides` value is set to 1.** The specification does not define
  a side count for a circle; 1 was chosen as a reasonable convention.
- **Invalid list positions return sentinel values rather than throwing
  exceptions.** `ShapeList.getShape()` and `removeShape()` return `null`,
  and `area()`/`perimeter()` return `-1`, when given an out-of-range
  position. A message is printed to the console in each case, and the
  program continues running rather than crashing.
