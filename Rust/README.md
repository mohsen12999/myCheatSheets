# Rust

## Refrences

* [A Gentle Introduction To Rust](https://stevedonovan.github.io/rust-gentle-intro/readme.html)

## install

* [install rustup](https://www.rust-lang.org/tools/install)
 
```sh
curl https://sh.rustup.rs -sSf | sh
rustup component add rust-docs
```

* after install, need ad to path `$HOME/.cargo/bin` in `.bashrc`
 
* `rustup update` to upgrade
* `rustup doc` will open the offline documentation
* for compile and run `rustc $1.rs && ./$1`

* build your project with `cargo build`
* run your project with `cargo run`
* test your project with `cargo test`
* build documentation for your project with `cargo doc`
* publish a library to `crates.io` with `cargo publish`

* Generating a new project `cargo new hello-rust` and `cargo run`

## Basic

```rs
fn main() {
    println!("Hello, World!");
}
```

* The exclamation mark indicates that this is a macro call.

```rs
fn main() {
    let answer = 42;
    println!("Hello {}", answer);
}
```

* `assert_eq!` This is the workhorse of testing in Rust; you assert that two things must be equal, and if not, panic.

## Looping and Ifing

```rs
fn main() {
    for i in 0..5 {
        println!("Hello {}", i);
    }
}
```

```rs
fn main() {
    for i in 0..5 {
        if i % 2 == 0 {
            println!("even {}", i);
        } else {
            println!("odd {}", i);
        }
    }
}
```

```rs
fn main() {
    for i in 0..5 {
        let even_odd = if i % 2 == 0 {"even"} else {"odd"};
        println!("{} {}", even_odd, i);
    }
}
```

## Adding Things Up

* `let` variables by default can only be assigned a value when declared. Adding the magic word `mut`

```rs
fn main() {
    let mut sum = 0;
    for i in 0..5 {
        sum += i;
    }
    println!("sum is {}", sum);
}
```

```rs
fn main() {
    let bigint: i64 = 0; // explicit
    let mut sum = 0.0; // implicit float
    for i in 0..5 {
        sum += i as f64; //cast type
    }
    println!("sum is {}", sum);
}
```

* see online [Primitive Types](https://doc.rust-lang.org/std/index.html#primitives) or see offline with: `rustup doc --std`

## Function Types are Explicit

```rs
fn sqr(x: f64) -> f64 {
    return x * x;
}

fn main() {
    let res = sqr(2.0);
    println!("square is {}", res);
}
```

```rs
// absolute value of a floating-point number
fn abs(x: f64) -> f64 {
    if x > 0.0 {
        x
    } else {
        -x
    }
}

// ensure the number always falls in the given range
fn clamp(x: f64, x1: f64, x2: f64) -> f64 {
    if x < x1 {
        x1
    } else if x > x2 {
        x2
    } else {
        x
    }
}

fn factorial(n: u64) -> u64 {
    if n == 0 {
        1
    } else {
        n * factorial(n-1)
    }
}
```

* It's not wrong to use `return`, but code is cleaner without it. You will still use `return` for returning early from a function.
* A reference is created by `&` and dereferenced by `*`.

```rs
fn by_ref(x: &i32) -> i32{
    *x + 1
}

fn main() {
    let i = 10;
    let res1 = by_ref(&i);
    let res2 = by_ref(&41);
    println!("{} {}", res1,res2);
}
```

* to modify one of its arguments

```rs
fn modifies(x: &mut f64) {
    *x = 1.0;
}

fn main() {
    let mut res = 0.0;
    modifies(&mut res);
    println!("res is {}", res);
}
```

## Learning Where to Find the Ropes

* offline search `rustup doc --std`, and can search in search span on top

```rs
let pi: f64 = 3.1416;
let x = pi/2.0;
let cosine = x.cos();
```

```
fn main() {
    let x = 2.0 * std::f64::consts::PI;
    let abs_difference = (x.cos() - 1.0).abs();
    assert!(abs_difference < 1e-10); // cousin of assert_eq!
}
```

```rs
use std::f64::consts;

fn main() {
    let x = 2.0 * consts::PI;
    let abs_difference = (x.cos() - 1.0).abs();
    assert!(abs_difference < 1e-10);
}
```

## Arrays and Slices

```rs
fn main() {
    let arr = [10, 20, 30, 40];
    let first = arr[0];
    println!("first {}", first);

    for i in 0..4 {
        println!("[{}] = {}", i,arr[i]);
    }
    println!("length {}", arr.len());
}
```

*  type of an array includes its size, like [&i32; 4]

```rs
// read as: slice of i32
fn sum(values: &[i32]) -> i32 {
    let mut res = 0;
    for i in 0..values.len() {
        res += values[i]
    }
    res
}

fn main() {
    let arr = [10,20,30,40];
    // send array as slice
    let res = sum(&arr);
    println!("sum {}", res);
}
```

* A C programmer pronounces & as 'address of'; a Rust programmer pronounces it 'borrow'.

## Slicing and Dicing

```rs
fn main() {
    let ints = [1, 2, 3];
    let floats = [1.1, 2.1, 3.1];
    let strings = ["hello", "world"];
    let ints_ints = [[1, 2], [10, 20]]; // array of array
    println!("ints {:?}", ints);
    println!("floats {:?}", floats);
    println!("strings {:?}", strings);
    println!("ints_ints {:?}", ints_ints);
}
```

* make slice of array

```rs
fn main() {
    let ints = [1, 2, 3, 4, 5];
    let slice1 = &ints[0..2];
    let slice2 = &ints[1..];  // open range!

    println!("ints {:?}", ints);
    println!("slice1 {:?}", slice1);
    println!("slice2 {:?}", slice2);
}
```
## Optional Values

* Slices, like arrays, can be indexed. Rust knows the size of an array at compile-time, but the size of a slice is only known at run-time. So s[i] can cause an out-of-bounds error when running and will panic. -> use `get`

```rs
fn main() {
    let ints = [1, 2, 3, 4, 5];
    let slice = &ints;
    let first = slice.get(0);
    let last = slice.get(5);

    println!("first {:?}", first);
    println!("last {:?}", last);
}
// first Some(1)
// last None
```

```rs
    println!("first {} {}", first.is_some(), first.is_none());
    println!("last {} {}", last.is_some(), last.is_none());
    println!("first value {}", first.unwrap());

// first true false
// last false true
// first value 1

    let maybe_last = slice.get(5);
    let last = if maybe_last.is_some() {
        *maybe_last.unwrap()
    } else {
        -1
    };
```

* Note the `*` - the precise type inside the `Some` is `&i32`, which is a reference. We need to dereference this to get back to a `i32` value.

```rs
    let last = *slice.get(5).unwrap_or(&-1);
```

* You can think of Option as a box which may contain a value, or nothing (None).
* It is very common for Rust functions/methods to return such maybe-boxes. [option](https://doc.rust-lang.org/std/option/enum.Option.html)

## Vectors

* `vec` re-sizeable arrays

```rs
fn main() {
    let mut v = Vec::new();
    v.push(10);
    v.push(20);
    v.push(30);

    let first = v[0];  // will panic if out-of-range
    let maybe_first = v.get(0);

    println!("v is {:?}", v);
    println!("first is {}", first);
    println!("maybe_first is {:?}", maybe_first);
}
// v is [10, 20, 30]
// first is 10
// maybe_first is Some(10)
```

```rs
fn dump(arr: &[i32]) {
    println!("arr is {:?}", arr);
}

fn main() {
    let mut v = Vec::new();
    v.push(10);
    v.push(20);
    v.push(30);

    dump(&v);

    let slice = &v[1..];
    println!("slice is {:?}", slice);
}
```

## Iterators

```rs
fn main() {
    let mut iter = 0..3;
    assert_eq!(iter.next(), Some(0));
    assert_eq!(iter.next(), Some(1));
    assert_eq!(iter.next(), Some(2));
    assert_eq!(iter.next(), None);
}
```

```rs
fn main() {
    let arr = [10, 20, 30];
    for i in arr.iter() {
        println!("{}", i);
    }

    // slices will be converted implicitly to iterators...
    let slice = &arr;
    for i in slice {
        println!("{}", i);
    }
}
```

```rs
fn main() {
    let sum: i32  = (0..5).sum();
    println!("sum was {}", sum);

    let sum: i64 = [10, 20, 30].iter().sum();
    println!("sum was {}", sum);
}
```

* The `windows` method gives you an iterator of slices - overlapping windows of values Or `chunks`:

```rs
fn main() {
    let ints = [1, 2, 3, 4, 5];
    let slice = &ints;

    for s in slice.windows(2) {
        println!("window {:?}", s);
    }
// window [1, 2]
// window [2, 3]
// window [3, 4]
// window [4, 5]

    for s in slice.chunks(2) {
        println!("chunks {:?}", s);
    }
// chunks [1, 2]
// chunks [3, 4]
// chunks [5]
}

```


https://stevedonovan.github.io/rust-gentle-intro/1-basics.html#more-about-vectors
