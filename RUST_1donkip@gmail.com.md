# Topic: RUST

**Author**: Allan Kiprop

**QAs Total**: 3

## Q1: How does Rust cater for its lack of an associated runtime?

**Difficulty:** `Senior`

**Source:**

https://dzone.com/articles/discovering-rust

**Answer:**

* Since it lacks a garbage collector that frees the memory of the objects it does not use, handling is achieved using **ownership, borrowing and lifetimes**.

* Normally, each value has an assigned variable **(owner)** and there can only be one owner at a time, when that owner is out of scope the value will be released.

For example:

```cs
fn main() {
    let name = "Jon".to_string();
    greet(name);
    println!("goodbye {}", name); //^^^^ value borrowed here after move
}

fn greet(name:String) {
    println!("hello {}", name);
}
```
* The compiler is telling us that the owner of the variable name has been passed to the greet function, so after running greet it is no longer in that scope. 

* Solving it is as simple as indicating that what we want is to lend the owner, so that when the function ends, get the owner again, and that is indicated with an &. 

```cs
fn main() {
    let name = "Jon".to_string();
    greet(&name);
    println!("goodbye {}", name);
}

fn greet(name:&String) {
    println!("hello {}", name);
}
```

* Therefore, the compiler interprets lifetime by checking the management of ownership and borrowing of the values.

---

## Q2: What does implementing `std::convert::From` achieve in Rust?

**Difficulty:** `Mid`

**Source:**

https://doc.rust-lang.org/beta/std/convert/trait.From.html
https://doc.rust-lang.org/beta/book/ch09-00-error-handling.html

**Answer:**
* It achieves value-to-value conversion while consuming the input value.It is the reciprocal of `Into`.

* One should always prefer implementing `From` over `Into` because implementing `From` automatically provides one with an implementation of `Into` thanks to the blanket implementation in the standard library.

* The `From` is also very useful when performing error handling. When constructing a function that is capable of failing, the return type will generally be of the form `Result<T, E>`. The From trait simplifies error handling by allowing a function to return a single error type that encapsulate multiple error types. 

Examples:

* `String` implements `From<&str>`:

* An explicit conversion from a `&str` to a String is done as follows:
```cs
let string = "hello".to_string();
let other_string = String::from("hello");

assert_eq!(string, other_string);

```
* While performing error handling it is often useful to implement `From` for your own error type. By converting underlying error types to our own custom error type that encapsulates the underlying error type, we can return a single error type without losing information on the underlying cause. 

* The ‘?’ operator automatically converts the underlying error type to our custom error type by calling `Into<CliError>::into` which is automatically provided when implementing `From`. The compiler then infers which implementation of `Into` should be used. 
```cs
use std::fs;
use std::io;
use std::num;

enum CliError {
    IoError(io::Error),
    ParseError(num::ParseIntError),
}

impl From<io::Error> for CliError {
    fn from(error: io::Error) -> Self {
        CliError::IoError(error)
    }
}

impl From<num::ParseIntError> for CliError {
    fn from(error: num::ParseIntError) -> Self {
        CliError::ParseError(error)
    }
}

fn open_and_parse_file(file_name: &str) -> Result<i32, CliError> {
    let mut contents = fs::read_to_string(&file_name)?;
    let num: i32 = contents.trim().parse()?;
    Ok(num)
}
```
---

## Q3: Why do we use `deref` coercion in Rust?

**Difficulty:** `Junior`

**Source:**

https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/deref-coercions.html

**Answer:**

* Deref coercion is handy in automatically converting references to pointers into references to their contents. It’s normally used to overload `*`, the dereference operator.

Common sorts of deref coercions include;

* `&String` to `&str`
 
* `&Arc<T>` to `&T`
  
* `&Vec<T>` to `&[T]`
  
* `&Rc<T>` to `&TW`
  
* `&Box<T>` to `&T`


For example:

```cs
use std::ops::Deref;

struct DerefExample<T> {
    value: T,
}

impl<T> Deref for DerefExample<T> {
    type Target = T;

    fn deref(&self) -> &T {
        &self.value
    }
}

fn main() {
    let x = DerefExample { value: 'a' };
    assert_eq!('a', *x);
}
```
