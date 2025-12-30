# InteractiveDrawingApp

A lightweight, Microsoft Paint–style drawing application built with JavaFX.  
Draw shapes with live preview, customize stroke thickness, and keep the UI responsive with a clean MVC-style structure.

---

## Features

- Click-and-drag drawing with real-time shape preview
- Multiple tools (e.g., rectangle, circle/oval, polyline/squiggle — depending on your build)
- Color selection for strokes/fills (if enabled)
- Adjustable line thickness via slider (applies to the next shapes you draw)
- Central `PaintModel` that stores all shapes (model-driven rendering)

---

## Architecture

The project is organized around separation of concerns:

- **Model**
  - `PaintModel`: holds the list of shapes and any global state needed for rendering
  - Shape objects store geometry (points, bounds, etc.)
  - Style attributes (color, thickness) are managed via “selected state” objects (e.g., `SelectedColour`, `SelectedLine`)

- **View**
  - JavaFX canvas/pane responsible for rendering the shapes from the model
  - Panels for tool selection and thickness selection (slider)

- **Controllers / Tools**
  - Tool classes handle mouse events (`press`, `drag`, `release`) and create/update shapes
  - `LineThicknessSelector` (controller) updates the selected thickness state
  - `LineThicknessPanel` (view) contains the slider UI and forwards changes to the controller

This keeps shape logic local to each drawing tool while letting the model remain the single source of truth.
