---
title: "Introduction"
description: "Introduction to zk rollup and symbolic ledger."
author: "zkFold"
date: "2024-11"
PUBLIC: true
---

# Introduction


## What is a ZK rollup?

A rollup is a blockchain scaling solution where a smart contract (on the underlying blockchain) validates state transitions on a separate ledger (the rollup ledger). In this _Layer 2_ solution, transactions settle upon a transition of the Layer 1 smart contract to a new state. Smart contract state transitions correspond to the application of _transaction batches_. As a part of the validation logic, the smart contract verifies the correctness of all transactions in a batch. In ZK rollups, the smart contract uses a zero-knowledge proof protocol to verify the state transitions. The states (or state diffs) of the rollup are posted on-chain as data.

Besides the state transition verification, the rollup smart contract is also responsible for briding assets between the L1 chain and the rollup chain. The smart contract can lock assets on the main chain and mint corresponding assets on the rollup chain, and vice versa. Those minted assets are called wrapped tokens. In order to unlock assets on one chain, the wrapped tokens must be burned on the other chain.

A rollup does not have its own _consensus mechanism_. Instead, it relies on the main chain for consensus. The main chain is responsible for finalizing the state updates of the rollup chain. Thus, the _finality_ of the rollup chain cannot be faster than the finality of the main chain.


## Symbolic Ledger

Symbolic Ledger is a UTXO-based ledger model created by zkFold that is designed to be efficient for use in zero-knowledge proving protocols. In addition, the ledger rules and on-chain data representation is architectured in a way to minimize communication with the L1 blockchain network, providing exceptional scaling capabilities. The model is generic and can be applied to different blockchains. The key assumptions are that the underlying blockchain can verify zero-knowledge proofs and that the (rollup) data can be posted efficiently on-chain.

This ledger model is implemented using the Symbolic framework also developed by zkFold. Any statement about the ledger can be naturally expressed in this framework and automatically converted to an arithmetic circuit for use in zero knowledge proof protocols.
