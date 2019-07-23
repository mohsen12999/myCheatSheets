# Progressive Web App

* Audience
* Platforms
* Connectivity
* Data cost
* Usage contexts

[Lighthouse](https://github.com/googlechrome/lighthouse) analyzes web apps and web pages, collecting modern performance metrics and insights on developer best practices.

[Workbox](https://developers.google.com/web/tools/workbox/) is a set of libraries and Node modules that make it easy to cache assets

[PWA Starter Kit](https://pwa-starter-kit.polymer-project.org/)

[PWA other templates](https://pwa-starter-kit.polymer-project.org/overview#other-templates)

[Books PWA](https://github.com/PolymerLabs/books)

[Shop PWA](https://github.com/Polymer/shop)

[Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/)

[Progressive Web App Checklist](https://developers.google.com/web/progressive-web-apps/checklist)

## Fetch & Promises

```js
fetch('/example/example.json')
  .then(function(response){
    return response.json();
})
.catch(function(error){
    console.log('fetch failed', error);
});
// or es2015 arrow function
fetch('/example/example.json')
  .then(response => {
    return response.json();
})
.catch(error => {
    console.log('fetch failed', error);
});
```

## Service Worker

* proxy between client and server and can cache info.
* can handle push notification
* promise function
* use https protect from man in the middle attack. free service like lets encrypt

* Service worker lifecycle
  * Registration
  * Installation
  * Activation

### Registration

Registration tells the browser where your service worker is located, and to start installing it in the background.

```js
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/service-worker.js')
  .then(function(registration) {
    console.log('Registration successful, scope is:', registration.scope);
  })
  .catch(function(error) {
    console.log('Service worker registration failed, error:', error);
  });
}
```

* The scope of the service worker determines which files the service worker controls, in other words, from which path the service worker will intercept requests. The default scope is the location of the service worker file, and extends to all directories below. You can also set an arbitrary scope by passing in an additional parameter when registering.


```js
navigator.serviceWorker.register('/service-worker.js', {
  scope: '/app/'
});
```

### Installation

This occurs if the service worker is considered to be new by the browser, either because the site currently doesn't have a registered service worker, or because there is a byte difference between the new service worker and the previously installed one.A service worker installation triggers an install event in the installing service worker.

```js
// Listen for install event, set callback
self.addEventListener('install', function(event) {
    // Perform some task
});
```

### Activation

Once a service worker has successfully installed, it transitions into the activation stage.

* If there are any open pages controlled by the previous service worker, the new service worker enters a waiting state. The new service worker only activates when there are no longer any pages loaded that are still using the old service worker.

```js
self.addEventListener('activate', function(event) {
  // Perform some task
});
```

## Fetch API

* replacement of XMLHttpRequest
* promise base
* implement CORS (Cross Origin Resource Sharing)
  * request must match page's schema, hostname and port except img, video/audio, embeded
  * fetch corse by default & if server does not support CORS `fetch('...',{mode:'no-corse'}` but javascript can't use content but can use in page and cach

```js
fetch('examples/example.json')
.then(function(response) {
  if (!response.ok) {
    throw Error(response.statusText);
  }
  // Read the response as json.
  return response.json();
})
.then(function(responseAsJson) {
  // Do stuff with the JSON
  console.log(responseAsJson);
})
.catch(function(error) {
  console.log('Looks like there was a problem: \n', error);
});
```

with `promise chaining`

```js
function logResult(result) {
  console.log(result);
}

function logError(error) {
  console.log('Looks like there was a problem: \n', error);
}

function validateResponse(response) {
  if (!response.ok) {
    throw Error(response.statusText);
  }
  return response;
}

function readResponseAsJSON(response) {
  return response.json();
}

function fetchJSON(pathToResource) {
  fetch(pathToResource) // 1
  .then(validateResponse) // 2
  .then(readResponseAsJSON) // 3
  .then(logResult) // 4
  .catch(logError);
}

fetchJSON('examples/example.json');
```

send

```js
var myHeaders = new Headers({
  'Content-Type': 'text/plain'
})
fetch('someurl/comment',{
  method: 'Post',
  body: 'title=hello&message=world',
  headers: myHeaders
})
```

```js
fetch(myRequest)
  .then(function(response) {
    var headers = response.headers;
    var contentType = headers.get('content-type');
    //........
})
```




















## Refrence

[Google Chrome Developer - Progressive Web App course](https://www.youtube.com/playlist?list=PLNYkxOF6rcIAdnzEsWkg0KpMn2WJwMBmN)
