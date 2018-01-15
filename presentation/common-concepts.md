
## Common Concepts

* Variables
* Data Types
* Functions
* Control Flow

--

### Variables

* ```Immutable``` by default
* Use ```mut``` keyword for mutable variables

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
    In Rust variable are immutable by default, so we call them Variable bindings. To make them mutable, mut keyword is used.
    Rust is a statically typed language; It checks data type at compile time. But it doesn’t require you to actually type it when declare variable bindings.
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

![triomphe](../../images/triomphe.png) <!-- .element: class="borderless medium" -->

--

### Exo 1
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Variables</a>

```rust
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


























// Hint: The declaration on line 4 is missing a keyword that is needed in Rust
// to create a new variable binding.
// Rust requires that all parts of a function's signature have type annotations,
// there's something wrong with the place where we're calling the function.
```
<!-- .element: class="playground" -->


--

### Exo 2
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a>
```rust
// Make me compile! Scroll down for hints :)

fn main() {
    num = 3;
    call_me();
}

fn call_me(num) {
    for i in 0..num {
        println!("Ring! Call number {}", i + 1);
    }
}


























// Hint: The declaration on line 4 is missing a keyword that is needed in Rust
// to create a new variable binding.
// Rust requires that all parts of a function's signature have type annotations,
// there's something wrong with the place where we're calling the function.
```
<!-- .element: class="playground" -->

--

### Exo 3
<a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a>

```rust
// Make me compile! Scroll down for hints :)

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



















// 1) The error message points to line 11 and says it expects a type after the
// `->`. This is where the function's return type should be-- take a look at
// the `is_even` function for an example!
//
// 2) a really common error that can be fixed by removing one character.
// It happens because Rust distinguishes between expressions and statements: expressions return
// a value and statements don't. We want to return a value from the `square` function, but it
// isn't returning one right now...
```
<!-- .element: class="playground" -->

