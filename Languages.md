# Languages Syllabi

This is my rough idea for how I see the progress for learning Prolog, Scheme, and Haskell
from an academic perspective. What I mean by that is just that issues of 
software engineering, industry best practices, and so on aren't considered.

- [Languages Syllabi](#languages-syllabi)
  - [Prolog](#prolog)
    - [Core Prolog](#core-prolog)
    - [Higher Prolog](#higher-prolog)
  - [Scheme](#scheme)
    - [Core Scheme](#core-scheme)
    - [Higher Scheme](#higher-scheme)
  - [Haskell](#haskell)
    - [Core Haskell](#core-haskell)
    - [Higher Haskell](#higher-haskell)


## Prolog

### Core Prolog

1) Pure Logic Programming 
   * Facts
   * Rules
   * Queries 
   * Unification 
   * Backtracking
2) Data Types 
   * Terms 
   * Constants
   * Variables
   * Functors
   * Numbers & Arithmetic 
   * Lists 
   * Trees
   * Maps (SWI Dicts) 
   * Characters
   * Strings 
3) Impure Prolog
   * Cut
   * Negeation as Failure

### Higher Prolog

4) Logical Foundations
   * Horn Clauses
   * SLD Resolution
   * SLDFN Resolution
5) Higher-Order/Meta-Programming
6) Definite Clause Grammars
7) Constraint Logic Programming 
8) AI & Theorem Proving
  

## Scheme

### Core Scheme

1) LISP 
   * S-Expressions
     * Integer, Rational, Real, Complex, Number
     * Booleans
     * Characters
     * Strings
     * Symbols & Quotation
     * Dotted Pairs
     * Lists
     * Vectors
     * Equality
   * Lambdas & Evaluation
   * Basic Forms
     * Variable Reference
     * Literals
     * Procedure Calls
     * Procedures
     * McCarthy Formalism
     * Assignment
   * Derived Forms
     * cond, case
     * let, let*, letrec
     * begin, do
2) Higher-Order Functional Programming 
   * Recursion
   * map
   * filter
   * fold
3) Impurity
   * Referential Transparency & define
   * Opacity & set!

### Higher Scheme

4) Metalinguistic Abstraction
   * S-Expressions Formally
   * Quotation & Quasi-Quotation
   * eval/apply
   * Abstract Syntax Trees & Interpreters
5) Continuations
   * CPS
   * call/cc
   * amb
6) Macros
   * syntax-rules 
   * syntax-case


## Haskell

### Core Haskell

1) Typed Functional Programming
   * Basic Types
     * Int
     * Integer
     * Float
     * Double
     * Bool
     * Char
     * String
     * Lists
   * Functions
     * Recursion
     * Pattern Matching
     * Cases
     * Guards
     * Lambdas
     * let and where
2) Hindley-Milner
   * Polymorphism
   * Type Inference & Type Annotations
   * Higher-Order Functions
     * map
     * filter
     * fold
     * scan
     * zip & zipWith
   * Tuples
   * Maybe
   * Either 
   * Function Types & Currying
   * Function Composition & Pointfree Style
   * The ($) Operator and Parentheses
3) User Defined Types
   * data, newtype, type
   * Algebraic Data Types
   * Products vs. Records
4) Typeclasses
   * Numerics
   * Eq
   * Ord
   * Enum
   * Show
   * Read
   * User Defined Typeclasses
   * Instance Declarations & Deriving
   * Superclasses & Subclasses
5) First Look At Monads
   * do Notation
   * IO
6) Containers
   * Maps
   * Sets 
   * Sequences
   * Trees

### Higher Haskell
7) Typeclassopedia:
   * Seven Core Typeclasses
      * Semigroup
      * Monoid
      * Functor
      * Applicative
      * Monad
      * Foldable
      * Traversable
   * Related Type Classes
      * Alternative
      * MonadPlus
      * Contravariant Functor
      * Bifunctor
      * Profunctor
      * Bifoldable
      * Bitraversable
   * Arrows
      * Category
      * Arrow
2) All About Monads
   * Standard Monads
     * List
     * Maybe
     * Reader
     * Writer
     * State
     * Error
     * IO
   * Monad Transformers
   * transformers & mtl
   * Algebraic Effects
   * Free Monads & Freer Monads
3) Laziness
   * Evaluation Strategies
   * Thunks
   * Streams
   * seq & deepseq
   * Forcing Strictness
   * Comonads
4) Metaprogramming
   * Quasi-Quotation
   * Template Haskell
5) Domain Specific Languages
   * Parser Combinators
   * Pretty Printing Documents
   * Embedded DSL
   * Deep Embedding
   * Shallow Embedding
6) Continuations 
   * Zippers
   * CPS
   * call/CC 
   * Delimited Continuations
7) Category Theory & The Lambda Calculus
8) Type Level Programming 
   * Terms, Types, Kinds
   * GADTs
   * RankNTypes & Impredicative Types
   * Existential Types
   * Multiparameter Type Classes & Functional Dependencies
   * Type Families
   * Dependent Types
   * Refinement Types & Liquid Haskell
9)  Optics
10) Recursion Shemes