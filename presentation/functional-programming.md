## Functional Programming

--

### Optional

* There is no ```null``` / ```nill``` (or ```undefined```).
* Use ````Some```` for presence and ```None``` for absence.

```rust
fn main() {
    let some_number = Some(5);
    let absent_number: Option<i32> = None;
}
``` 

--

### Pattern matching

* Use ````match```` to compare a value against series of pattern.

```rust
enum Game {
    Dota,
    LoL,
    HotS,
    HoN
}
fn game_to_awesomeness(game : Game) -> String {
    match game {
        Game::Dota => String::from("Awesome"),
        Game::LoL => String::from("Dota for kids."),
        Game::HotS => String::from("Pay to win Dota."),
        Game::HoN => String::from("Dota without money."),
    }
}
``` 

--

### Closure

* Use pipe to write a closure

```Rust
let add = |x: i32, y: i32| x + y;
let result = add(5, 5);

println!("{}", result);
```

--

### Iterator

* Java 8 streams like

```Rust
let years = vec!(2015, 2016, 2017, 2018);
let incremented_years: Vec<i32> = years.iter()
    .map(|y| y + 1)
    .collect();

println!("{:?}", incremented_years);
```

--

![triomphe](https://xebia-france.github.io/xke-rs/images/triomphe.png) <!-- .element: class="borderless medium" -->

--

### Exo 1

````rust
// Make me run without error by using Some, None.
// Change only function checked_division.
fn main() {
    let result = checked_division(12, 0);
    println!("{:?} option of something or None when nothing", result)
}

fn checked_division(dividend: i32, divisor: i32) -> Option<i32> {
    dividend / divisor
}

````
<!-- .element: class="playground" -->

--

### Exo 2

<div><a href="https://doc.rust-lang.org/book/second-edition/ch06-03-if-let.html" target="_blank">If let</a></div>

````rust
// Make me compile by using Some, None.
fn main() {
    let maybe_seven = Some(7);
    
    if let 7 = maybe_seven {
        println!("Success")
    }
}

````
<!-- .element: class="playground" -->

--

### Exo 3

<div><a href="https://doc.rust-lang.org/book/first-edition/patterns.html#guards" target="_blank">Pattern matching</a></div>

````rust
// Print "Success" when x plus y is equal to 0.
fn main() {
    let pair = (2, -42);

    match pair {
         => println!("Success"), // Change here
        (x, y) => println!("x: {}, y: {}", x, y),
    }
}
````
<!-- .element: class="playground" -->

--

### Exo 4

<div><a href="https://doc.rust-lang.org/book/first-edition/patterns.html" target="_blank">Pattern matching</a></div>

````rust
// Make me print only "Success"es
// ... Warnings are not accepted :)
// Scroll down for hints.
fn main() {
    let ar = vec![2, 5, 42, 56, 22, 3];
    ar.iter().for_each(|x| print_number(*x));
}

fn print_number(number: i32) {
    match number {
        1 => println!("NOP"),
         => println!("Success"), // Change this line
        4 => println!("NOP"),
        _ => println!("NOP"),
    }
}




// Consider using sequence matching or value matching.

````
<!-- .element: class="playground" -->

--

### Exo 5

````rust
// Make me run and pass.
fn main() {
    let array: Vec<u32> = (0..10)
        .xxx() // consider filtering
        .xxxx() // consider concatenation
        .collect();
    
    assert_eq!(vec![0,2,4,6,8,15,16], array)
}

````
<!-- .element: class="playground" -->

--
