# Topic: Rust

**Author**: XuXiZhen

**Conact EMail**: xizhen1109@gmail.com

**QAs Total**: 3

---

## Q1: What are the differences between Rust's `String` and `str`?

**Difficulty:** `Junior`

**Source**:

https://stackoverflow.com/questions/27791532/how-do-i-create-a-global-mutable-singleton

**Answer**:

`String` is the dynamic heap string type, like `Vec`: use it when you need to own or modify your string data.

`str` is an immutable1 sequence of UTF-8 bytes of dynamic length somewhere in memory. Since the size is unknown, one can only handle it behind a pointer. This means that `str` most commonly2 appears as `&str`: a reference to some UTF-8 data, normally called a "string slice" or just a "slice". [A slice](https://doc.rust-lang.org/book/ch04-03-slices.html) is just a view onto some data, and that data can be anywhere, e.g.

- `In static storage`: a string literal `"foo"` is a `&'static str`. The data is hardcoded into the - executable and loaded into memory when the program runs.

- `Inside a heap allocated String`: [String dereferences to a &str view](https://doc.rust-lang.org/std/string/struct.String.html#deref) of the `String`'s data.

- `On the stack`: e.g. the following creates a stack-allocated byte array, and then gets a [view of that data as a &str](https://doc.rust-lang.org/std/str/fn.from_utf8.html):

```js
use std::str;

let x: &[u8] = &[b'a', b'b', b'c'];
let stack_str: &str = str::from_utf8(x).unwrap();
```

In summary, use String if you need owned `string` data (like passing strings to other threads, or building them at runtime), and use `&str` if you only need a view of a string.

This is identical to the relationship between a vector `Vec<T>` and a slice `&[T]`, and is similar to the relationship between by-value `T` and by-reference `&T` for general types.

- A `str` is fixed-length; you cannot write bytes beyond the end, or leave trailing invalid bytes. Since UTF-8 is a variable-width encoding, this effectively forces all strs to be immutable in many cases. In general, mutation requires writing more or fewer bytes than there were before (e.g. replacing an `a` (1 byte) with an `ä` (2+ bytes) would require making more room in the `str`). There are specific methods that can modify a `&mut str` in place, mostly those that handle only ASCII characters, like [make_ascii_uppercase](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_uppercase).

- [Dynamically sized types](http://smallcultfollowing.com/babysteps/blog/2014/01/05/dst-take-5/) allow things like `Rc<str>` for a sequence of reference counted UTF-8 bytes since Rust 1.2. Rust 1.21 allows easily creating these types.

---

## Q2: How do I `cross-complie` in Rust?

**Difficulty:** `Mid`

**Source**:

https://rust-lang.github.io/rustup/cross-compilation.html

**Answer**:

Rust [supports a great number of platforms](https://doc.rust-lang.org/nightly/rustc/platform-support.html). For many of these platforms The Rust Project publishes binary releases of the standard library, and for some the full compiler. rustup gives easy access to all of them.

When you first install a toolchain, `rustup` installs only the standard library for your host platform - that is, the architecture and operating system you are presently running. To compile to other platforms you must install other target platforms. This is done with the `rustup target add` command. For example, to add the Android target:

- $ rustup target add arm-linux-androideabi
info: downloading component 'rust-std' for 'arm-linux-androideabi'
info: installing component 'rust-std' for 'arm-linux-androideabi'

With the `arm-linux-androideabi` target installed you can then build for Android with Cargo by passing the `--target` flag, as in `cargo build --target=arm-linux-androideabi`.

Note that rustup target add only installs the Rust standard library for a given target. There are typically other tools necessary to cross-compile, particularly a linker. For example, to cross compile to Android the [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) must be installed. In the future, `rustup` will provide assistance installing the NDK components as well.

To install a target for a toolchain that isn't the default toolchain use the `--toolchain` argument of rustup target add, like so:

- $ rustup target add --toolchain <toolchain> <target>...

To see a list of available targets, `rustup target list`. To remove a previously-added target, `rustup target remove`.

---

## Q3: What is the relation between `auto-dereferencing` and `deref` coercion?

**Difficulty**: `Senior`

**Source**:

https://stackoverflow.com/questions/53341819/what-is-the-relation-between-auto-dereferencing-and-deref-coercion

**Answer**:

The parallels between the two cases are rather superficial.

In a method call expression, the compiler first needs to determine which method to call. This decision is based on the type of the receiver. The compiler builds a list of candidate receiver types, which include all types obtained by repeatedly derefencing the receiver, but also `&T` and `&mut T` for all types `T` encountered. This is the reason why you can call a method receiving `&mut self` directly as `x.foo()` instead of having to write `(&mut x).foo()`. For each type in the candidate list, the compiler then looks up inherent methods and methods on visible traits. See the [language reference](https://doc.rust-lang.org/1.26.1/reference/expressions/method-call-expr.html) for further details.

A deref coercion is rather different. It only occurs at a coercion site where the compiler exactly knows what type to expect. If the actual type encountered is different from the expected type, the compiler can use any coercion, including a deref coercion, to convert the actual type to the expected type. The list of possible coercions includes unsized coercions, pointer weakening and deref coercions. See the the [chapter on coercions in the Nomicon](https://doc.rust-lang.org/nomicon/coercions.html) for further details.

So these are really two quite different mechanisms – one for finding the right method, and one for converting types when it is already known what type exactly to expect. The first mechanism also automatically references the receiver, which can never happen in a coercion.

- I thought that a dereference does not always involve deref coercion, but I'm not sure: does dereferencing always use some Deref::deref trait implementation?

Not every dereferencing is a deref coercion. If you write `*x`, you explicitly dereference `x`. A deref coercion in contrast is performed implicitly by the compiler, and only in places where the compiler knows the expected type.

The [semantics of dereferencing](https://doc.rust-lang.org/reference/expressions/operator-expr.html#the-dereference-operator) depend on whether the type of `x` is a pointer type, i.e. a reference or a raw pointer, or not. For pointer types, `*x` denotes the object `x` points to, while for other types `*x` is equivalent to `*Deref::deref(&x)` (or the mutable anlogue of this).

- If so, is the implementor of `T: Deref<Target = U> where T: &U` built into the compiler?

I'm not quite sure what your syntax is supposed to mean – it's certainly not valid Rust syntax – but I guess you are asking whether derefencing an instance of `&T` to `T` is built into the compiler. As mentioned above, dereferencing of pointer types, including references, is built into the compiler, but there is also a [blanket implementation of Deref for &T](https://doc.rust-lang.org/nightly/src/core/ops/deref.rs.html#86-90) in the standard library. This blanket implementation is useful for generic code – the trait bound `T: Deref<Target = U>` otherwise wouldn't allow for `T = &U`.
