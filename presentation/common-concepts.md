
## Common Concepts

* Variables
* Data Types
* Functions
* Control Flow

--

### Variables

* **Immutable** by default <!-- .element: class="beige" -->
* Use **mut** keyword for mutable variables <!-- .element: class="beige" -->
* **Snake case** naming convention <!-- .element: class="beige" -->


```rust
fn main() {
    let mut child_age = 5;
    println!("The value of child_age is: {}", child_age);
    child_age = 6;
    println!("The value of child_age is: {}", child_age);
}
``` 
<!-- .element: class="fragment" data-fragment-index="2" --> 

Note:
- In Rust variable are immutable by default, so we call them **Variable bindings**. To make them mutable, mut keyword is used.
- Immutable variables encourages you to write your code in a way that takes advantage of the safety and easy concurrency that Rust offers.

--

### Data types

* **Statically typed** language <!-- .element: class="beige" -->
* Powerful **type inference** <!-- .element: class="beige" -->

Note:
- Rust is a statically typed language => It checks data type at compile time.
- But it doesn’t require you to actually type it when declare variable bindings.

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

```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x);
}
```

Note:
- the ```main``` function => entry point of many programs 
- ```fn``` keyword => declare new functions
- In function signatures, you **must** declare the type of each parameter => deliberate decision

--

## Functions 
Return value <!-- .element: class="beige" -->

```rust
fn main() {
    println!("The eval of plus_one(5) is: {}", plus_one(5));
    println!("The eval of plus(5, 2) is: {}", plus(5, 2));
}

fn plus_one(x: i32) -> i32 {
    return x + 1;
}

// or
fn plus(x: i32, y: i32) -> i32 {
    x + y
}
```

Note:
- we **must** declare the function return types after an arrow (->)
- to return a value we can use ether ```return``` keyword or un expression with no semicolon (last value in the bloc).

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
<!-- .element: class="fragment" data-fragment-index="2" --> 


Note:
- You can of cause use multiples ```if else if``` conditions
- No ternary operation, but ```let if``` instead 

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

```rust
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 { break counter * 2; }
};
println!("Result is: {}", result);
```
<!-- .element: class="fragment" data-fragment-index="2" --> 

Note:
- ```break``` with return value

--

## Exercises

![triomphe](https://xebia-france.github.io/xke-rs/images/triomphe.png) <!-- .element: class="borderless medium" -->

--

### Exo 1

<div><a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Variables</a></div>
<!-- .element: class="small" -->

```rust
// Make me compile! Scroll down for hints :)

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

<div><a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a></div>
<!-- .element: class="small" -->

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

<div><a href="https://doc.rust-lang.org/book/second-edition/ch03-01-variables-and-mutability.html" target="_blank">Functions</a></div>
<!-- .element: class="small" -->

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

--

### Exo 4

<div><a href="https://doc.rust-lang.org/book/second-edition/ch03-05-control-flow.html" target="_blank">Control Flow</a></div>
<!-- .element: class="small" -->

```rust
pub fn bigger(a: i32, b:i32) -> i32 {
    // Complete this function to return the bigger number!
    // Do not use:
    // - return
    // - another function call
    // - additional variables
    // Scroll down for hints.
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn ten_is_bigger_than_eight() {
        assert_eq!(10, bigger(10, 8));
    }

    #[test]
    fn fortytwo_is_bigger_than_thirtytwo() {
        assert_eq!(42, bigger(32, 42));
    }
}

























// It's possible to do this in one line if you would like!
// Some similar examples from other languages:
// - In C(++) this would be: `a > b ? a : b`
// - In Python this would be:  `a if a > b else b`
// Remember in Rust that:
// - the `if` condition does not need to be surrounded by parentheses
// - `if`/`else` conditionals are expressions
// - Each condition is followed by a `{}` block.
```
<!-- .element: class="playground" -->

