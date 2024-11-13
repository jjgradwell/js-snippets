Vanilla JavaScript code to uncheck all check boxes, except for the currently checked item

```
const checkbox = document.getElementsByName("type")
checkbox.forEach( item => {
  item.addEventListener('click', () => {
    let state = item.checked // Store the checkbox state
    for( var cb of checkbox ) cb.checked = false; // Uncheck all checkboxes
    item.checked = state // Restore the state for current checkbox
  })
});
```

