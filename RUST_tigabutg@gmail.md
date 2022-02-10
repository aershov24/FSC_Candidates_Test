# Q1: When to use Rust?

**Difficulty:**  `Junior`

**Source:**

<https://docs.microsoft.com/en-us/learn/modules/rust-introduction/3-rust-features?ns-enrollment-type=LearningPath&ns-enrollment-id=learn.languages.rust-first-steps>

**Answer:**

The `Rust` language has many strengths to consider when choosing the best language for your project:

* `Rust` allows for control over the **performance** and **resource** consumption of programs and libraries written in the language on par with C and C++, while still being _memory_ safe by default eliminating entire classes of common bugs.
* `Rust` has rich abstraction features that allow developers to **encode** many of the invariants of their program into _code_, which is then checked by the compiler instead of relying on convention or documentation. This feature can often lead to the feeling of **"if it compiles, it works."**
* `Rust` has built-in tools for _building, testing, documenting, and sharing_ code as well as a rich ecosystem of third-party tools and libraries. These tools can make some tasks that are difficult in some languages, such as *building dependencies*, easy and productive in `Rust`.

---

# Q2: What is the difference between Rust’s `String` and `str`?

**Difficulty**: `mid`

**Source:**

<https://medium.com/@raphaelribas/rusts-string-vs-str-a5183e3f180c>

**Answer:**

 The type `str` refers to the **actual array of characters**, unlike most languages where _strings are a pointer to the array of characters_. In practice you can’t use the type `str` for most of it, a lot of things require the size of the object to be known at compile time, like **structs or function arguments**, `&str` however is ok, because a _reference is actually a pointer to the data_.



 The type `String` on the other hand is more like _other programming languages_, it basically **wraps** a pointer to a `str` that you can modify. It is a more like `std::string` from C++. But note that a `String` variable also **owns** the `str` value underneath. _Which is a very important fact for Rust_. When you have `&str`, because it is a **reference**, the compiler needs to be convinced that the original `str` it refers to will live at least as long as the reference. Which makes it inconvenient or even impossible to use `&str` in certain cases.

 ---

# Q3: Why we would need `unsafe traits`?

**Difficulty**: `senior`

**Source:** 

**Book:** _Mastering Rust Second Edition:  Rahul Sharma Vesa Kaihlavirta_

* One of the primary motivations for `unsafe traits` existing in the first place
is _to mark types that cannot be sent to or shared between threads_. This is achieved via the unsafe `Send` and `Sync` marker traits.

* Another motivation for marking traits as `unsafe` is to **encapsulate operations** that are likely to have an undefined behavior by a family of types.

**NOTE**: With the motivation for `unsafe traits` covered, let's look at how we can define and use `unsafe traits`. _Marking a trait as unsafe doesn't make your methods unsafe_. We can have `unsafe traits` that have `safe` methods. The opposite is also true; we can have a `safe trait` that can have `unsafe` methods within it, _but that doesn't signify that the trait is unsafe_. `Unsafe traits` are denoted in the same way as functions by simply prepending them with the **unsafe keyword**:

For example

```rust
// unsafe_trait_and_impl.rs
struct MyType;
unsafe trait UnsafeTrait {
unsafe fn unsafe_func(&self);
fn safe_func(&self) {
println!("Things are fine here!");
}
}
trait SafeTrait {
unsafe fn look_before_you_call(&self);
}
unsafe impl UnsafeTrait for MyType {
unsafe fn unsafe_func(&self) {
println!("Highly unsafe");
}
}
impl SafeTrait for MyType {
unsafe fn look_before_you_call(&self) {
println!("Something unsafe!");
}
}


fn main() {
let my_type = MyType;
my_type.safe_func();
unsafe {
my_type.look_before_you_call();
}
}
```
