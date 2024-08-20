# Getting Started

ZKFold Symbolic uses the Haskell type system to distinguish arithmetizable computations from non-arithmetizable ones.

A pure function `f` of any arity can be compiled into an arithmetic circuit provided that:

- Every argument and the return value of f belongs to the class `Arithmetizable a`.

- Type `a` belongs to the class `Symbolic`.

The Standard Library, as well as the Cardano Type Library, contains a collection of types that cover the basic use-cases. In the next section, we discuss how to define your own `Arithmetizable a` types.

## Framework Overview

### zkFold Symbolic Base
#### Haskell tools
Use the full power of GHC and the Haskell toolstack when developing your zk-enhanced applications.

### zkFold Symbolic Standard Library and Compiler
Build zk-apps using our standard library and compile the code to arithmetic circuits.

#### ZKP protocols
The circuits produced by the zkFold Symbolic compiler can be immediately used in zero knowledge protocols. Prove and verify statements encoded by the circuits with the help of our easy-to-use APIs.

### For Cardano DApps
#### Cardano Type Library
Pre-defined collection of types for building zero knowledge smart contracts for the Cardano blockchain.

#### Transaction Builder APIs
Construct zero knowledge smart contract transactions using our set of transaction builder APIs.

### For Privacy-Preserving Applications
#### Data-sharing DSL
- Define your data structures

- Prove and verify the knowledge of a signed data structure matching some pattern

- Prove and verify the presence of data matching your patterns in a collection of records