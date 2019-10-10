---
title: Response Metadata and Types
layout: page
header_js: |
  fetch('/assets/js/colors.json')
    .then(checkStatus)
    .then(function(response) {
      console.log(response.headers.get("Content-Type"));
      console.log(response.headers.get("Date"));

      console.log(response.status);
      console.log(response.statusText);
      console.log(response.type);
      console.log(response.url);
    })
    .catch(function(error) {
      console.log('Fetch Error: ' + error.message);
    });
---

## Response Metadata and Types

### Example:

```
fetch('/assets/js/colors.json')
  .then(checkStatus)

  .then(function(response) {
    console.log(response.headers.get("Content-Type"));
    console.log(response.headers.get("Date"));

    console.log(response.status);
    console.log(response.statusText);
    console.log(response.type);
    console.log(response.url);
  })

  .catch(function(error) {
    console.log('Fetch Error: ' + error.message);
  });
```

### Response Types

- **basic**: no restrictions on what you can view
- **cors**: response from different origin and restricts the headers you can view (though includes Content-Type)
- **opaque**: response from different origin and no CORS header; we won't be able to read the data or status returned so we cannot see if the request was successful or not

[<- Previous](/chain-responses/ "Previous")
