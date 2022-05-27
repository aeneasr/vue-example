# ory-vue-example

1. npx @vue/cli create ory-example
2. Vue 3.0
3. npm i
4. npm run serve
5. npx @ory/cli tunnel http://localhost:8080 --dev --project playground
6. npm i @ory/client
   import {V0alpha2Api, Configuration} from '@ory/client'

const ory = new V0alpha2Api(new Configuration({
basePath: 'http://localhost:4000',
baseOptions: {
withCredentials: true
}
}))



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
