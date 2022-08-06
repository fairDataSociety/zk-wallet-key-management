# zk-wallet-key-management
ZK-Snarks based Wallet Key Management using smart contracts for seed phrase controller, a zk trusted setup on the client side and certificate transparency logs to keep track of revoked keys (experimental)


## Abstract

This project is an approach to seed phrase and private key less key management, which we call `radioactive toxic waste`, which should be avoided at all cost being treated by humans.

## Features at a glance

- ENS -`PublicResolver` (exists in `fdp-contracts`)
- Wasm secure execution context - `KeychainOpsManager`
- ZK-snarks trusted setup  - `KeySequencer`
- Ethereum Smart Contracts - `KeyController`
- Certificate Transparency for blockchain wallets

### Wasm for secure execution

- Keypair operations are executed with security policies using WasmEdge

### *NS supported by default

- First release will use ENS to connect addresses to keys, the spec will allowed for other chains nameservices.

### A seed phrase key manager or controller

A smart contract (no need to be one per user) that handles seed phrase identification through ZK-snarks proofs, must be able to:

- Associate a seed phrase to Swarm Bee store FDP encrypted seed phrase
- Keep track of key derivation using fingerprinting
- Be able to recover keys by registered WebAuthentication keys, backup codes or Google Drive exported keystores

### A Go based tooling by using `gnark` for zk trusted setup

Where it will create zk-snarks proofs and then update the smart contract with private keys sequences. Seed phrase is downloaded into client (same as FDP) and key is generated inside `WasmEdge`

### Recovery 

- WebAuthentication (recommended approach)
- Backup codes
- Google Drive

### Certificate Transparency support

Keys are rotated bty design, so public keys must be registered as revoked in a offchain Certificate Transparency database, but with the additional zk-snarks proof as index to search for seed phrase merkle tree of private keys (HD Wallet keys). These logs must not contain any machine or hardware tags or identifier.

### API and documentation plus a sample Dapp

### Collaborators

- Luis Sanchez (Bee team)
- Rogelio Morrell (FDP team)

MIT Licensed
