# Getting Started

## Symbolic Fundamentals

zkFold Symbolic uses the Haskell type system to distinguish arithmetizable computations from non-arithmetizable ones. Every arithmetizable function must be polymorphic in the _context variable_ `c` satisfying the type constraint `Symbolic c`. This allows us to manipulate the function as a mathematical expression and compile it to an arithmetic circuit as well as evaluate it on concrete inputs.

A sufficient condition for a function to be arithmetizable is that all its arguments and the return value belong to the class `SymbolicData c`. Our Standard Library provides a collection of basic types with instances of `SymbolicData c`. Basic types are covered on [the next page](basic-types.md) of this documentation. Oftentimes, when building on top of those basic types, developers can derive instances of `SymbolicData c` for their custom types. We will discuss custom type implementation on the [Custom Types page](custom-types.md).

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