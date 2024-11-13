Vanilla javascript method for adding a delay before execution

```
const delay = (delayMS) => {
  return new Promise(resolve => setTimeout(resolve, delayMS));
}
```

usage `delay(1000).then( () => { alert("hi"); });` which will wait for 1 second before running the function
