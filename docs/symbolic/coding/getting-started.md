# Getting Started

ZKFold Symbolic uses the Haskell type system to distinguish arithmetizable computations from non-arithmetizable ones.

A pure function `f` of any arity can be compiled into an arithmetic circuit provided that:

- Every argument and the return value of f belongs to the class `Arithmetizable a`.

- Type `a` belongs to the class `Symbolic`.

The Standard Library, as well as the Cardano Type Library, contains a collection of types that cover the basic use-cases. In the next section, we discuss how to define your own `Arithmetizable a` types.