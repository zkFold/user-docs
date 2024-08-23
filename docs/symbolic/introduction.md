# Introduction

## What is zkFold Symbolic?

zkFold Symbolic is a programming framework. It is a subset of Haskell compilable to arithmetic circuits. Symbolic leverages the functional programming paradigm to provide a high-level language for the development of zero knowledge applications. It is designed to be a powerful tool for developers who want to build trustless, decentralized, and privacy-preserving applications and smart contracts.

The key design pillars of Symbolic are code efficiency and safety. It is high-level enough to abstract all mathematical nuances of zero knowledge protocols yet extremely efficient with the arithmetic circuits it produces.

Traditional performance metrics such as CPU cycles and RAM requirements do not make sense in the context of ZK-programs. Instead, the performance of a compiled circuit is usually measured in the number of additions and multiplications it contains. Symbolic translates the code directly into an arithmetic circuit, avoiding the limitations and inefficiencies of a typical Virtual Machine approach.

The idea of the zkFold Symbolic compiler is inspired by symbolic mathematics software packages, such as Wolfram Mathematica. The same abstract Haskell function can be interpreted in two different ways: as a mathematical expression that can be converted to an arithmetic circuit or as an algorithm that produces a concrete numerical output given a concrete input. This approach leads to a more natural and intuitive way of writing zero knowledge programs.

## Key Features

### High-level language with a performance of a low-level one
zkFold Symbolic compiler generally produces near-optimal arithmetic circuits from the high-level Haskell code. Developers are free to implement their custom optimizations and introduce new arithmetizable types using code snippets written in the lower-level eDSL.

### Correct-by-construction arithmetic circuits
Coding arithmetic circuits in a low-level language bears a significant probability of introducing errors that invalidate the security of the underlying business logic. This can be avoided by using zkFold Symbolic's standard type library as well as any custom types and functions defined on top of it. The developers can focus on the business logic of their application while the compiler takes care of the correctness of the arithmetic circuits.

Additionally, zkFold Symbolic provides built-in tests for any user-generated function. In particular, the tests verify that the function and its circuit representation implement the same map from the inputs to the output.

Finally, the zkFold Symbolic compiler is very compact, spanning just a few thousand lines of code, making it easy to audit.

### Low barrier to entry
In zkFold Symbolic, developers implement zero knowledge programs, i.e. statements to prove and verify, as pure, polymorphic Haskell functions. The complementing zero knowledge proof protocols are provided as easy-to-use APIs. Thus, in-depth knowledge of the underlying cryptography is not required.

### Support for the state-of-the-art ZKP protocols
zkFold Symbolic comes with several state-of-the-art zero knowledge proof protocols and circuit construction techniques that work out of the box. Our team is constantly upgrading the existing codebase and adding support for the novel cryptographic primitives as new research comes out.

## Use Cases

### Large-scale dApps
For decentralized applications with large transaction volumes, the cost of on-chain transactions can be a significant factor. Symbolic allows developers to create efficient zero knowledge smart contracts and effortlessly take advantage of various transaction batching techniques. This shortens the development cycle and leads to a significant cost reduction for the project and its users.

### Complex on-chain smart contracts
In zero knowledge proof protocols, zkSNARKS in particular, the cost of proof verification is independent (or depends sub-linearly) of the complexity of the statement being proven. This property makes zkSNARKS an ideal medium for implementing complex on-chain smart contracts as the computational burden is shifted from the on-chain verifier to the off-chain prover, i.e. the user or the application backend. In zkFold Symbolic, developers can implement arbitrary complex smart contract logic that can be verified on-chain for a fixed, predictable cost.

### Privacy-preserving applications
As the name suggests, zero knowledge proof protocols allow one party to prove to another that a statement is true without revealing any information beyond the validity of the statement. This property is particularly useful in privacy-preserving applications where the user should remain in control of their data. Symbolic provides a high-level language for designing secure data-sharing protocols that can be easily integrated into any application, be it a mobile app, a web service, or a blockchain-based solution.

### Verifier circuits in recursive proof protocols
Recursive proof protocols are particularly difficult to implement due to the need to generate a circuit from the proof verification algorithm. Symbolic simplifies this process as its standard library already contains very efficient in-circuit implementations for many data types and operations used in ZKP protocols. This library can be leveraged to implement custom recursive proof systems with minimal effort.
