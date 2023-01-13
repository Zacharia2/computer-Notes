```js
const contents = await fetch(url, {
  method: 'GET',
  headers: {
    'access-control-allow-origin': '*'
  }
}).then(res => res.text());
```