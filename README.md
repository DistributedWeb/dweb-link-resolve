# dweb-link-resolve

resolve urls, links to a dweb key using common methods

[![npm][npm-image]][npm-url]
[![travis][travis-image]][travis-url]
[![standard][standard-image]][standard-url]

### Supports

* Common dweb key representations (`dweb://`, etc.)
* URLs with keys in them (`dwebx.org/6161616161616161616161616161616161616161616161616161616161616161`)
* `dwebfs-key` or `dweb-key` headers
* Url to JSON http request that returns `{key: <dweb-key>}`
* DWeb-DNS resolution (via [dweb-dns](https://github.com/datprotocol/dweb-dns))

## Install

```
npm install dweb-link-resolve
```

## Usage

```js
var datResolve = require('dweb-link-resolve')

datResolve(link, function (err, key) {
  console.log('found key', key)
})
```

## API

### `datResolve(link, callback(err, key))`

Link can be string or buffer.

Resolution order:

1. Validate buffers or any strings with 64 character hashes in them via [dweb-encoding](https://github.com/juliangruber/dweb-encoding)
2. Check headers in http request
3. Check JSON request response for `key`
4. DWeb-DNS resolution via [dweb-dns](https://github.com/datprotocol/dweb-dns)

## Refering to dwebs
Trying to tighten up a bit dweb-link-resolve (and its dependencies dweb-dns and dweb-decode). I am noticing a few inconsistencies as I'm writing dweb-shell.

Ideally, I'd like to launch dweb-shell like this:
```sh
$ dweb-shell dweb://40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9+5/path4
```

and have it open the dweb at version 5 and change directory to /path4.

Currently ```dweb-shell google-fonts-kewitz.hashbase.io/fonts/``` [fails somewhere in dweb-link-resolve](https://github.com/millette/dweb-shell/issues/5).

### Examples
Note that dweb-link-resolve also supports other methods, such as detection of dweb keys in paths and http headers.

#### Simplest
* Plain: 40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9
* DNS: dbrowser.com

#### With version
* Plain: 40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9+5
* DNS: dbrowser.com+5

#### With scheme
* https: https://40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9/
* dweb: dweb://dbrowser.com

#### With path
* https: 40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9/path1
* dweb: dbrowser.com/path2

#### Combinations
* 40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9+5/path3
* dweb://40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9+5/path4
* https://40a7f6b6147ae695bcbcff432f684c7bb5291ea339c28c1755896cdeb80bd2f9/path5 [(^1)][]
* https://dbrowser.com+5/path6 [(^2)][]

### Notes
1. browsers expect http and https schemes with traditional hostname, not a dweb key
2. browsers expect http and https schemes with traditional hostname, no +5 (version) support

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first.

## License

[MIT](LICENSE.md)

[npm-image]: https://img.shields.io/npm/v/dweb-link-resolve.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/dweb-link-resolve
[travis-image]: https://img.shields.io/travis/joehand/dweb-link-resolve.svg?style=flat-square
[travis-url]: https://travis-ci.org/joehand/dweb-link-resolve
[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square
[standard-url]: http://npm.im/standard
[(^1)]: <#notes>
[(^2)]: <#notes>
