# UPLC Converter

## Overview
UPLC Converter is a tool that transpiles Untyped Plutus Core (UPLC) scripts to arithmetic circuits. It makes it possible to use UPLC scripts in the zkFold Symbolic framework on par with Symbolic smart contracts.

According to the [Plutus Core specification](https://plutus.cardano.intersectmbo.org/resources/plutus-core-spec.pdf), a _UPLC program_ is a tree where nodes are _UPLC terms_. UPLC Converter recursively traverses the UPLC program and converts each term to the corresponding zkFold Symbolic expression. For example, a term type $[M~ N]$ is converted by the following Haskell function:
```Haskell
funcApply :: (SymbolicData n, SymbolicData k, m ~ n -> k) => m -> n -> k
funcApply f x = f x
```
In order to convert $[M~ N]$, we supply the conversion `f` for $M$ as the first argument and the conversion `x` for $N$ as the second argument.

The resulting Haskell expression is then converted to an arithmetic circuit using the zkFold Symbolic framework. The circuit outputs `1` if and only if the UPLC program executes successfully on the given input.

## Specification

## CLI Commands