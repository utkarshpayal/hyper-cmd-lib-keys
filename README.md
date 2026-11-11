# hyper-cmd-lib-keys

Small Node.js helper library ("HyperCmd Keys lib") for handling keys and key pairs as hex-encoded `Buffer`s. It is used by the HyperCmd tooling.

This repository is a fork of [holepunchto/hyper-cmd-lib-keys](https://github.com/holepunchto/hyper-cmd-lib-keys).

## Features / API

`index.js` exports the following functions:

| Function | Description |
| --- | --- |
| `parseKeyPair(json)` | Parses a JSON string of the form `{"publicKey": "<hex>", "secretKey": "<hex>"}` and returns `{ publicKey, secretKey }` as `Buffer`s. |
| `randomBytes(n)` | Returns a `Buffer` of `n` cryptographically random bytes (via `sodium.randombytes_buf`). |
| `prepKey(hex)` | Converts a hex string into a `Buffer`. |
| `prepKeyList(hexList)` | Converts an array of hex strings into an array of `Buffer`s. |
| `checkAllowList(allowList, key)` | Returns `true` if `key` (a `Buffer`) is present in `allowList` (an array of `Buffer`s), using `Buffer#equals`. |

## Tech stack

- Node.js (CommonJS)
- [`sodium-universal`](https://www.npmjs.com/package/sodium-universal) for random byte generation

## Installation

```sh
git clone https://github.com/utkarshpayal/hyper-cmd-lib-keys.git
cd hyper-cmd-lib-keys
npm install sodium-universal
```

Note: `index.js` requires `sodium-universal`, but it is not listed under `dependencies` in `package.json`, so it has to be installed explicitly.

## Usage

```js
const keys = require('./index.js') // or require('hyper-cmd-lib-keys') when installed as a package

const kp = keys.parseKeyPair('{"publicKey":"aabb","secretKey":"ccdd"}')
// kp.publicKey -> <Buffer aa bb>, kp.secretKey -> <Buffer cc dd>

const allow = keys.prepKeyList(['aabb', '0011'])
keys.checkAllowList(allow, keys.prepKey('aabb')) // true

const seed = keys.randomBytes(32) // 32 random bytes
```

## Tests / build

There is no build step and no test suite in this repository.

## License

MIT, as declared in `package.json` (no separate `LICENSE` file is included).
