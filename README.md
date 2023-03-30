# readycase
## Drag and drop functionality via the keyboard
Whilst the functionality could be accomplished any number of ways, when you move away from native HTML elements into complex interactions using `<div>` and `<span>` elements. Accessibility requirements become more difficult to implement.

**Individual items** (items which will be moved between cells / days of the week)
* Every item contained in an `<li>` element
* Every item has a checkbox with appropriate labelling. The below example uses `aria-labelledby` however a `<label>` element, or `aria-label` could be alternatives

```html
<li><input type="checkbox" aria-labelledby="lbl1"> <span id="lbl1">10:00-10:00 (COMM)</span></li>
```

**Individual cells** (days of the week)
* All cells are keyboard focusable, the user can move in any direction. Each cell has `tabindex="1"`
* When a cell receives keyboard focus, the buttons **drop** and **uncheck** are visible. Buttons use native HTML `<button>` elements
* The buttons receive keyboard focus directly after the cell, the focus order is **cell > drop button > uncheck button**
* When a cell loses keyboard focus, the buttons **drop** and **uncheck** are hidden

**Workflow**
* Clicking **drop** will move the checked items from the source cell to the destination cell
* Clicking **uncheck** will uncheck the items in the source cell

### Relevant WCAG success criteria
* [2.1.1 Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html) - all functionality must be available from the keyboard
and, shortcut and access keys do not conflict with browser or assistive technology shortcuts
* [2.5.1 Pointer Gestures](https://www.w3.org/WAI/WCAG21/Understanding/pointer-gestures.html) - path-based multi-point functionality can be operated with single-point actions

## Aria live region
These regions create aural zones which the screen reader uses to announce content. They're typically created to provide audible feedback for clientside content updates.

**Move Assist**
* Create a live region container around all of the updates
* Add `role="status` to the container
* Add the container content via Javascript. Adding the content to the live region will trigger the screen reader to announce the content. However it only announces **new** content
* Adding `aria-atomic="true"` to the container will trigger the screen reader to announce all content, both old and new (though has had patchy support). To reliability trigger the screen reader to announce all content each time regardless if anything has changed. The entire live region container needs to be reset to empty, and text readded.
* The live region works best with only text content (no controls)

```html
<div role="status">

<ul>
<li>Item that can be moved</li>
<li>Item with issues</li>
</ul>

</div>
```

### Relevant WCAG success criteria
* [4.1.3 Status Messages](https://www.w3.org/WAI/WCAG21/Understanding/status-messages.html) - all client-side updated success or action outcome messages use role=status

## Clickable size
* [WCAG 2.2 requirements](https://www.w3.org/TR/WCAG22/#target-size-minimum) set a minimum target size for pointer inputs to be 24 x 24 pixels. Whilst you could alternate between pixel size depending on device, users who navigate with a mouse and have mobility impairments will still encounter difficulties if the target size remains the current dimenions. Increasing it to the minimum 24 x 24 pixel size will position the product to be more forward focused for WCAG 2.2 due out later this year.
