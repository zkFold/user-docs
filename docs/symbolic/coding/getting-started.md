---
title: "Getting Started"
description: "Getting started."
author: "zkFold"
date: "2024-11"
PUBLIC: true
---

# Getting Started

## Symbolic Fundamentals

zkFold Symbolic doesn't rely on any GHC compiler magic or compiler plugins:
Symbolic code is usual Haskell code, compiled by usual GHC 9.6.0 compiler.
We only use the Haskell type system in a smart way to distinguish arithmetizable
computations from non-arithmetizable ones. While this is great, this also means
that at least basic knowledge of Haskell language is required; we advise to at
least get comfortable with the syntax first.

Now, back to Symbolic. It is distinguished from simple Haskell by presence of
the _context type variable_ `c` satisfying the type constraint `Symbolic c`
which is later used in Symbolic data types. For example, here is the Symbolic
function which, given a native field element and a `ByteString` of length 256,
computes MiMC hash on the contents of a bytestring and compares it with the
expected result:

```haskell
{-# LANGUAGE DataKinds         #-}
{-# LANGUAGE NoImplicitPrelude #-}

import ZkFold.Symbolic.Algorithms.Hash.MiMC (hash)
import ZkFold.Symbolic.Class                (Symbolic)
import ZkFold.Symbolic.Data.Bool            (Bool)
import ZkFold.Symbolic.Data.ByteString      (ByteString)
import ZkFold.Symbolic.Data.Eq              ((==))
import ZkFold.Symbolic.Data.FieldElement    (FieldElement)

checkHash :: Symbolic c => FieldElement c -> ByteString 256 c -> Bool c
checkHash expected byteString = hash byteString == expected
```

!!! coming-soon "Coming soon"

    If you too are worried by the amount of the `import` stanzas, you are not
    alone. Soon we will define the `ZkFold.Symbolic.Prelude` module which would
    reexport the most useful definitions of Symbolic Standard Library.

The main benefit of making all functions polymorphic in `c` is that it allows us
to reinterpret them in a plethora of different ways, most notably both as a
blueprint for an arithmetic circuit used in a zkSNARK and as a pure function to
be evaluated on concrete inputs.

While there is no restriction on which functions can be written and reused in
other functions (as zkFold Symbolic code is just Haskell code), for a function
to be __compilable into a circuit__, certain conditions have to be satisfied:

1. All of its arguments are an instance of `SymbolicInput`;
2. Its return type is `SymbolicData`.

`checkHash` satisfies these constraints, so we can compile it with, you guessed
it, `compile` function and print the compiled circuit:

```haskell
import ZkFold.Symbolic.Compiler (compile)
import MyExample                (checkHash)

printCheckHashAC :: IO ()
printCheckHashAC = print (compile checkHash)
```

Our Standard Library provides a collection of basic types with instances of
both `SymbolicInput` and `SymbolicData`. Basic types are covered on
[the next page](basic-types.md) of this documentation. When building on top of
those basic types, developers can write down their own instances of
`SymbolicInput` and `SymbolicData` for their custom types. We will discuss
custom type implementation on the [Custom Types page](custom-types.md).

## Tips and tricks

### Higher-order functions

Being usual Haskell code, zkFold Symbolic admits usual Haskell idioms, including
polymorphism, monads, higher-order functions and whatnot. For example, we could
rewrite our `checkHash` function in the following way:

```haskell
import ZkFold.Symbolic.Algorithms.Hash.MiMC qualified as MiMC

checkWith ::
    Symbolic c =>
    FieldElement c -> (ByteString c -> FieldElement c) -> ByteString c -> Bool c
checkWith expected hash byteString = hash byteString == expected

checkHash :: Symbolic c => FieldElement c -> ByteString c -> Bool c
checkHash expected = checkWith expected MiMC.hash
```

And this would still compile just fine &mdash; and to the same circuit as
before, even &mdash; nevermind the higher-order functions and eta-reduction.
Once again: anything goes as long as the function which ends up being compiled
satisfies the constraints outlined above.

### Embedding Haskell values

While there is typically no way to obtain the value of a Symbolic datatype
inside a Symbolic function (because, in an arbitrary context, there might be no
such thing as "value" to worry about, at all), going in the other direction is
dead simple: just call the conversion function! At zkFold, we call this
conversion function `fromConstant`.

Now, for a final version of a `checkHash`:

```haskell
import Numeric.Natural                 (Natural)

import ZkFold.Base.Algebra.Basic.Class (FromConstant (..))

checkWith' ::
    (Symbolic c, FromConstant a (FieldElement c)) =>
    a -> (ByteString c -> FieldElement c) -> ByteString c -> Bool c
checkWith' expected hash byteString = hash byteString == fromConstant expected

checkHash' :: Symbolic c => ByteString c -> Bool c
checkHash' = checkWith' (0xDEADF00D :: Natural) MiMC.hash
```

Few things to note:

1. As can be expected from its type, `checkHash'` compiles fine, too.
2. As provided `expected` value is constant, it can (and will) be encoded in the
   circuit using fewer constraints, bringing further optimizations!

!!! danger

    As always is with sensitive information, care must be taken: do not use this
    technique to encode private values inside the circuit! Anyone who gets to
    view the contents of the circuit can extract the information easily.

<!-- ## Framework Overview

### zkFold Symbolic Base
#### Haskell tools
Use the full power of GHC and the Haskell toolstack when developing your zero knowledge applications.

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

- Prove and verify the presence of data matching your patterns in a collection of records -->
