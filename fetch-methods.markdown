---
title: Fetch() Methods
layout: page
header_js: |
  fetch('/assets/js/colors.json')
    .then(response => response.json())
    .then(data => {
      console.log(data)
    })
---

## Fetch() Methods

`fetch()` returns only Promises. To use the returned value, we need to call [the appropriate method](https://fetch.spec.whatwg.org/#body-mixin) to extract the `body` and handle the data, i.e.:

```
arrayBuffer() (i.e. an array of bytes)
blob() (i.e., a file, an image, etc.)
formData()
json()
text()
```

The Fetch spec indicates each of these methods should return a Promise that resolves to the noted object (text, JSON, etc.).

### Example:

```
fetch('/assets/js/colors.json')
  .then(response => response.json()) // returns another Promise; if successful, .then ...
  .then(data => { // now we get the data
    console.log(data)
  })
```

[<- Previous](/ "Previous")
[Next ->](/chain-responses/ "Next")
