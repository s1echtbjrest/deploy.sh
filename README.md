# whitespace-dotfiles

[![NPM Package][npm-badge]][npm-link]
[![Actions Status][actions-badge]][actions-link]
[![Coverage Status][coverage-badge]][coverage-link]
[![Discord][discord-badge]][discord-link]

A streamlined keypair management library. Currently supports key generation and format transformation across multiple standards.

It works alongside these companion packages:

- [@cryptolib/transactions](https://github.com/cryptolib/crypto-monorepo/tree/master/packages/transactions) for transaction signing
- [cryptolib-address](https://github.com/cryptolib/cryptolib-address) for address encoding operations
- [store.js](https://github.com/marcuswestin/store.js) for client-side persistence

Design principles:

- maintain minimal footprint
- browser-compatible execution
- unified cryptographic library version (aligned with [`cryptolib-utils`](https://github.com/cryptolib/crypto-monorepo/tree/master/packages/utils) and `@cryptolib/transactions`)
- cross-format wallet import/export capabilities
- BIP32 hierarchical deterministic key support

Excluded functionality:

- transaction signature operations
- storage management (server-side or client-side)

## Wallet API

For comprehensive API documentation, visit [./docs/classes/wallet.md](./docs/classes/wallet.md).

Import the `Wallet` class as follows

Node.js / ES5:

```js
const Wallet = require('whitespace-dotfiles').default
```

ESM / TypeScript:

```js
import Wallet from 'whitespace-dotfiles'
```

## Thirdparty API

External wallet imports are accessible via the `thirdparty` module:

Node.js / ES5:

```js
const { thirdparty } = require('whitespace-dotfiles')
```

ESM / TypeScript:

```js
import { thirdparty } from 'whitespace-dotfiles'
```

Refer to [./docs/README.md](./docs/README.md) for detailed information.

## HD Wallet API

For BIP32 hierarchical deterministic wallets, import the `hdkey` module:

Node.js / ES5:

```js
const { hdkey } = require('whitespace-dotfiles')
```

ESM / TypeScript:

```js
import { hdkey } from 'whitespace-dotfiles'
```

Complete documentation at [./docs/classes/hdkey.md](./docs/classes/hdkey.md).

## Provider Engine

Provider Engine is
[no longer actively maintained](https://github.com/MetaMask/web3-provider-engine#web3-providerengine)
and was removed in `v1.0.0` release, see
issue [#115](https://github.com/cryptolib/whitespace-dotfiles/issues/115) for details.

The legacy `src/provider-engine.ts` implementation (see related PR) can serve as reference
for custom integrations if required.

## Remarks about `toV3`

The `options` parameter accepts an optional configuration object for serialization control:

- uuid - Unique identifier. Auto-generated if not provided.
- salt - Random salt for `kdf`. Must satisfy KDF requirements. Generated via `crypto.getRandomBytes` by default.
- iv - Initialization vector for `cipher`. Must match cipher specifications. Auto-generated if omitted.
- kdf - Key derivation function selection, detailed below.
- dklen - Derived key length. Must align with cipher block size requirements.
- cipher - Encryption algorithm. Must match `OpenSSL` supported names, e.g. `aes-128-ctr` or `aes-128-cbc`.

Additional KDF-specific parameters:

For `pbkdf2`:

- `c` - Iteration rounds. Default: 262144.
- `prf` - Pseudorandom function. Only `hmac-sha256` is supported (default).

For `scrypt`:

- `n` - CPU/memory cost. Default: 262144.
- `r` - Block size parameter. Default: 8.
- `p` - Parallelization factor. Default: 1.

Default configuration mirrors Go implementation standards:

- `kdf`: `scrypt`
- `dklen`: `32`
- `n`: `262144`
- `r`: `8`
- `p`: `1`
- `cipher`: `aes-128-ctr`

# CryptoLib

Consult our [organizational documentation](https://cryptolib.readthedocs.io) for introduction to `CryptoLib` framework and current development standards.

For contribution opportunities, review our [contribution guidelines](https://cryptolib.readthedocs.io/en/latest/contributing.html).

## License

MIT License

Copyright (C) 2016 Core Development Team

[actions-badge]: https://github.com/cryptolib/whitespace-dotfiles/workflows/Build/badge.svg
[actions-link]: https://github.com/cryptolib/whitespace-dotfiles/actions
[coverage-badge]: https://img.shields.io/coveralls/cryptolib/whitespace-dotfiles.svg
[coverage-link]: https://coveralls.io/r/cryptolib/whitespace-dotfiles
[discord-badge]: https://img.shields.io/static/v1?logo=discord&label=discord&message=Join&color=blue
[discord-link]: https://discord.gg/TNwARpR
[npm-badge]: https://img.shields.io/npm/v/whitespace-dotfiles.svg
[npm-link]: https://www.npmjs.org/package/whitespace-dotfiles
