# What is zkFold Symbolic?

zkFold Symbolic is a subset of Haskell compilable to arithmetic circuits. It is, therefore, a high-level functional programming language that allows developers to harness the power of zero knowledge protocols for their trustless, decentralized, and privacy-preserving applications. It aims to reduce the barrier to entry in the development of zk-enhanced applications and smart contracts.

The key design pillars of Symbolic are code efficiency and safety. It is high-level enough to abstract all mathematical nuances of zero knowledge protocols yet extremely efficient with the arithmetic circuits it produces.

Traditional performance metrics such as CPU cycles and RAM requirements do not make sense in the context of zk-programs. Instead, the performance of a compiled circuit is usually measured in the number of additions and multiplications it contains. Symbolic transpiles the code directly, avoiding the limitations and inefficiencies of a typical VM approach.

The idea of the zkFold Symbolic compiler is inspired by symbolic math software packages (e.g., Wolfram Mathematica). There, user-defined functions are polymorphic in their arguments and can accept both symbolic expressions, with the result being another symbolic expression, as well as concrete numeric values. Similarly, in zkFold Symbolic, an arithmetic circuit representation of some pure polymorphic function is constructed by applying that function to the arithmetic circuit representation of its arguments.