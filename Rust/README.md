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

## More about vectors

* `vec!` for initializing a vector.
* `push` and `pop` for add and remove value to end of vector. `insert`, `remove`, `clear`, `clone`, `sort`, `dedup`

```rs
fn main() {
    let mut v1 = vec![10, 20, 30, 40];
    v1.pop();

    let mut v2 = Vec::new();
    v2.push(10);
    v2.push(20);
    v2.push(30);

    assert_eq!(v1, v2);

    v2.extend(0..2);
    assert_eq!(v2, &[10, 20, 30, 0, 1]);
}
```

```rs
fn main() {
    let mut v1 = vec![1, 10, 5, 1, 2, 11, 2, 40];
    v1.sort();
    v1.dedup(); // remove duplicate
    assert_eq!(v1, &[1, 2, 5, 10, 11, 40]);
}
```

## Strings

```rs
fn dump(s: &str) {
    println!("str '{}'", s);
}

fn main() {
    let text = "hello dolly";  // the string slice
    let s = text.to_string();  // it's now an allocated string

    dump(text);
    dump(&s);
}
```

* `String` is basically a `Vec<u8>` and `&str` is `&[u8]`, but those bytes must represent valid UTF-8 text.



```rs
fn main() {
    let mut s = String::new();
    // initially empty!
    s.push('H');
    s.push_str("ello");
    s.push(' ');
    s += "World!"; // short for `push_str`
    // remove the last char
    s.pop();

    assert_eq!(s, "Hello World");
}
```

* You can convert many types to strings using `to_string`

```rs
fn array_to_str(arr: &[i32]) -> String {
    let mut res = '['.to_string();
    for v in arr {
        res += &v.to_string();
        res.push(',');
    }
    res.pop();
    res.push(']');
    res
}

fn main() {
    let arr = array_to_str(&[10, 20, 30]);
    let res = format!("hello {}", arr);

    assert_eq!(res, "hello [10,20,30]");
}
```

* slices works with strings

```rs
fn main() {
    let text = "static";
    let string = "dynamic".to_string();

    let text_s = &text[1..];
    let string_s = &string[2..4];

    println!("slices {:?} {:?}", text_s, string_s);
}
// slices "tatic" "na"
```

* cannot index strings! This is because they use the One True Encoding, UTF-8, where a 'character' may be a number of bytes.

```rs
fn main() {
    let multilingual = "Hi! ¡Hola! привет!";
    for ch in multilingual.chars() {
        print!("'{}' ", ch);
    }
    println!("");
    println!("len {}", multilingual.len());
    println!("count {}", multilingual.chars().count());

    let maybe = multilingual.find('п');
    if maybe.is_some() {
        let hi = &multilingual[maybe.unwrap()..];
        println!("Russian hi {}", hi);
    }
}
// 'H' 'i' '!' ' ' '¡' 'H' 'o' 'l' 'a' '!' ' ' 'п' 'р' 'и' 'в' 'е' 'т' '!'
// len 25
// count 18
// Russian hi привет!
```

* The Rust `char` type is a 4-byte Unicode code point. Strings are not arrays of chars!
* The string `split_whitespace` method returns an iterator

```rs
    let s = "¡";
    println!("{}", &s[0..1]); <-- bad, first byte of a multibyte character

    let mut words = Vec::new();
    words.extend(text.split_whitespace());

    let stripped: String = text.chars()
        .filter(|ch| ! ch.is_whitespace()).collect();
    // theredfoxandthelazydog
```

* The `filter` method takes a closure, which is Rust-speak for lambdas or anonymous functions. 

## Interlude: Getting Command Line Arguments

```rs
fn main() {
    for arg in std::env::args() {
        println!("'{}'", arg);
    }
}
// src$ rustc args0.rs
// src$ ./args0 42 'hello dolly' frodo
// './args0'
// '42'
// 'hello dolly'
// 'frodo'
```

* Would it have been better to return a Vec? It's easy enough to use collect to make that vector, using the iterator skip method to move past the program name.

```rs
    let args: Vec<String> = std::env::args().skip(1).collect();
    if args.len() > 0 { // we have args!
        ...
    }
```

