
```
const checkbox = document.getElementsByName("type")
checkbox.forEach( item => {
  item.addEventListener('click', () => {
    state = item.checked // Store the checkbox status
    for( var cb of checkbox ) cb.checked = false; // Unchek all checkboxes
    item.checked = state // Restore the state for current checkbox
  })
});
```
