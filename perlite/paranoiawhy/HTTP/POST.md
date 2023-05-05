# fetch

```js
const form = document.querySelector("form");

form.onsubmit = (e) => {
  e.preventDefault();
  const data = new URLSearchParams(new FormData(form));
  fetch("http://localhost:1234/upload", {
    method: "POST",
    body: data,
  });
};
```