```rs
use std::env;

fn main() {
    let first = env::args().nth(1).expect("please supply an argument");
    let n: i32 = first.parse().expect("not an integer!");
    // do your magic
}
```

* `nth(1)` gives you the second value of the iterator, and `expect` is like an `unwrap` with a readable message.

## Matching

```rs
    // let multilingual = "Hi! ¡Hola! привет!";
    match multilingual.find('п') {
        Some(idx) => {
            let hi = &multilingual[idx..];
            println!("Russian hi {}", hi);
        },
        None => println!("couldn't find the greeting, Товарищ")
    };
```

* `match` consists of several patterns with a matching value following the fat arrow, separated by commas. It has conveniently unwrapped the value from the `Option` and bound it to `idx`. You must specify all the possibilities, so we have to handle `None`.

```rs
    // not interested in failure 
    if let Some(idx) = multilingual.find('п') {
        println!("Russian hi {}", &multilingual[idx..]);
    }
```

```rs
    let text = match n {
        0 => "zero",
        1 => "one",
        2 => "two",
        _ => "many",
    };

    let text = match n {
        0...3 => "small",
        4...6 => "medium",
        _ => "large",
     };
```

## Reading from Files

```rs
use std::env;
use std::fs::File;
use std::io::Read;

fn main() {
    let first = env::args().nth(1).expect("please supply a filename");

    let mut file = File::open(&first).expect("can't open the file");

    let mut text = String::new();
    file.read_to_string(&mut text).expect("can't read the file");

    println!("file had {} bytes", text.len());

}
// file1 file1.rs
```

* `read_to_end` put the contents into a vector of bytes.
* `Result` is defined by two type parameters, for the `Ok` value and the `Err` value 

```rs
fn good_or_bad(good: bool) -> Result<i32,String> {
    if good {
        Ok(42)
    } else {
        Err("bad".to_string())
    }
}

fn main() {
    println!("{:?}",good_or_bad(true));
    //Ok(42)
    println!("{:?}",good_or_bad(false));
    //Err("bad")

    match good_or_bad(true) {
        Ok(n) => println!("Cool, I got {}",n),
        Err(e) => println!("Huh, I just got {}",e)
    }
    // Cool, I got 42

}
```

* This version of the file reading function does not crash. It returns a `Result` and it is the caller who must decide how to handle the error.

```rs
use std::env;
use std::fs::File;
use std::io::Read;
use std::io;

fn read_to_string(filename: &str) -> Result<String,io::Error> {
    let mut file = match File::open(&filename) {
        Ok(f) => f,
        Err(e) => return Err(e),
    };
    let mut text = String::new();
    match file.read_to_string(&mut text) {
        Ok(_) => Ok(text),
        Err(e) => Err(e),
    }
}

fn main() {
    let file = env::args().nth(1).expect("please supply a filename");

    let text = read_to_string(&file).expect("bad file man!");

    println!("file had {} bytes", text.len());
}
```

* The `std::io` module defines a type alias `io::Result<T>` which is exactly the same as `Result<T,io::Error>` and easier to type.

```rs
fn read_to_string(filename: &str) -> io::Result<String> {
    let mut file = File::open(&filename)?;
    let mut text = String::new();
    file.read_to_string(&mut text)?;
    Ok(text)
}

// or

fn read_to_string(filename: &str) -> io::Result<String> {
    let mut file = try!(File::open(&filename));
    let mut text = String::new();
    try!(file.read_to_string(&mut text));
    Ok(text)
}
```

## Rust likes to Move It, Move It

```rs
fn dump(s: String) {
    println!("{}", s);
}

fn main() {
    let s1 = "hello dolly".to_string();
    dump(s1);
    println!("s1 {}", s1); // <---error: 'value used here after move'
}
```

```rs
fn dump(s: &String) { // String reference
    println!("{}", s);
}

fn dump(s: &str) { // best way
    println!("{}", s);
}

```

## Scope of Variables

