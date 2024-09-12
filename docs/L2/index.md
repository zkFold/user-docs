# Layer 2 Solutions

## Symbolic Ledger
Symbolic Ledger is a mathematical model of a layer 2 ledger that possesses exceptional scaling capabilities. The model includes data types and validation rules for the ledger state, transactions, and blocks. Symbolic Ledger can be realized as a rollup or a sidechain.

It is implemented using the zkFold Symbolic framework. Any statement about the ledger can be naturally expressed as a Haskell (zkFold Symbolic) function and converted to an arithmetic circuit for use in a ZKP protocol.

## Rollup
A rollup is a layer 2 solution that uses the main chain as a data availability layer and does not have its own consensus mechanism. The rollup smart contract is responsible for verifying the correctness of the rollup chain state transitions. The state update of the rollup is posted on the main chain as data.

## Sidechain
A sidechain is a layer 2 solution that has its own consensus mechanism. The sidechain's network of nodes is responsible for finalizing its state transitions. The sidechain is connected to the main chain through a two-way bridge that allows assets to be transferred between the main chain and the sidechain.