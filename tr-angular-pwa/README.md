# TR Angular Progressive Web App (PWA)

This repository provides an example of converting an Angular application into a Progressive Web App (PWA) with service worker implementation and offline caching.

## Features

- Service worker implementation for offline caching
- Basic offline support for accessing cached resources
- Automatic caching of static files for offline usage

## Getting Started

### Prerequisites

- Node.js (version >= 10)
- Angular CLI (version >= 12)

### Installation

1. Clone the repository:

   ```shell
   git clone https://github.com/your-username/angular-pwa.git
    cd angular-pwa
    npm install

### Usage
1. Build the Angular app:
ng build --prod

2. Start the development server:
ng serve

The app will be accessible at http://localhost:4200

### Service Worker and Offline Caching
The service worker file (sw.js) is responsible for caching the static files of the Angular app. The following files are cached by default:

/
/index.html
/styles.css
/app.js
To add or modify the files to be cached, open sw.js and update the cache list accordingly.

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open('my-cache').then((cache) => {
      return cache.addAll([
        '/',
        '/index.html',
        '/styles.css',
        '/app.js',
        // Add any other static files or assets you want to cache
      ]);
    })
  );
});

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});

### Deploying the PWA
To deploy the PWA to a hosting server, follow these steps:

1. Build the Angular app:
ng build --prod

2. Deploy the compiled files (index.html, styles.css, app.js, etc.) to your hosting server.

3. Ensure the server is configured to support serving the PWA files with correct headers to enable service worker registration.

### Contributing
Contributions are welcome! If you find any issues or have suggestions for improvement, feel free to open a new issue or submit a pull request

### License
This project is licensed under the MIT License.