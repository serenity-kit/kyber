# Kyber

## Goal

- Create a pure JavaScript (ideally TypeScript) implementation of the Kyber algorithm

## Why not use an existing implementation compiled to WebAssembly

WebAssembly is a viable option. That said there are several downsides and concerns:

- Often requires special setup with the bundler e.g. https://www.npmjs.com/package/vite-plugin-wasm or async loading like https://github.com/jedisct1/libsodium.js/
- ReactNative doesn't support WebAssembly

In practice a lot of developers just prefered the simplicity of a pure JS implementation. https://paulmillr.com/noble/ is a great example. Even the Frank Denis (libsodium creator) is advocating for it https://github.com/jedisct1/libsodium.js/issues/327#issuecomment-1793419292

### What about performance?

WebAssembly can be faster, but the factors in reality often outweight the lower performance.

## What is Kyber?

> Kyber is a key encapsulation mechanism (KEM) designed to be resistant to cryptanalytic attacks with future powerful quantum computers. It is used to establish a shared secret between two communicating parties without an (IND-CCA2) attacker in the transmission system being able to decrypt it. This asymmetric cryptosystem uses a variant of the learning with errors lattice problem as its basic trapdoor function. It won the NIST competition for the first post-quantum cryptography (PQ) standard. (Wikipedia)

### Resources

- https://pq-crystals.org/kyber/
- https://en.wikipedia.org/wiki/Kyber

## Variantes

## API Proposal
