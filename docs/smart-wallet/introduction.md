---
title: "Smart Wallet"
description: "An introduction to the Smart Contract Wallet Backend."
author: "vlasin"
date: "2025-03"
PUBLIC: true
---

# Smart Wallet

## Overview

The Smart Contract Wallet Backend (_Smart Wallet_ for short) is a blockchain-agnostic programmable crypto wallet with an extensible feature set packed in a TypeScript library. The library provides a set of APIs to be used by wallet apps.

The key features of the Smart Wallet are:

- Web2 Login
- Babel Fees
- Sponsored Transactions
- Batch Transactions

<!-- ## Wallet Instructions
The smart contract wallet's extensible functionality is based on the idea of _wallet instructions_. A wallet instruction is a piece of code in the form of an arithmetic circuit that can be signed by the wallet owner. More specifically, a wallet instruction must be of the format that is used in the Symbolic Verifier. To spend a wallet UTxO, a Symbolic Verifier proof for _some_ wallet instruction must be verified on-chain.

Wallet instructions enables programming spending logic for the wallet UTxOs "on-the-fly". For example, an atomic swap between two users can be performed in an asyncronous way and without any on-chain setup: both users can sign a _swap_ wallet instruction and send it to the order aggregator. Once the aggregator identifies a pair of instructions that can be matched against each other, it can submit the atomic swap transaction to the blockchain. -->

## Features

### Web2 Login
The Smart Contract Wallet Backend enables spending of the wallet's UTxOs using Web2 authentification tokens. This feature enables cryptocurrency wallets without a seed phrase which simplify the user experience for new Web3 users.

First, the wallet backend creates an address that is associated with the user's Web2 account. Then, the user can spend funds from that address by logging in with their Web2 account and proving that they know an active Web2 token that is associated with the account.

### Babel Fees
Babel fees are a way to pay for the transaction fees in a different token than the native token of the blockchain.

The aggregation server can accept transaction requests where fees are paid in different tokens. The server can then match it with the known set of Babel fees instructions. This adds extra inputs and outputs to the transaction to balance it out so that the resulting fee is paid in ada

### Sponsored Transactions
Sponsored transactions are a way for a third party to pay for the transaction fees of a user. The third party can be, for example, a wallet provider, a dApp, or a recipient of a payment.

By submitting instructions to the aggregation server, the third party can sponsor the transaction fees of the user from their own funds. It is possible to set up various conditions for the sponsorship, such as the maximum amount of sponsored fees per transaction, the maximum number of transactions per day, etc.

### Batch Transactions
Users of wallets based on the Smart Contract Wallet Backend can create multi-user transactions in a convenient asynchronous way where every user can sign their part of the transaction independently.

The aggregation server can collect the signed parts of the transaction from the users and submit the full transaction to the blockchain once all parts are collected. This feature is useful for atomic swaps, escrow transactions, and other multi-user transactions. It also helps in reducing the transaction fees for the users.

<!-- ## APIs
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
The Symbolic Wallet API provides the additional functionality that is specific to the Smart Contract Wallet Backend. Below we give the reference implementation of the Symbolic Wallet API in Haskell.

The following data types are used in the Symbolic Wallet API:

- `Wallet`: A wallet object.
- `Address`: A wallet address.
- `Instruction`: A wallet instruction. It is a piece of code that describes the spending logic for the wallet UTxOs.
- `InstructionId`: An instruction identifier that is derived from the instruction object by hashing.
- `InstructionInput`: An input for a wallet instruction. It is a piece of data that is required to verify the instruction.

The following methods are available as a part of Symbolic Wallet API:

```Haskell title="Haskell"
signInstruction :: Wallet -> Instruction -> IO Signature
```

Sign a wallet instruction.

```Haskell title="Haskell"
submitInstruction :: Address -> Instruction -> Signature -> IO ()
```

Submit a wallet instruction to the aggregation server.

```Haskell title="Haskell"
submitInstructionInput :: Address -> InstructionId
    -> InstructionInput -> IO ()
```

Submit a wallet instruction input to the aggregation server. -->