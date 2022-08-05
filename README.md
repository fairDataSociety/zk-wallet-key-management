# zk-wallet-key-management
ZK-Snarks based Wallet Key Management using smart contracts for seed phrase controller, a zk trusted setup on the client side and certificate transparency logs to keep track of revoked keys (experimental)


## Abstract

This experiments is an approach to seed phrase and private key less key management, which we call `radioactive toxic waste`, which should be avoided at all cost being treated by humans.

How we are accomplishing this feature?

### A seed phrase key manager or controller

A smart contract (no need to be one per user) that handles seed phrase identification through ZK-snarks proofs, must be able to:

- Associate a seed phrase to Swarm Bee store FDP seed phrase
- Keep track of key derivation using fingerprinting
- Be able to recover keys by registered WebAuthentication keys, backup codes or Google Drive exporte keystores

### A Go base `gnark` zk trusted setup

Where it will create zk-snarks proofs and then update the smart contract with private keys sequences. Seed phrase is downloaded into client (same as FDP) and key is generated inside a TPM Secure Enclave. A production implementation must be contained in mobile which have SDKs available for TPMs.

### Recovery 

- WebAuthentication (recommended approach)
- Backup codes
- Google Drive

### Certificate Transparency support

Public keys which are rotated, must be registered as revoked in a offchain Certificate Transparenct database, but with the additional zk-snarks proof as index to search for seed phrase merkle tree of private keys (HD Wallet keys). These logs must not contain any machine or hardware tags or identifier.

### API and documentation plus a sample Dapp

### Collaborators

- Luis Sanchez (Bee team)
- Rogelio Morrell (FDP team)
