# Topic: Rust

**Author**: amiodataco

**QAs Total**: 3

---

## Q1: Why are `macro_rules!` useful in Rust?

**Difficulty:** `Senior`

**Source:**

https://doc.rust-lang.org/rust-by-example/macros.html

**Details**:

Rust provides a powerful _macro system_ that allows **metaprogramming**, unlike macros in **C** and other languages, *Rust macros* are expanded into abstract syntax trees, rather than string preprocessing, so you don't get unexpected precedence bugs.


**Answer:**

_Macros_ in Rust are useful because:


* **You Don't repeat yourself.** There are many cases where you may need similar functionality in multiple places but with different types. Often, writing a macro is a useful way to avoid repeating code.
* **Domain-specific languages**. Macros allow you to define special syntax for a specific purpose. 
* **Variadic interfaces.** Sometimes you want to define an interface that takes a variable number of arguments. An example is `println!` which could take any number of arguments, depending on the format string!.

Macros are created using the `macro_rules!` macro:


```rust

// This is a simple macro named `say_hello`.
macro_rules! say_hello {
    // `()` indicates that the macro takes no argument.
    () => {
        // The macro will expand into the contents of this block.
        println!("Hello!");
    };
}
```

---

## Q2: What is `Crate` for Rust?

**Difficulty:** `Junior`

**Source:**

https://doc.rust-lang.org/cargo/appendix/glossary.html

**Answer:**

A Rust _crate_ is either a library or an executable program, referred to as either a **library crate** or a **binary crate**, respectively. Loosely, the term _crate_ may refer to either the source code of the target or to the compiled artifact that the target produces. It may also refer to a **compressed package**  fetched from a [`registry`](https://doc.rust-lang.org/cargo/appendix/glossary.html#registry).


---

## Q3: What are traits in Rust?

**Difficulty**: `Mid`

**Source:**

https://www.educative.io/edpresso/what-are-traits-in-rust

**Answer:**

A *trait* in Rust is a group of methods that are defined for a particular type.
Traits are an abstract definition of shared behavior amongst different types. So, 
in a way, traits are to Rust what interfaces are to Java or abstract classes are to
*C++*. A trait method is able to access other methods within that trait.

A trait is implemented similarly to an *inherent implementation* except that a
trait name and the `for` keyword follow the `impl` keyword before the type name.
Let’s implement an built-in trait called `ToString` on a `Dog` struct:


**Code**

```rust

struct Dog {
  name: String,
  age: u32, 
  owner: String
}


// Implementing an in-built trait ToString on the Dog struct
impl ToString for Dog {
  fn to_string(&self) -> String{
    return format!("{} is a {} year old dog who belongs to {}.", self.name, self.age, self.owner);
  }
}

fn main() {
  let dog = Dog{name: "Frodo".to_string(), age: 3, owner: "Maryam".to_string()};
  println!("{}", dog.to_string());
}

```

**Code Output** 

```
Frodo is a 3 year old dog who belongs to Maryam.
```


