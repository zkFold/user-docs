# Introduction

## What is a ZK Rollup?

A rollup is a layer 2 scaling solution that relies on a smart contract to manage the state of the rollup chain. The smart contract is responsible for verifying the correctness of the rollup chain state transitions. In ZK rollups, the smart contract uses a zero-knowledge proof protocol to verify the state transitions. The state update of the rollup is posted on the main chain as data. In the context of Cardano, the state update is attached to an unspent transaction output as datum.

Besides the state transition verification, the rollup smart contract is also responsible for briding assets between the main chain and the rollup chain. The smart contract can lock assets on the main chain and mint corresponding assets on the rollup chain, and vice versa. Those minted assets are called wrapped tokens. In order to unlock assets on one chain, the wrapped tokens must be burned on the other chain.

A rollup does not have its own _consensus mechanism_. Instead, it relies on the main chain for consensus. The main chain is responsible for finalizing the state updates of the rollup chain. Thus, the _finality_ of the rollup chain cannot be faster than the finality of the main chain. The latter also acts as a _data availability layer_ for the rollup chain.

## Symbolic Ledger

Symbolic Ledger is a mathematical model of a layer 2 ledger that possesses exceptional scaling capabilities. The model includes data types and validation rules for the ledger state, transactions, and blocks. Symbolic Ledger can be realized as a rollup or a sidechain.

It is implemented using the zkFold Symbolic framework. Any statement about the ledger can be naturally expressed as a Haskell (zkFold Symbolic) function and converted to an arithmetic circuit for use in a ZKP protocol.