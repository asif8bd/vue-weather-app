# vue-weather-app

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

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

##  Deploy the Vue js web-pack application in Tomcat 

### Add the below configuration to the vue.config.js
```
publicPath: process.env.NODE_ENV === 'production'
module.exports = {
 publicPath: process.env.NODE_ENV === 'production'? '/weather/': '/'
}
```
### Now let us create a production build with below command.
```
npm run-script build
```