```rs
{
    let a = 10;
    let b = "hello";
    {
        let c = "hello".to_string();
        // a,b and c are visible
    }
    // the string c is dropped
    // a,b are visible
    for i in 0..a {
        let b = &b[1..];
        // original b is no longer visible - it is shadowed.
    }
    // the slice b is dropped
    // i is _not_ visible!
}
```

```rs
fn main() {
    let s1 = "hello dolly".to_string();
    let mut rs1 = &s1;
    {
        let tmp = "hello world".to_string();
        rs1 = &tmp;
    }
    println!("ref {}", rs1); <---error:`tmp` does not live long enough
}
```

* We borrow the value of `s1` and then borrow the value of `tmp`. But `tmp`'s value does not exist outside that block!

## Tuples

* very useful to return multiple values from a function

```rs
// tuple1.rs

fn add_mul(x: f64, y: f64) -> (f64,f64) {
    (x + y, x * y)
}

fn main() {
    let t = add_mul(2.0,10.0);

    // can debug print
    println!("t {:?}", t);

    // can 'index' the values
    println!("add {} mul {}", t.0,t.1);

    // can _extract_ values
    let (add,mul) = t;
    println!("add {} mul {}", add,mul);
}
// t (12, 20)
// add 12 mul 20
// add 12 mul 20
```

```rs
let tuple = ("hello", 5, 'c');

assert_eq!(tuple.0, "hello");
assert_eq!(tuple.1, 5);
assert_eq!(tuple.2, 'c');

    for t in ["zero","one","two"].iter().enumerate() {
        print!(" {} {};",t.0,t.1);
    }
    //  0 zero; 1 one; 2 two;
```

* `zip` combines two iterators into a single iterator of tuples

```rs
    let names = ["ten","hundred","thousand"];
    let nums = [10,100,1000];
    for p in names.iter().zip(nums.iter()) {
        print!(" {} {};", p.0,p.1);
    }
    //  ten 10; hundred 100; thousand 1000;
```

## Structs

```rs
struct Person {
    first_name: String,
    last_name: String
}

fn main() {
    let p = Person {
        first_name: "John".to_string(),
        last_name: "Smith".to_string()
    };
    println!("person {} {}", p.first_name,p.last_name);
}
```

```rs
struct Person {
    first_name: String,
    last_name: String
}

impl Person {

    fn new(first: &str, name: &str) -> Person {
        Person {
            first_name: first.to_string(),
            last_name: name.to_string()
        }
    }

    fn full_name(&self) -> String {
        format!("{} {}", self.first_name, self.last_name)
    }
}

fn main() {
    let p = Person::new("John","Smith");
    println!("person {} {}", p.first_name,p.last_name);
    println!("fullname {}", p.full_name());
}
```

* The keyword `Self` refers to the struct type.

```rs
    fn copy(&self) -> Self {
        Self::new(&self.first_name,&self.last_name)
    }

    fn set_first_name(&mut self, name: &str) {
        self.first_name = name.to_string();
    }

    fn to_tuple(self) -> (String,String) {
        (self.first_name, self.last_name)
    }
```

* The directive makes the compiler generate a `Debug` implementation, which is very helpful.

```rs
use std::fmt;

#[derive(Debug)]
struct Person {
    first_name: String,
    last_name: String
}

impl Person {

    fn new(first: &str, name: &str) -> Person {
        Person {
            first_name: first.to_string(),
            last_name: name.to_string()
        }
    }

    fn full_name(&self) -> String {
        format!("{} {}",self.first_name, self.last_name)
    }

    fn set_first_name(&mut self, name: &str) {
        self.first_name = name.to_string();
    }

    fn to_tuple(self) -> (String,String) {
        (self.first_name, self.last_name)
    }
}

fn main() {
    let mut p = Person::new("John","Smith");

    println!("{:?}", p);

    p.set_first_name("Jane");

    println!("{:?}", p);

    println!("{:?}", p.to_tuple());
    // p has now moved.

}
// Person { first_name: "John", last_name: "Smith" }
// Person { first_name: "Jane", last_name: "Smith" }
// ("Jane", "Smith")
```

## Lifetimes Start to Bite


https://stevedonovan.github.io/rust-gentle-intro/2-structs-enums-lifetimes.html#lifetimes-start-to-bite


