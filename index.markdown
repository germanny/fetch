---
title: Home
layout: page
header_js: |
  fetch('/assets/js/colors.json')
    .then(response => {
      console.log(response);
    })
---

## What is the Fetch API?

Fetch returns a "Promise" - an object that may produce a single value some time in the future (a resolved value or a reason it's not resolve). This response can be "fulfilled", "rejected", or "pending", allowing us to work with data asynchronously.

The response of a `fetch()` request is what's known as a `Stream` object, which means that when we call (for example) the `json()` method, a Promise is returned since the reading of the stream will happen asynchronously.

### Example:

#### colors.json

```
{
  "colors": [
    {
      "color": "black",
      "category": "hue",
      "type": "primary",
      "code": {
        "rgba": "[255,255,255,1]",
        "hex": "#000"
      }
    }
    ...
  ]
}
```

Let's say we want to fetch the data in this file:

```
fetch('/assets/js/colors.json')
  .then(response => { // do something
    console.log(response);
  });
```

The response tells you a lot about what's being returned (if the request is successful and a status, for example), but not the actual data itself (in this case, a list of colors). This will be represented as:

```
body: ReadableStream
```

[Next ->](/fetch-methods/ "Next")
