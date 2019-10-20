---
title: Chain Responses
layout: page
header_js: |
  fetch('/assets/js/colors.json')
    .then(checkStatus)
    .then(parseJSON)
    .then(data => {
      console.log("Success! ", data);
    }).catch(function(err) {
      console.log('Failed! ' + err);
    });
---

## Chaining Promises

Chaining Promises lets you perform multiple tasks across different functions.

### Example

Helper functions to check the status of the response and return the appropriate Promise:

```
const checkStatus = response => {
  if (response.status < 200 || response.status >= 300) {
    return Promise.reject(new Error(response.status + ", " + response.statusText));
  }

  return Promise.resolve(response);
}

const parseJSON = response => response.json();
```

Now, hop through some checks and Promises:

```
fetch('/assets/js/colors.json')
  // if this resolves, go to next .then ...
  .then(checkStatus)

  // if this resolves and returns a Promise from the response.json(), go to the next .then ...
  .then(parseJSON)

  // do something with the data
  .then(data => {
    console.log("Success! ", data);
  })

  // but if the above failed, show an error
  .catch(function(err) {
    console.log('Failed! ' + err);
  });
```

[<- Previous](/fetch-methods/ "Previous")
[Next ->](/pros-and-cons/ "Next")
