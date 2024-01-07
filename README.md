# Kyber

## Goals

- Create a pure TypeScript implementation of the Kyber algorithm with a great API (ESM & CommonJS)
- Create a proper test suite (check what others do)
- Measure and compare performance to other implementations (WebAssembly)
- Apply to https://www.opentech.fund/ or similar for an in-depth cryptography audit

## Why not use an existing implementation compiled to WebAssembly

WebAssembly is a viable option. That said there are several downsides and concerns:

- Often requires special setup with the bundler e.g. https://www.npmjs.com/package/vite-plugin-wasm or async loading like https://github.com/jedisct1/libsodium.js/
- ReactNative doesn't support WebAssembly

In practice a lot of developers just prefered the simplicity of a pure JS implementation. https://paulmillr.com/noble/ is a great example. Even the Frank Denis (libsodium creator) is advocating for it https://github.com/jedisct1/libsodium.js/issues/327#issuecomment-1793419292

### What about performance?

WebAssembly can be faster, but the factors in reality often outweight the lower performance.

## What is Kyber?

> Kyber is a key encapsulation mechanism (KEM) designed to be resistant to cryptanalytic attacks with future powerful quantum computers. It is used to establish a shared secret between two communicating parties without an (IND-CCA2) attacker in the transmission system being able to decrypt it. This asymmetric cryptosystem uses a variant of the learning with errors lattice problem as its basic trapdoor function. It won the NIST competition for the first post-quantum cryptography (PQ) standard. (Wikipedia)

What does it mean? It allows to create a shared secret between two parties which allows to replace the not post-quantum save public-private crytography use-cases.

This summer NIST started to [standardize Kyber](https://www.nist.gov/news-events/news/2023/08/nist-standardize-encryption-algorithms-can-resist-attack-quantum-computers) like they did in the past for AES. I expect Kyber to be used in lots of protocols in the coming decade. Signal uses it already for conversations and you can use it in TLS e.g. https://aws.amazon.com/blogs/security/how-to-tune-tls-for-hybrid-post-quantum-cryptography-with-kyber/

### Resources

- https://pq-crystals.org/kyber/
- https://en.wikipedia.org/wiki/Kyber

## Existing implementations

- https://github.com/pq-crystals/kyber/ reference implementation in C by the designers
- https://github.com/Argyle-Software/kyber - rust implemenation
  - https://www.npmjs.com/package/pqc-kyber - wasm bindings
- https://github.com/symbolicsoft/kyber-k2so
  - https://symbolic.software/blog/2023-12-19-kyberk2sovariabletiming/ an issue in multiple implementations was found and fixed
- https://github.com/antontutoveanu/crystals-kyber-javascript - JS implementation - maybe out of date? missing fixes for issues? API design?
- https://github.com/fisherstevenk/crystals-kyber-ts/ - TS implementation - maybe fine? maybe missing fixes for issues? API design?

## API Proposal

Key Encapsulation

```ts
import { generateKeyPair, encapsulate, decapsulate } from '@serenity-kit/kyber-768';

const keyPairBob = generateKeyPair();

const { ciphertext, sharedSecret } = encapsulate(keyPairBob.publicKey);
const sharedSecret2 = decapsulate(keyPairBob.privateKey, ciphertext);
// sharedSecret === sharedSecret2
```

Other packages:

- `@serenity-kit/kyber-512`
- `@serenity-kit/kyber-1024`
