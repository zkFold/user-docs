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
Smart Contract Wallet Backend provides two APIs: the standard CIP-30 Wallet API and the Symbolic Wallet API.

### CIP-30 Wallet API
The CIP-30 Wallet API is the standard wallet API that is implemented by most of the wallets in the Cardano ecosystem. The API is based on the Cardano Improvement Proposal 30 (CIP-30) and provides a set of functions for managing the wallet's UTxOs. The Smart Contract Wallet Backend implements the full CIP-30 Wallet API. Specifically, the API object provides the following methods:

- `getExtensions`: Get the list of the enabled API extensions.
- `getNetworkId`: Get the current network ID.
- `getUtxos`: Get the list of the wallet's UTxOs.
- `getCollateral`: Get the list of the wallet's collateral UTxOs.
- `getBalance`: Get the balance of the wallet.
- `getUsedAddresses`: Get the list of the wallet's used addresses.
- `getUnusedAddresses`: Get the list of the wallet's unused addresses.
- `getChangeAddress`: Get the wallet's change address.
- `getRewardAddresses`: Get the list of the wallet's reward addresses.
- `signTx`: Sign a transaction.
- `signData`: Sign data.
- `submitTx`: Submit a transaction to the blockchain.

To create an API object from the Wallet Backend object, use the `cip30` function.

You can find the full specification of the CIP-30 Wallet API [here](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0030).

### Symbolic Wallet API
The Symbolic Wallet API provides the additional functionality that is specific to the Smart Contract Wallet Backend. The API object provides the following methods:

- `signInstruction`: Sign a wallet instruction.
- `submitInstruction`: Submit a wallet instruction to the aggregation server.
- `signInstructionInput`: Sign a wallet instruction input.
- `submitInstructionInput`: Submit a wallet instruction input to the aggregation server.