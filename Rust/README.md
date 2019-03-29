# Rust

## Refrences

* [A Gentle Introduction To Rust](https://stevedonovan.github.io/rust-gentle-intro/readme.html)

## install

* [install rustup](https://www.rust-lang.org/tools/install)
 
```sh
curl https://sh.rustup.rs -sSf | sh
rustup component add rust-docs
```

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




