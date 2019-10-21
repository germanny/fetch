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

### Example of manipulating meta tags for failed API calls

From [Understand the JavaScript SEO basics, by Google](https://developers.google.com/search/docs/guides/javascript-seo-basics#use-meta-robots-tags-carefully), though maybe this should be rewritten in a `try ... catch` statement.

```
fetch('/api/products/' + productId)
  .then(function (response) { return response.json(); })
  .then(function (apiResponse) {
    if (apiResponse.isError) {
      // get the robots meta tag
      var metaRobots = document.querySelector('meta[name="robots"]');
      // if there was no robots meta tag, add one
      if (!metaRobots) {
        metaRobots = document.createElement('meta');
        metaRobots.setAttribute('name', 'robots');
        document.head.appendChild(metaRobots);
      }
      // tell Googlebot to exclude this page from the index
      metaRobots.setAttribute('content', 'noindex');
      // display an error message to the user
      errorMsg.textContent = 'This product is no longer available';
      return;
    }
    // display product information
    // ...
  });
```

[<- Previous](/fetch-methods/ "Previous")
[Next ->](/pros-and-cons/ "Next")
