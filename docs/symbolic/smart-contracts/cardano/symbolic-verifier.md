# Smart Contracts with Symbolic Verifier

## Overview

![](zk-smart-contract-tx.png "A diagram illustrating the Symbolic Verifier script (Plutus)")

Cardano Type Library facilitates zero knowledge smart contracts on Cardano.

Cardano nodes are capable of executing code written in Untyped Plutus Core (UPLC), a low-level functional programming language. On the other hand, zero knowledge smart contracts can be represented by arithmetic circuits, a mathematical formalism that is used to describe true/false statements about some "public data". To verify a zero knowledge smart contract, we run the `verify` algorithm against the hash of transaction data, the commitment to a Plonk arithmetic circuit, and the corresponding zero knowledge proof. If the verification passes, the network participants can be sure that the transaction satisfies the respective zkFold Symbolic smart contract.

## Type Signature 

All zkFold Symbolic smart contracts are Haskell pure functions of transaction data and some auxiliary data. This auxiliary data usually consists of private information available to the parties involved in the transaction. It does not need to be posted on the blockchain.

```Haskell
smartContract :: Transaction a -> AuxiliaryData a -> Bool a
```

Type `Transaction` is a part of our Cardano Type Library. On the other hand, `AuxiliaryData` is a type defined by the smart contract developer.