Pure javascript function to load a page from supplied url, and execute the scripts that are found in it.

```curPage``` is a variable in main javascript to track the current page, and only load if the requested url if different from the saved page.

```
function fetchPage( url ) {
  if ( curPage == url ) return false
  fetch( url )
  .then( response => { return response.text() })
  .then( data => {
    const app = document.getElementById('main')
    app.innerHTML = data;
    // Load scripts in the order they are defined, Note that inserting scripts into an element using innerHTML doesnt work - hence this logic
    var scripts = app.querySelectorAll("script");
    if (scripts !== null && scripts.length > 0) {
      var loadScript = index => {
        if (index < scripts.length) {
          var newScript = document.createElement("script");
          if (scripts[index].innerText) {
            var inlineScript = document.createTextNode(scripts[index].innerText);
            newScript.appendChild(inlineScript);
          } else {
            newScript.src = scripts[index].src;
          }
          scripts[index].parentNode.removeChild(scripts[index]);
          newScript.addEventListener("load", event => loadScript(index + 1));
          newScript.addEventListener("error", event => loadScript(index + 1));
          app.appendChild(newScript);
        }
      }
      loadScript(0); // Start loading script 0. Function is recursive to load the next script after the current one has finished downloading.
    }
  })
  .catch( err => { console.warn('Something went wrong.', err) });
  curPage = url;
}
```
