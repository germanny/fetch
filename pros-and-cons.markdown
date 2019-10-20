---
title: Pros and Cons of Fetch API
layout: page
---

# Pros and Cons of Fetch API

## Pros

- No need for extra dependencies
- Gets http requests native in ES6
- Low level and very specific API that's good for simplistic API calls.

## Cons

- The default `catch()` block doesn't get http status code errors (only things like `failed request` or `network error`)
- Fetch, similar to `XMLHttpRequest`, rejects the promise if there is a network error (e.g., the address cannot be resolved, server is unreachable, or CORS not permitted). 404, 500, etc. errors are treated as **success** and do not enter the `catch()` block.
- The basic usage has pretty low reusability.

```
// This resolves an error only if there is a network error:
fetch(url).then(response => response.json())
  .then(result => console.log('success:', result))
  .catch(error => console.log('error:', error));

// To register response status errors, the function is more complicated:
fetch(url)
  .then(response => {
    // We have to check that the response is "ok" or the status code is successful every. single. time.:
    if (response.status >= 200 && response.status < 300) {
      return response.json()
    } else {
      return Promise.reject('something went wrong!')
    }
  )
  .then(result => console.log('success:', result))
  .catch(error => console.log('error:', error));
```

- When sending `POST` requests, JSON data has to be converted to a string and the `Content-Type` header must indicate that the payload is JSON, otherwise the server will treat it as a string:

```
fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    var: 'value',
    var2: 'value 2'
  })
});
```
