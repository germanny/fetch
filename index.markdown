---
title: Home
layout: page
header_js: |
  fetch('/assets/js/colors.json')
    .then(response => { // do something
      console.log(response);
    });
---

## What is the Fetch API?

The Fetch API is a promised-based API that can perform server requests to fetch data asynchronously using plain Javascript.

Fetch returns an object containing the response (the promise) from the server, indicating the status and the headers. If there is a network error or the url doesn't resolve or whatever, then the promise will be rejected. We'll check the status and if it's looking good, we need to use a second method to call the data.

(The response of a Fetch request is what's known as a `Stream` object, which means that if, for example, we call the `json()` method, a Promise is returned since the reading of the stream will happen asynchronously.)

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

Let's say we want to check the response for this file:

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

[Next ->](/response-metadata-and-types/ "Next")
