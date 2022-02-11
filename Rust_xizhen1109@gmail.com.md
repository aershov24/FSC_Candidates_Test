# Topic: Rust

**Author**: XuXiZhen

**Conact EMail**: xizhen1109@gmail.com

**QAs Total**: 4

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

## Q2: How do I create a `global`, `mutable singleton` in Rust?

**Difficulty:** `Mid`

**Source**:

https://stackoverflow.com/questions/27791532/how-do-i-create-a-global-mutable-singleton

**Answer**:

In the 3 following solutions:

- If you remove the [Mutex](https://doc.rust-lang.org/std/sync/struct.Mutex.html) then you have a global singleton without any mutability.
- You can also use a [RwLock](https://doc.rust-lang.org/std/sync/struct.RwLock.html) instead of a Mutex to allow multiple concurrent readers.

Using `lazy-static`:

The [`lazy-static`](https://crates.io/crates/lazy_static) crate can take away some of the drudgery of manually creating a singleton. Here is a global mutable vector:

```js
use lazy_static::lazy_static; // 1.4.0
use std::sync::Mutex;

lazy_static! {
    static ref ARRAY: Mutex<Vec<u8>> = Mutex::new(vec![]);
}

fn do_a_call() {
    ARRAY.lock().unwrap().push(1);
}

fn main() {
    do_a_call();
    do_a_call();
    do_a_call();

    println!("called {}", ARRAY.lock().unwrap().len());
}
```

Using `once_cell`:

The [`once_cell`](https://crates.io/crates/once_cell) crate can take away some of the drudgery of manually creating a singleton. Here is a global mutable vector:

```js
use once_cell::sync::Lazy; // 1.3.1
use std::sync::Mutex;

static ARRAY: Lazy<Mutex<Vec<u8>>> = Lazy::new(|| Mutex::new(vec![]));

fn do_a_call() {
    ARRAY.lock().unwrap().push(1);
}

fn main() {
    do_a_call();
    do_a_call();
    do_a_call();

    println!("called {}", ARRAY.lock().unwrap().len());
}
```

Using `std::sync::SyncLazy`:

The standard library is in the [`process`](https://github.com/rust-lang/rust/issues/74465) of adding `once_cell`'s functionality, currently called [`SyncLazy`](https://doc.rust-lang.org/nightly/std/lazy/struct.SyncLazy.html):

```js
#![feature(once_cell)] // 1.53.0-nightly (2021-04-01 d474075a8f28ae9a410e)
use std::{lazy::SyncLazy, sync::Mutex};

static ARRAY: SyncLazy<Mutex<Vec<u8>>> = SyncLazy::new(|| Mutex::new(vec![]));

fn do_a_call() {
    ARRAY.lock().unwrap().push(1);
}

fn main() {
    do_a_call();
    do_a_call();
    do_a_call();

    println!("called {}", ARRAY.lock().unwrap().len());
}
```

`A special case: atomics`:

If you only need to track an integer value, you can directly use an [`atomic`](https://doc.rust-lang.org/std/sync/atomic/):

```js
use std::sync::atomic::{AtomicUsize, Ordering};

static CALL_COUNT: AtomicUsize = AtomicUsize::new(0);

fn do_a_call() {
    CALL_COUNT.fetch_add(1, Ordering::SeqCst);
}

fn main() {
    do_a_call();
    do_a_call();
    do_a_call();

    println!("called {}", CALL_COUNT.load(Ordering::SeqCst));
}
```

`Manual, dependency-free implementation`:

There are several existing implementation of statics, such as [`the Rust 1.0 implementation of stdin`](https://github.com/rust-lang/rust/blob/2a8cb678e61e91c160d80794b5fdd723d0d4211c/src/libstd/io/stdio.rs#L217-L247). This is the same idea adapted to modern Rust, such as the use of `MaybeUninit` to avoid allocations and unnecessary indirection. You should also look at the modern implementation of [`io::Lazy`](https://github.com/rust-lang/rust/blob/1.42.0/src/libstd/io/lazy.rs). I've commented inline with what each line does.

```js
use std::sync::{Mutex, Once};
use std::time::Duration;
use std::{mem::MaybeUninit, thread};

struct SingletonReader {
    // Since we will be used in many threads, we need to protect
    // concurrent access
    inner: Mutex<u8>,
}

fn singleton() -> &'static SingletonReader {
    // Create an uninitialized static
    static mut SINGLETON: MaybeUninit<SingletonReader> = MaybeUninit::uninit();
    static ONCE: Once = Once::new();

    unsafe {
        ONCE.call_once(|| {
            // Make it
            let singleton = SingletonReader {
                inner: Mutex::new(0),
            };
            // Store it to the static var, i.e. initialize it
            SINGLETON.write(singleton);
        });

        // Now we give out a shared reference to the data, which is safe to use
        // concurrently.
        SINGLETON.assume_init_ref()
    }
}

fn main() {
    // Let's use the singleton in a few threads
    let threads: Vec<_> = (0..10)
        .map(|i| {
            thread::spawn(move || {
                thread::sleep(Duration::from_millis(i * 10));
                let s = singleton();
                let mut data = s.inner.lock().unwrap();
                *data = i as u8;
            })
        })
        .collect();

    // And let's check the singleton every so often
    for _ in 0u8..20 {
        thread::sleep(Duration::from_millis(5));

        let s = singleton();
        let data = s.inner.lock().unwrap();
        println!("It is: {}", *data);
    }

    for thread in threads.into_iter() {
        thread.join().unwrap();
    }
}
```
`The meaning of "global"`:

Please note that you can still use normal Rust scoping and module-level privacy to control access to a `static` or `lazy_static` variable. This means that you can declare it in a module or even inside of a function and it won't be accessible outside of that module / function. This is good for controlling access:

```js
use lazy_static::lazy_static; // 1.2.0

fn only_here() {
    lazy_static! {
        static ref NAME: String = String::from("hello, world!");
    }
    
    println!("{}", &*NAME);
}

fn not_here() {
    println!("{}", &*NAME);
}
```

However, the variable is still global in that there's one instance of it that exists across the entire program.

---

## Q3: Is there any way to get unstable features on the compiler versions in stable or beta??

**Difficulty:** `Mid`

**Source**:

https://stackoverflow.com/questions/34430429/is-there-any-way-to-get-unstable-features-on-the-compiler-versions-in-stable-or

**Answer**:

You cannot (trivially) compile any stable version of Rust to use unstable features. Nor can you download the stable version as if it were unstable. However, Rust's downloads has a set of archives.

By checking when the most recent release happened:

![](https://i.stack.imgur.com/dJfYk.png)

I could figure out what day the current Beta was technically a Nightly. Now, presuming there wasn't a major bugfix between the previous Nightly and Beta releases of 1.6, I went to the folder (in this case, December 9, 2015) and downloaded the corresponding Nightly installer from the list.

There are folders going back to 2014-11-07, so if you need a specific version of Rust from the past to compile your code, you can likely find it there.

---

## Q4: What is the relation between `auto-dereferencing` and `deref` coercion?

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
