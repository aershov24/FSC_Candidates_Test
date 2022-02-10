# Topic: RUST

**Author**: Allan Kiprop

**QAs Total**: 3

## Q1: How does Rust cater for its lack of an associated runtime?

**Difficulty:** `Senior`

**Source:**

https://dzone.com/articles/discovering-rust

**Answer:**

Since it lacks a garbage collector that frees the memory of the objects it does not use, handling is achieved using **ownership, borrowing and lifetimes**.

Normally, each value has an assigned variable **(owner)** and there can only be one owner at a time, when that owner is out of scope the value will be released.

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
The compiler is telling us that the owner of the variable name has been passed to the greet function, so after running greet it is no longer in that scope. 

Solving it is as simple as indicating that what we want is to lend the owner, so that when the function ends, get the owner again, and that is indicated with an &. 

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

Therefore, the compiler interprets lifetime by checking the management of ownership and borrowing of the values.


---

# Topic: RUST

**Author**: Allan Kiprop

**QAs Total**: 3

## Q2: What does implementing `std::convert::From` achieve in Rust?

**Difficulty:** `Mid`

**Source:**

https://dzone.com/articles/discovering-rust

**Answer:**

Since it lacks a garbage collector that frees the memory of the objects it does not use, handling is achieved using **ownership, borrowing and lifetimes**.

Normally, each value has an assigned variable **(owner)** and there can only be one owner at a time, when that owner is out of scope the value will be released.

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
The compiler is telling us that the owner of the variable name has been passed to the greet function, so after running greet it is no longer in that scope. 

Solving it is as simple as indicating that what we want is to lend the owner, so that when the function ends, get the owner again, and that is indicated with an &. 

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

Therefore, the compiler interprets lifetime by checking the management of ownership and borrowing of the values.
# Topic: RUST

**Author**: Allan Kiprop

**QAs Total**: 3

## Q3: How does rust cater for its lack of an associated runtime?

**Difficulty:** `Senior`

**Source:**

https://dzone.com/articles/discovering-rust

**Answer:**

Since it lacks a garbage collector that frees the memory of the objects it does not use, handling is achieved using **ownership, borrowing and lifetimes**.

Normally, each value has an assigned variable **(owner)** and there can only be one owner at a time, when that owner is out of scope the value will be released.

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
The compiler is telling us that the owner of the variable name has been passed to the greet function, so after running greet it is no longer in that scope. 

Solving it is as simple as indicating that what we want is to lend the owner, so that when the function ends, get the owner again, and that is indicated with an &. 

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

Therefore, the compiler interprets lifetime by checking the management of ownership and borrowing of the values.
