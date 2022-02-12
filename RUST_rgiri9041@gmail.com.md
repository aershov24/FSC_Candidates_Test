# Topic: RUST

**Author**: Raj Kumar Giri

**QAs Total**: 3

---

## Q1:  why does not `RUST tuple` use square bracket to access elements inside? 
**Difficulty:** `Junior`

**Source:**

 https://stackoverflow.com/questions/66792715/why-does-not-rust-tuple-use-square-bracket-to-access-elements-inside
 
**Answer:**

 The square bracket indexing syntax in Rust can always be used with a dynamic index. That means that the following code should work:
 ```rs
for i in 0..3 {
    do_something_with(x[i]);
}
```
Even if the compiler may not know which value i will take, it must know the type of x[i]. For heterogeneous tuple types like (i32, f64, u8) that's impossible. There is no type that is i32, f64 and u8 at the same time, so the traits Index and IndexMut can't be implemented:
```rs
// !!! This will not compile !!!

// If the Rust standard library allowed square-bracket indexing on tuples
// the implementation would look somewhat like this:
impl Index<usize> for (i32, f64, u8) {
    type Output = ???; // <-- What type should be returned?

    fn index(&self, index: usize) -> &Self::Output {
        match index {
            0 => &self.0,
            1 => &self.1,
            2 => &self.2,
            _ => panic!(),
        }
    }
}

fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);
    for i in 0..3 {
        do_something_with(x[i]);
    }
}
```
Theoretically the standard library could provide an implementation for homogeneous tuples (i32, i32, i32) etc. but this is a corner case that can easily be replaced by an array [i32; 3]. So there is no such implementation.

## Q2:   What is the difference between Rust’s `String` and `str`?

**Difficulty:** `Mid`

**Source:**

 https://www.ameyalokare.com/rust/2017/10/12/rust-str-vs-String.html

**Answer:**
` String`
If you’re a Java programmer, a Rust String is semantically equivalent to `StringBuffer` (this was probably a factor in my confusion, as I’m so used to equating String with immutable). As such, a `String` maintains a length and a capacity whereas a str only has a len() method. As an example:
```ra
let mut s = String::from("Hello, Rust!");
println!("{}", s.capacity()); // prints 12
s.push_str("Here I come!");
println!("{}", s.len()); // prints 24

let s = "Hello, Rust!";
println!("{}", s.capacity()); // compile error: no method named `capacity` found for type `&str`
println!("{}", s.len()); // prints 12
&str
```
You can only ever interact with str as a borrowed type aka &str. This is called a string slice, an immutable view of a string. This is the preferred way to pass strings around, as we shall see.

`&String`
This is a reference to a `String`, also called a `borrowed type`. This is nothing more than a pointer which you can pass around without giving up `ownership`. Turns out a &String can be coerced to a &str:
```rs
fn main() {
    let s = String::from("Hello, Rust!");
    foo(&s);
}

fn foo(s: &str) {
    println!("{}", s);
}
```
In the above example, foo() can take either string slices or borrowed Strings, which is super convenient. As such, you almost never need to deal with `&Strings`. The only real use case I can think of is if you want to pass a mutable reference to a function that needs to modify the string:
```rs
fn main() {
    let mut s = String::from("Hello, Rust!");
    foo(&mut s);
}

fn foo(s: &mut String) {
    s.push_str("appending foo..");
    println!("{}", s);
}
```

## Q3:  How does `Rust` guarantee memory safety and prevent segfaults?

**Difficulty**: `Senior`

**Source:**

 https://stackoverflow.com/questions/36136201/how-does-rust-guarantee-memory-safety-and-prevent-segfaults

**Details**:

How `Rust` achieves memory safety is, at its core, actually quite simple. It hinges mainly on two principles: ownership and borrowing.
**Answer:**

 `Ownership`

The `compiler` uses an affine type system to track the ownership of each value: a value can only be used at most once, after which the compiler refuses to use it again.
```rs
fn main() {
    let original = "Hello, World!".to_string();
    let other = original;
    println!("{}", original);
}
yields an error:

error[E0382]: use of moved value: `original`
 --> src/main.rs:4:20
  |
3 |     let other = original;
  |         ----- value moved here
4 |     println!("{}", original);
  |                    ^^^^^^^^ value used here after move
  |
  = note: move occurs because `original` has type `std::string::String`, which does not implement the `Copy` trait
This, notably, prevents the dreaded double-free regularly encountered in C or C++ (prior to smart pointers).
```

`Borrowing`

The illumination that comes from Rust is that `memory issues` occur when one mixes aliasing and mutability: that is, when a single piece of memory is accessible through multiple paths and it is mutated (or moved away) leaving behind dangling pointers.

The core tenet of borrow checking is therefore: `Mutability XOR Aliasing`. It's similar to a Read-Write Lock, in principle.

This means that the `Rust` compiler tracks aliasing information, for which it uses the lifetime annotations (those 'a in &'a var) to connect the lifetime of references and the value they refer to together.

A value is borrowed if someone has a reference to it or INTO it (for example, a reference to a field of a struct or to an element of a collection). A borrowed value cannot be moved.

`Mutability (without aliasing)`

You can obtain only a single mutable reference (&mut T) into a given value at any time, and no immutable reference into this value may exist at the same time; it guarantees that you have exclusive access to this tidbit of memory and thus you can safely mutate it.

Aliasing (without mutability)

You can obtain multiple immutable references (&T) into a given value at any time. However you cannot mutate anything through those references (*).
