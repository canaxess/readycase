# readycase
## Drag and drop functionality via the keyboard
**Individual items**
* Every item contained in an `<li>` element
* Every item has a checkbox with appropriate labelling

```html
<li><input type="checkbox" aria-labelledby="lbl1"> <span id="lbl1">10:00-10:00 (COMM)</span></li>
```

**Individual cells**
* All cells are keyboard focusable, the user can move in any direction. Each cell has `tabindex="1"`
* When a cell receives keyboard focus, the buttons **drop** and **uncheck** are visible. Buttons use native HTML `<button>` elements
* The buttons receive keyboard focus directly after the cell, the focus order is **cell > drop button > uncheck button**
* When a cell loses keyboard focus, the buttons **drop** and **uncheck** are hidden

**Workflow**
* Clicking **drop** will move the checked items from the source cell to the destination cell
* Clicking **uncheck** will uncheck the items in the source cell
