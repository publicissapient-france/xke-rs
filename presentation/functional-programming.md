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
// Make me run by using Some, None
fn main() {
    let result = checked_division(12, 0);
    println!("{:?} option of something or None when nothing", result)
}

fn checked_division(dividend: i32, divisor: i32) -> Option<i32> {
        Some(dividend / divisor)
}

````

--

### Exo 2

````rust
// Make me compile by using Some, None
fn main() {
    let maybe_seven = Some(7);
    
    if let 7 = maybe_seven {
        println!("maybe_seven equal to: {}")
    }
}

````

--

### Exo 3

````rust
// Make me compile for only print "Success". Change only line 6. Print only if x + y is equal to 0 where Pair(x, y).
fn main() {
    let pair = (2, -2);

    match pair {
          => println!("Success"),
        (x, y) => println!("x: {}, y: {}", x, y),
    }
}

````

--

### Exo 4

````rust
// Make me compile for only print "Success". Change only line 10.
fn main() {
    let ar = vec![2, 5, 42, 56, 22, 3];
    ar.iter().for_each(|x| print_number(*x));
}

fn print_number(number: i32) {
    match number {
        1 => println!("NOP"),
          => println!("Success"),
        _ => println!("NOP"),
    }
}

````

--

### Exo 5

````rust
// Make me pass for closure by changing line 7.
fn main() {

let mut num_five = 5;

{
    let mut add_some_number = |x: i32| num_five += x;

    add_some_number(5);
}

assert_eq!(5, num_five);
}
````

--

### Exo 6

````rust
// Make me pass for closure by changing line 3.
fn main() {
    let bar = 
    
    assert_eq!(-10, (bar.my_closure)(5));
}

struct Bar<F: FnOnce(i32) -> i32> {
    my_closure: F
}
````

--

### Exo 7

````rust
// Make me run and pass change only line 3.
fn main() {
    let array: Vec<u32> = (0..10).xxx.collect();
    assert_eq!(vec![0,2,4,6,8,15,16], array)
}

````

--

### Exo 8

````rust
// Make me run and pass. Consider Read next chapter before doing this.
fn main() {
    let mut bitcoin_price = BitcoinPrice {current_price: };
    
    assert_eq!(Some(41990.4), bitcoin_price.nth(3));

}

struct BitcoinPrice {
    current_price: f64,
}

impl Iterator for BitcoinPrice {
    type Item = f64;
    
    fn next(&mut self) -> Option<f64> {

    }
}







// Hint, start with 4000 and increase by 80%
````

--
