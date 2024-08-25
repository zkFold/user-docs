# Smart Contract Wallet Backend

## Overview

The Smart Contract Wallet Backend is an implementation of a programmable wallet with an extensible API and feature set that uses zkFold Symbolic framework. It includes all necessary components for a wallet application except the graphical user interface. The wallet backend is packaged as a WASM module that can be integrated into any browser-based wallet application.

## Wallet Instructions
The smart contract wallet's extensible functionality is based on the idea of _wallet instructions_. A wallet instruction is a piece of code in the form of a Plonk circuit that can be signed by the wallet owner. More specifically, a wallet instruction must be of the format that is used in the Symbolic Verifier. To spend a wallet UTxO, a Symbolic Verifier proof for _some_ wallet instruction must be verified on-chain.

Wallet instructions enables programming spending logic for the wallet UTxOs "on-the-fly". For example, an atomic swap between two users can be performed in an asyncronous way and without any on-chain setup: both users can sign a _swap_ wallet instruction and send it to the order aggregator. Once the aggregator identifies a pair of instructions that can be matched against each other, it can submit the atomic swap transaction to the blockchain.

## Features

### Web2 Login
The smart contract wallet backend enables spending of the wallet's UTxOs using Web2 authentification tokens. This feature enables seedless cryptocurrency wallets that simplifies the user experience for new Web3 users.

### Babel Fees
Babel fees are a way to pay for the transaction fees in a different token than the native token of the blockchain.

### Sponsored Transactions
Sponsored transactions are a way for a third party to pay for the transaction fees of a user. The third party can be, for example, a wallet provider, a dApp, or a recipient of a payment.

### Multi-User Transactions
Users of wallets based on the smart contract wallet backend can create multi-user transactions in a convenient asynchronous way where every user can sign their part of the transaction independently.

## APIs

### CIP-30 Wallet API

### Symbolic Wallet API