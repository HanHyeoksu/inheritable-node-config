# Configure your Node.js Applications
[![NPM](https://nodei.co/npm/inheritable-config.png)](https://nodei.co/npm/inheritable-config/)

## Introduction
`inheritable-node-config` is forked and extended version of [Lorentwest's node-config](https://github.com/lorenwest/node-config). It provides inheritance function between config files by naming the config file name like `docker:development.js`. Is also allows multi extends by naming it as `docker:development,docker-base.js`.

## Inheitance example
`docker:developmet,docker-base.js` inherits `development.js` and `docker-base.js`. In this case `development.js` is overwritten by `docker-base` because `docker-base` is right side of `development`.

**NODE_ENV**: `docker:development,docker-base`

`./config/default.js`
```js
module.exports = {
  mongodb: {
    port: 27017 
  }
};
```

`./config/development.js`
```js
module.exports = {
  redis: {
    host: 'localhost',
    port: 2000
  },
  mongodb: {
    host: 'localhost'
  }
};
```

`./config/docker-base.js`
```js
module.exports = {
  redis: {
    host: 'redis'
  },
  mongodb: {
    host: 'mongo'
  }
};
```

`./config/docker:development,docker-base.js`
```js
module.exports = {
  label: 'docker:dev'
};
```

`index.js`
```js
var config = require('inheritable-config');

console.log(config);
/*
{
  label: 'docker:dev',
  redis: {
    host: 'redis',
    port: 2000
  },
  mongodb: {
    host: 'mongo',
    port: 27017
  }
}
*/
```

## License
May be freely distributed under the [MIT license](https://raw.githubusercontent.com/lorenwest/node-config/master/LICENSE).

Copyright (c) 2018 hshan, Loren West 
[and other contributors](https://github.com/lorenwest/node-config/graphs/contributors)