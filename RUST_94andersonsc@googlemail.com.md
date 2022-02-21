# Topic: Rust

**Author**: Scott Anderson

**QAs Total**: 3

# Q1: How to interpolate variables into a string in Rust?

**Difficulty**: Junior/Hobbyist

**Sources**:
 - https://stackoverflow.com/questions/30154541/how-do-i-concatenate-strings
 - https://doc.rust-lang.org/std/macro.format.html

**Details**:
(What is 'string interpolation'?)[https://www.webopedia.com/definitions/string-interpolation/]

Rust code example:
```
fn printFooBar() {
  let foo: &str = 'Foo';
  let bar : &str = 'Bar'

  let together = format!("{}, {}!", foo, bar);
  println!(together);
}
```

**Answer**

You can interpolate a string using the `format!()` function in Rust, to produce a new string with dynamic values injected.

To use the `format!()` function, the first parameter must be the 'format string' (a string literal) in which variables' values are to be injected. Within the 'format string' values are injected in sequence each time a `{}` notation occurs.

Additional parameters following the first parameter should be variables or primitive literals - anything which implements the `to_string()` trait, which includes:
 - strings
 - integers
 - floats
And does not include:
 - arrays
 - tuples

# Q2: How do I implement a Trait for an action within a struct?

**Difficulty**: Intermediate

**Sources**:
 - https://dzone.com/articles/discovering-rust

**Details**:
Example
```
struct Vector {
  x: f32
  y: f32
}

Trait Addition {
  fn add(self: Vector, other: Vector) -> Vector;
}

impl Addition for Vector  {
  fn add(self, other: Vector) -> Vector {
    Vector {
      x: self.x + other.x
      y: self.y + other.y
    }
  }
}

let vec1 = {
  x: 100,
  y: 265
}

let vec2 = {
  x: 250,
  y: -122
}

let result = vec1.add(vec2);

println!("The resultant vector has x: {}, y: {}", result.x, result.y);
// The line above should print: "The resultant vector has x: 350, y: 143"
```

**Answer**:

A `trait` is an abstract definition for a struct which will need to be implemented via an `impl` call per-class

# Q3: Why am I getting an error referring to

**source**: https://stackoverflow.com/questions/25818082/vector-of-objects-belonging-to-a-trait

Given the following code:
```
trait Animal {
    fn make_sound(&self) -> String;
}

struct Cat;
impl Animal for Cat {
    fn make_sound(&self) -> String {
        "meow".to_string()
    }
}

struct Dog;
impl Animal for Dog {
    fn make_sound(&self) -> String {
        "woof".to_string()
    }
}

let v: Vec<Animal> = Vec::new();
```
...the following lines throw an error:
```
    let v: Vec<Animal> = Vec::new();
    //throws: "error: instantiating a type parameter with an incompatible type `Animal`, which does not fulfill `Sized`"
```
Please explain in your own words:
 - What this error is referring to
 - A potential solution to resolve the issue

 **Details**:
 Please provide a working example to fix the code

**Answer**:

 - What is the error?

A trait object cannot be passed directly as a type parameter, as it does not have the 'Sized' trait.
The 'Sized' trait is an associated memory allocation size, which is implicit in pointer types, such as `&str`

- A potential solution

The logical mistake in the code is that the `Trait` needs to be encapsulated with a container that implements `Sized`. For instance replacing the line:
```
let v: Vec<Animal> = Vec::new();
```
With:
```
let v: Vec<Box<dyn Animal>> = Vec::new();
```



