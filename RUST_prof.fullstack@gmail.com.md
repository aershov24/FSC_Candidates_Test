# Topic: Rust Programming Language

**Author**: Muhammad Ali Khan

**QAs Total**: 3

---

## Q1: How is the Rust `ownership model` executed and enforced?

**Difficulty:** `Junior`

**Source:**

https://hacks.mozilla.org/2015/05/diving-into-rust-for-the-first-time/

https://dzone.com/articles/ownership-in-the-rust-language

https://github.com/alshdavid/BorrowScript#borrow-checker-tldr

https://doc.rust-lang.org/stable/book/2018-edition/ch04-01-what-is-ownership.html

**Answer:**

The [_Rust Compiler_](https://www.rust-lang.org/) and [_Borrow checker_](https://github.com/alshdavid/BorrowScript#borrow-checker-tldr) execute and enforce the checks required for the [`ownership model`](https://hacks.mozilla.org/2015/05/diving-into-rust-for-the-first-time/) to work.  

---

## Q2: How to iterate through `enum` values in Rust?

**Difficulty:** `Mid`

**Source:**

https://stackoverflow.com/questions/21371534/in-rust-is-there-a-way-to-iterate-through-the-values-of-an-enum

https://docs.rs/enum-iterator/latest/enum_iterator/

**Details**:

Provide some code example.

**Answer:**

The [`strum`](https://crates.io/crates/strum) crate can be used to easily _iterate_ through the values of an `enum`.

For example:

```rust
use strum::IntoEnumIterator; // 0.17.1
use strum_macros::EnumIter; // 0.17.1

#[derive(Debug, EnumIter)]
enum Direction {
    NORTH,
    SOUTH,
    EAST,
    WEST,
}

fn main() {
    for direction in Direction::iter() {
        println!("{:?}", direction);
    }
}
```

---

## Q3: Why are `explicit lifetimes` needed in Rust?

**Difficulty**: `Senior`

**Source:**

https://stackoverflow.com/questions/31609137/why-are-explicit-lifetimes-needed-in-rust/31609892#31609892

**Details**:

Provide code and **program output**.

**Answer:**

* Rust **implicitly** adds and assigns a lifetime definition using apostrophe (‘) symbol for references in the function parameters.
* If you are _not_ outputting these references, then there is no compiler error.
* _However_, if you output the reference, then the compiler needs to know what lifetime to assign to output.

For example:

```rust
fn foo<'a, 'b>(x: &'a u32, y: &'b u32) -> &'a u32 {
    x
}

fn main() {
    let x = 12;
    let z: &u32 = {
        let y = 42;
        foo(&x, &y)
    };
}
```

This code _compiles_ because the result of foo has the _same lifetime_ as its first argument (‘a), so it may **outlive** its second argument. This is expressed by the lifetime names in the signature of foo.

However, the compiler would _complain_ that y does not live long enough if the arguments are _switched_ in the call to foo.

Consider:

[![Terminal-output.png](https://i.postimg.cc/T2Z4d9rr/Terminal-output.png)](https://postimg.cc/K4DNQtpz)

