# Koka-language
A fully functional programming language from Microsoft Research, whose central idea is an effects system. The language is still under active development.

## Overview

### What is Koka?

Koka is an experimental functional programming language developed by Daan Leijen at Microsoft Research in 2012. The name means *"effect"* in Japanese, which hints at the language's main feature: **explicit tracking of side effects**.

The compiler translates Koka code directly to C, making it efficient and portable across Windows, macOS, and Linux. An official VS Code extension is also available and installs the compiler automatically.

---

## Core Features

### Effect System

Every function in Koka has a type signature that describes not only its inputs and output, but also **which side effects it may perform**.

```koka
fun divide : (int, int) -> exn int     // may throw an exception
fun print  : (string) -> console ()    // may write to the console
fun rand   : () -> ndet int            // non-deterministic result
```

This makes programs more predictable: if a function has no effects in its type, it is guaranteed to be pure and safe.

### Functional Paradigm

Koka is a functional language at its core:

* Functions are first-class values
* Data is immutable by default
* Pure functions are preferred
* Supports higher-order functions

### Static & Strong Type System

Koka uses a **static type system**, meaning all types are checked at compile time. 
This allows the compiler to catch type errors early, before the program is executed.

Koka also has a **strong type system**, which means there are no automatic conversions between different types. 
Every value must strictly match its expected type, and any conversion must be done explicitly.

Type inference is built in, so explicit annotations are often unnecessary

### Memory Management


Koka uses **Perceus reference counting**, an optimized form of reference counting for memory management instead of a garbage collector.

The compiler automatically inserts allocation and deallocation operations only where they are needed, reducing unnecessary runtime overhead.

When an object has **unique ownership**, Koka enables **FBIP (Fast Borrow In Place)**, allowing in-place updates instead of copying data.

This results in efficient memory usage and performance close to imperative languages, while still maintaining memory safety.

---

## Language Basics

| Concept              | Syntax                                           |
| -------------------- | ------------------------------------------------ |
| Immutable value      | `val x = 42`                                     |
| Mutable variable     | `var x := 42`                                    |
| Function definition  | `fun double(x: int): int { x * 2 }`              |
| Pattern matching     | `match list { Nil -> ... \| Cons(h, t) -> ... }` |
| Lambda               | `fn(x) x * 2`                                    |
| String concatenation | `"hello" ++ " world"`                            |
| List concatenation   | `[1,2] ++ [3,4]`                                 |

> **Important:** Koka is indentation-sensitive. Indentation mistakes often appear as unrelated syntax errors rather than explicit indentation errors.

---

## Strengths & Weaknesses

### Strengths

* Very high reliability due to the effect system
* Clean and readable syntax
* Compiles to efficient C code
* Safe memory management without garbage collector overhead

### Weaknesses

* Steep learning curve, especially around the effect system
* Limited documentation and learning resources
* Primarily a research language rather than a general-purpose language
* Some documented features are not actually implemented (e.g., random number generation)

---

## Project: Jack Compiler in Koka

As part of our course project, we implemented a **Jack compiler** using Koka.

### Compilation Pipeline

#### Stage 1 — Jack → VM

The compiler receives a directory containing `.jack` source files written in the high-level Jack language.

Each `.jack` file is translated into a corresponding `.vm` file written in the intermediate VM language.

#### Stage 2 — VM → Assembly

The compiler then takes all generated `.vm` files and combines them into a single `.asm` assembly file.

### What We Learned

Working with Koka on this project provided hands-on experience with:

* Functional-style compiler construction
* File I/O modules
* String manipulation
* Algebraic data types
* Parsing, transforming, and generating code

