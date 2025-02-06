---
title: "Basic types"
description: "The basic types."
author: "zkFold"
date: "2024-11"
PUBLIC: true
---

# Basic Types

Here are some of the types from Symbolic Standard Library which you are most
likely to encounter while working with the language. All of them implement
both `SymbolicData` and `SymbolicInput` except for `(e -> a)`, which is only
`SymbolicData`.

`Bool c`

:   Symbolic datatype corresponding to the usual boolean value. Supports basic
    boolean operations (`&&`, `||`, `not`, `xor` etc.) and conditional branching
    &mdash; as long as the resulting type is `SymbolicData`:

    ```haskell
    import ZkFold.Symbolic.Data.Conditional  (bool)
    import ZkFold.Symbolic.Data.Eq           ((==))
    import ZkFold.Symbolic.Data.FieldElement (FieldElement)

    safeInv :: Symbolic c => FieldElement c -> FieldElement c -> FieldElement c
    safeInv default_ x = bool (finv x) default_ (x == zero)
    ```

    Located in `ZkFold.Symbolic.Data.Bool`.

`FieldElement c`

:   Corresponds to a single native field element of a context `c`. Supports
    comparison, all field operations and can be obtained from `Natural`,
    `Integer` and from the Haskell value of a native field element (the latter
    is called `BaseField c`).

    Located in `ZkFold.Symbolic.Data.FieldElement`.

`ByteString n c`

:   Fixed-size bytestring. Supports equality, bitwise logical operations and
    various operations which treat it as a contiguous sequence of elements
    (bits): concatenation, reversing, truncation, extension etc.

    Most operations require `KnownNat n`, which is to be expected.

    Located in `ZkFold.Symbolic.Data.ByteString`.

`(x, y)`

:   As long as both `x` and `y` are `SymbolicData` (`SymbolicInput`), a pair
    (and, in general, a tuple) of them is, too.

`e -> a`

:   As long as `a` is `SymbolicData`, `e -> a` is, too. Unfortunately, the same
    doesn't hold for `SymbolicInput`, so we currently cannot compile functions
    which take another function as input; however, thanks to `SymbolicData`
    instance, both currying and branching via `Bool c` work with functions.

`Vector n x`

:   This is our custom "fixed-size" vector type. Usually, we use it in an
    ordinary Haskell code. However, as long as `x` is `SymbolicData`
    (`SymbolicInput`) and `n` is `KnownNat`, a `Vector` of them is, too.

    Definition of a `Vector` can be found in `ZkFold.Base.Data.Vector`.

`Maybe c x`

:   Symbolic `Maybe` datatype. As long as `x` is `SymbolicData` in context `c`,
    `Maybe c x` is, too, and provides familiar `Maybe` interface: construnctors
    `just`, `nothing`, as well as `maybe` combinator.

!!! coming-soon "Coming soon"

    While sum types cannot be `SymbolicData` as-is, soon we will offer a
    lightweight wrapper which can turn any algebraic datatype containing
    Symbolic datatypes into their Symbolic counterpart.

`UInt n r c`

:   Fixed-width unsigned integer. Supports comparison, all ring operations which
    treat it as a residue modulo `2^n` and can be obtained from `Natural`,
    `Integer` and from `FieldElement c` as long as `n` is big enough.

    `r` is a register size which can be tweaked in different usecases for
    maximum performance. Can be set either to `Auto` which greedily chooses
    biggest registers or to `Fixed m` where `m` is fixed number of bits in a
    register.

    Most operations require `KnownNat (NumberOfRegisters (BaseField c) n r)`.

    Located in `ZkFold.Symbolic.Data.UInt`.

!!! coming-soon "Coming soon"

    Actually, using `NumberOfRegisters` slows down compilation of Haskell code
    quite a bit and also hurts readability, so we are going to get rid of this
    constraint soon and only require `KnownNat n` and `KnownRegisterSize r`.

`FFA p c`

:   Foreign-field arithmetic modulo `p` inside arbitrary context `c`. Currently
    only ring operations are supported.

    Located in `ZkFold.Symbolic.Data.FFA`.

!!! coming-soon "Coming soon"

    Soon, we will migrate FFA to more efficient implementation, which would also
    allow for exact equality and fast exponentiation.

`Point (Ed25519 c)`

:   Point of an Edwards 25519 curve as a Symbolic datatype. Supports basic curve
    operations.

!!! coming-soon "Coming soon"

    Currently we are in an active process of integrating Incrementally
    Verifiable Computations (IVCs) into zkFold Symbolic. Based on this
    technique, soon we will be able to provide arbitrarily-sized types for
    Symbolic, including `List`s, arbitrary-sized `ByteString`s,
    arbitrary-precision arithmetic and more!
