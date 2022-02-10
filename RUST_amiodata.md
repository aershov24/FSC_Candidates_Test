# Topic: Rust

**Author**: amiodataco

**QAs Total**: 3

---

## Q1: How can a Rust program access metadata from its `Cargo` package?

**Difficulty:** `Senior`

**Source:**

https://stackoverflow.com/questions/27840394/how-can-a-rust-program-access-metadata-from-its-cargo-package

**Details**:

Provide some code example.

**Answer:**

`Cargo` passes some metadata to the compiler through environment variables, a list of which can be found in the [`Cargo documentation pages`](http://doc.crates.io/environment-variables.html. You can access environment variables using the `env!()` macro. To insert the version number of your program you can do this:


```rust
const VERSION: &str = env!("CARGO_PKG_VERSION");

// ...

println!("MyProgram v{}", VERSION);
```

---

## Q2: What is `Crate` for Rust?

**Difficulty:** `Junior`

**Source:**

https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md

**Answer:**

A Rust _crate_ is either a library or an executable program, referred to as either a _library crate_ or a _binary crate_, respectively. Loosely, the term _crate_ may refer to either the source code of the target or to the compiled artifact that the target produces. It may also refer to a compressed package fetched from a [`registry`](https://doc.rust-lang.org/cargo/appendix/glossary.html#registry).



---

## Q3: What does the `ops::Try` trait describe in Rust? 

**Difficulty**: `Mid`

**Source:**

https://rust-lang.github.io/rfcs/3058-try-trait-v2.html

**Answer:**

The `ops::Try` trait describes a type's behavior when used with the `?` operator, like how the `ops::Add` trait describes its behavior when used with the `+` operator.