# Star Wars Wiki

## About
Single-page Star Wars Wiki application built with Vue.js to view people in the Star-Wars Universe and their information. API from https://swapi.co/ is used.

## Features
- Lazy loading of some fields in profile that require API calls to reduce initial home page loading time
- Employs caching to minimise API calls for profiles that have previously been loaded (Once a profile's data is fetched, it will be stored so the next the next time profile is clicked on, there is no loading)
- Profile page loads only after all API calls for that profile have been made and information has been retrieved (Semaphore-like variables to ensure all API calls are finished)

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
