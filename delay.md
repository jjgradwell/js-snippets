```
const delay = (delayMS) => {
  return new Promise(resolve => setTimeout(resolve, delayMS));
}
```
usage `delay(1000).then( () => { });`
