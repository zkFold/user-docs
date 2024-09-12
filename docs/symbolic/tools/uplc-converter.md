# UPLC Converter

## Overview
UPLC Converter is a tool that transpiles Untyped Plutus Core (UPLC) scripts to arithmetic circuits. It makes it possible to use UPLC scripts in the zkFold Symbolic framework on par with Symbolic smart contracts.

According to the [Plutus Core specification](https://plutus.cardano.intersectmbo.org/resources/plutus-core-spec.pdf), a _UPLC program_ is a tree where nodes are _UPLC terms_. UPLC Converter recursively traverses the UPLC program and converts each term to the corresponding zkFold Symbolic expression. 

The resulting Haskell expression is then converted to an arithmetic circuit using the zkFold Symbolic framework. The circuit outputs `1` if and only if the UPLC program executes successfully on the given input.

## Specification
In this section, we describe the rules for converting UPLC terms to arithmetic circuits.

### Variables
```UPLC title="UPLC"
x
```
Every variable must first be defined in a $\lambda$-abstraction term. When we encounter a variable term, we look up the associated `SymbolicData` object in the environment that is defined as a `Map`.

```Haskell title="Haskell"
x :: SymbolicData x => Map Natural x -> Natural -> x
```

### Constants
```UPLC title="UPLC"
(con T c)
```

Every constant in UPLC is constructed using the predefined built-in types and type operators. All those types and type operators have their counterparts in Haskell base library. Thus, constants can be converted to `SymbolicData` objects using the `fromConstant` function.

```Haskell title="Haskell"
con :: (FromConstant a x, SymbolicData x) => a -> x
con = fromConstant
```

### Built-in functions
```UPLC title="UPLC"
(builtin b)
```

Every version of UPLC has a fixed set of built-in functions. We can, therefore, define zkFold Symbolic counterparts for each of them. For example, a UPLC built-in function `ifThenElse` is converted to the function of the same name in zkFold Symbolic.

```Haskell title="Haskell"
ifThenElse :: (Symbolic c, SymbolicData x, Context x ~ c) => Bool c -> x -> x -> x
```

### $\lambda$-abstraction
```UPLC title="UPLC"
(lam x M)
```

Lambda abstraction term adds a new variable to the environment and converts the body of the lambda term.

```Haskell title="Haskell"
lam :: (SymbolicData x, SymbolicData y) => (x -> y) -> x -> y
```

### Function application
```UPLC title="UPLC"
[M N]
```

Function application term simply converts to the function application in Haskell.

```Haskell title="Haskell"
m :: (SymbolicData x, SymbolicData y) => x -> y

n :: SymbolicData x => x

m n :: SymbolicData y => y
```

### Delay and force
```UPLC title="UPLC"
(delay M)

(force M)
```

Delay and force implement type abstraction and type application in UPLC. They are skipped during the conversion process.

### Error
```UPLC title="UPLC"
(error)
```

Currently, the error term is not supported in UPLC Converter.

## CLI Commands

Below we provide the list of available commands for UPLC Converter.

### Convert UPLC to Circuit

```bash
uplc-converter circuit <input-file> <output-file>
```

The command expects the path to the input UPLC script in CBOR and the path to the output zkFold Circuit file. The output file will contain the generated arithmetic circuit.

### Convert a Plutus V3 Script to a Symbolic Verifier Script

```bash
uplc-converter symbolic-script <input-file> <output-file>
```

This command converts a Plutus V3 script to a Symbolic Verifier script. The input file should be a zkFold Circuit file, and the output file will contain the symbolic verifier script in CBOR.

### Generate a Forwarding Script

```bash
uplc-converter forwarding-script <input-file> <output-file>
```

This command generates a forwarding script that forwards the validation to the given UPLC script. The input file should be a zkFold Circuit file, and the output file will contain the symbolic verifier script in CBOR.