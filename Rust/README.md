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




















