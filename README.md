# axios-elasticache-memcached-adapter

Cache adapter for axios using memcached elasticache

This library was built on top of [memcached-elasticache](https://github.com/jkehres/memcached-elasticache) to support http requests caching using [AWS ElastiCache](https://aws.amazon.com/es/elasticache/)

[![David](https://img.shields.io/david/jefer590/axios-elasticache-memcached-adapter.svg)](https://www.npmjs.com/package/axios-elasticache-memcached-adapter)
[![npm](https://img.shields.io/npm/v/axios-elasticache-memcached-adapter.svg)](https://www.npmjs.com/package/axios-elasticache-memcached-adapter)
[![node](https://img.shields.io/node/v/axios-elasticache-memcached-adapter.svg)](https://www.npmjs.com/package/axios-elasticache-memcached-adapter)
[![npm](https://img.shields.io/npm/dt/axios-elasticache-memcached-adapter.svg)](https://www.npmjs.com/package/axios-elasticache-memcached-adapter)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com)

## Disclaimer

This library was built only for server side usage.

## Install

``` shell
npm install --save axios-elasticache-memcached-adapter
```

## Setting up the client

The library setup takes four parameters

- `serverLocations`: Server Location of memcached cluster. Check [Server Locations documentation](https://github.com/3rd-Eden/memcached#server-locations) from the memcached library.
- `ttl`: Cache Time-to-Live in seconds. Default value is 100 seconds.
- `salt`: Salt Suffix for the memcached key. Default is empty string `''`
- `options`: Options object with the memcached client params. Check the [client options documentation](https://github.com/3rd-Eden/memcached#options) from the memcached library.

## Usage

To use this library, you need to setup the memcached options to create the adapter function and then attach it to the axios instance.

```javascript
const axios = require('axios')
const axiosCacheMemcached = require('axios-elasticache-memcached-adapter')

const memcachedAdapter = axiosCacheMemcached.setup('localhost:11211')

const http = axios.create({
  adapter: memcahachedAdapter
})

http.get(url, options).then(response => {
  // Cached or Uncached axios response
})
```

or

```javascript
const axios = require('axios')
const axiosCacheMemcached = require('axios-elasticache-memcached-adapter')

const memcachedAdapter = axiosCacheMemcached.setup('mycfgmemcached.endpoint.elasticache.aws.amazon.com', 600, 'mysalt2.com', { maxValue: 1024 * 1024 * 5 })

axios.get(url, {
  params: theparams,
  adapter: memcachedAdapter
})
```

## License

This project is released under the MIT license. See the [LICENSE](LICENSE) for more information.
