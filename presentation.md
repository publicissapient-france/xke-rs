<!-- .slide: data-background="#2C374C" -->

## xke-rs <!-- .element: class="grisFonce2" -->
For those who didn't had time to install rust.
```
curl https://sh.rustup.rs -sSf | sh
```

Note:
    This is the speaker notes

---

# Rust

**From hero to zero** <!-- .element: class="grisFonce2" -->

---

### Hands On

Organization:
1. Language presentation
2. Exercises
3. Questions

--

Animators:
* PODYACHIY Dimitry
* PETIT Jean-Baptiste

---

### What is rust ?
* Programing language
* GC less
* Low level
* Abstractions (iterators, closure, types...)
* Version 1 in may 2015
* In production in mozilla, Atlassian, npm, clever cloud, dropbox...

---

Why rust instead of go ? (or the differences between Rust and Go).

||Rust|Go|
|---|---|---|
|Runtime|[lightweight](https://www.rust-lang.org/en-US/faq.html#does-rust-have-a-runtime)|[pretty big](https://www.quora.com/How-does-the-Go-runtime-work-What-does-it-consist-of-What-functionalities-does-it-provide-and-what-can-be-expected-from-a-developer-perspective)|
|GC|no|yes|
|Types|strong|soft|
|LC|hard|easy|
|Goal|replace C ([a safe, modern and fearless concurrent C](https://www.rust-lang.org/en-US/faq.html#what-is-this-projects-goal))|[tool with fast compilation time and easy concurrency](https://talks.golang.org/2012/splash.article)|

--

They are not on the same field. Rust isn't better than Go. Go isn't better than rust.

--

But, why docker has choose Go if it wasn't a C replacement ?? Because [various](https://fr.slideshare.net/jpetazzo/docker-and-go-why-did-we-decide-to-write-docker-in-go/18-Why_GoThe_Five_Reasons_Why) reasons but none of them is: Go is a drop in replacement to C/C++).

---

Why would we learn Rust ? Why it would be nice to know rust in Xebia ?
* Learn Rust, increase your computer comprehension.
* IOT guys, rust is for you.
* Rust is growing.
* Wanna: true performance && security && low memory usage && memory predictability, for a new project ?

---

## Cargo

The Rust package manager <!-- .element: class="beige" -->

--

### Cargo

* Bootstrap a project
* Build code
* Manage dependencies

--


Bootstrap

```bash
$ cargo new hello_cargo --bin
$ cd hello_cargo
$ tree .
.
├─ Cargo.toml
└─ src
    └─ main.rs
```

Build / run

```bash
$ cargo run
```

--

## Exercises

![triomphe](images/triomphe.png) <!-- .element: class="borderless medium" -->

--

1. Create a new project with cargo
2. Execute it
3. Try to change ```src/main.rs``` 

```rust
// from
println!("Hello, world!");
// to 
println("Hello, world!");
```

and build it   

---

## Common Concepts

* Variables
* Data Types
* Functions
* Control Flow

--

### Variables

* **Immutable** by default <!-- .element: class="beige" -->
* Add ```mut``` keyword for mutable variables

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
``` 
<!-- .element: class="fragment" data-fragment-index="2" --> 

Note:
    Immutable variables encourages you to write your code in a way that takes advantage of the safety and easy concurrency that Rust offers.

--

### Data types

* **Statically typed** language <!-- .element: class="beige" -->
* Powerful **type inference** <!-- .element: class="beige" -->

Note:
    Rust is a statically typed language, which means that it must know the types of all variables at compile time

--

Some examples 

```rust
let foo: i16 = 1001; // integer 16 bits
let mut bar: f32; // float 32 bits
let sum = 32 + 64; // inference
let b: bool = true;
let z = 'ℤ'; // char UTF8
```

Some more examples
<!-- .element: class="fragment" data-fragment-index="2" --> 

```rust
// Tuples
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
let first = tup.0;

// Arrays
let arr = [1, 2, 3, 4, 5];
let second = arr[1];

// Type is mandatory here
let guess: u32 = "42".parse().expect("Not a number!");
```
<!-- .element: class="fragment" data-fragment-index="2" -->
 
--

## Functions

**Snake case** naming convention <!-- .element: class="beige" -->

```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x);
}
```

--

## Functions 
Return value <!-- .element: class="beige" -->

```rust
fn main() {
    println!("The value of x is: {}", plus_one(5));
}

fn plus_one(x: i32) -> i32 {
    x + 1
}

// or
fn plus_two(x: i32) -> i32 {
    return x + 2;
}
```

--

### Control Flow
Conditionals <!-- .element: class="beige" -->

```rust
// IF
let number = 6;
if number % 4 == 0 {
    println!("number is divisible by 4");
} else {
    println!("number is not divisible by 4");
}
```

```rust
// LET IF
let condition = true;
let number = if condition { 5 } else { 6 };
println!("The value of number is: {}", number);
```

--

### Control Flow
Loops <!-- .element: class="beige" -->

```rust
let mut number = 3;
while number != 0 {
    println!("{}!", number);
    number = number - 1;
}
```

```rust
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("the value is: {}", element);
}
```

--

## Exercises

![triomphe](images/triomphe.png) <!-- .element: class="borderless medium" -->

--

### Exo 1
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Variables</a>

    // Make me compile!

    fn main() {
        let x;
        if x == 10 {
            println!("Ten!");
        } else {
            println!("Not ten!");
        }
        x = 5;
        println!("x is now {}", x);
    }
    
    
<a href="https://play.rust-lang.org/?gist=088ab0244adcd11389016c52066cf63a&version=stable" target="_blank">Playground</a> <!-- .element: class="playground" -->


--

### Exo 2
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a>

    // Make me compile!
    
    fn main() {
        num = 3;
        call_me();
    }
    
    fn call_me(num) {
        for i in 0..num {
            println!("Ring! Call number {}", i + 1);
        }
    }

<a href="https://play.rust-lang.org/?gist=d2fa03b272a7aef268c6dd4c30013622&version=stable" target="_blank">Playground</a> <!-- .element: class="playground" -->

--

### Exo 3
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a>

    // Make me compile!    
    // This store is having a sale where if the price is an even number, you get
    // 10 (money unit) off, but if it's an odd number, it's 3 (money unit) less.

    fn main() {
        let original_price = 51;
        println!("Your sale price is {}", sale_price(original_price));
    }
    
    fn sale_price(price: i32) -> {
        if is_even(price) {
            price - 10
        } else {
            price - 3
        }
    }
    
    fn is_even(num: i32) -> bool {
        num % 2 == 0;
    }


<a href="https://play.rust-lang.org/?gist=9de544d47e2d2ce0ea04df2c328fa2c8&version=stable" target="_blank">Playground</a> <!-- .element: class="playground" -->

---

## Functional Programming
Is possible in rust <!-- .element: class="beige" -->

--
