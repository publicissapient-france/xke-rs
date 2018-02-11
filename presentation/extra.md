## Extra
#### Only for the brave <!-- .element: class="beige" -->

--

### Exercise on struct 1

```rust
// Implement a generic Point struct that can hold either i32 or f64, mixed
struct ???
fn main () {
    let point = Point { x: 5, y: 10.10};
    assert_eq!(5, point.x);
    assert_eq!(10.10, point.y);    
    
    let point_2 = Point { x: 5.10, y: 10};
    assert_eq!(5.10, point_2.x);
    assert_eq!(10, point_2.y);
}

```
<!-- .element: class="playground" -->

--

### Exercise on struct 2

```rust
// Create a "yeah_printable" function that takes a Printable and return a String like "YEAH, Point { x: 5, y: 10 }".
trait Printable {
    fn print(&self) -> String;
}

struct Point {
    x: i32,
    y: i32
}

impl Printable for Point {
    fn print(&self) -> String {
        format!("Point x: {}, y: {}", self.x, self.y)
    }
}

???

fn main () {
    let point = Point { x: 5, y: 10 };
    assert_eq!("YEAH, Point { x: 5, y: 10 }".to_string(), yeah_printable(point))
}

```
<!-- .element: class="playground" -->

--

### Exercise on closure 1

<div><a href="https://doc.rust-lang.org/book/second-edition/ch13-01-closures.html" target="_blank">Closures</a></div>

````rust
// Make me pass the assertion
fn main() {
    let mut num_five = 5;
    
    {
        let mut add_some_number = |x: i32| num_five += x; // Force closure to take ownership of num_five
        add_some_number(5);
    }

    assert_eq!(5, num_five);
}







// When declaring a closure without any keyword (mut, move... ) the closure capture environment by borrow immutably.
// If you want to modify a captured environment variable, this variable must be borrowed mutable and the closure must be mutable (set with mut keyword).
// If you want to copy (take ownership) the environment you must use the keyword move.
````
<!-- .element: class="playground" -->

--

### Exercise on closure 2

````rust
// Implement a closure that fulfil the requirement of G: FnMut(i32) -> ().

fn main() {
    let mut env_ownershiped = 4;
    let mut env_mutable = 4;
    let env_borrowed = 4;

    {
        let mut closures = Closures {
            closure_that_moves_its_environment: move |x| env_ownershiped = env_ownershiped + x,
            closure_that_borrow_mutable_its_environment: ???,
            closure_that_borrow_immutable_its_environment: |x| x + env_borrowed,
        };

        // Do you think we can write another closure with 'env_mutable' and call it here ?

        (closures.closure_that_moves_its_environment)(5);
        (closures.closure_that_borrow_mutable_its_environment)(5);
        (closures.closure_that_borrow_immutable_its_environment)(5);
    }
    
    println!("env_ownershiped is moved into closure so it initial value don't change: 4, {}", env_ownershiped);
    println!("env_mutable is modified by closure so it value is 9, {}", env_mutable);
    println!("env_borrowed is not modified so it value is 4, {}", env_borrowed);
}

struct Closures<F: FnOnce(i32) -> (), G: FnMut(i32) -> (), H: Fn(i32) -> i32> {
    closure_that_moves_its_environment: F,
    closure_that_borrow_mutable_its_environment: G,
    closure_that_borrow_immutable_its_environment: H,
}











// Answer is no because we cannot borrow multiple time a mutable value.
````
<!-- .element: class="playground" -->

--

### Exercise on Iterator 1

````rust
// Implement an infinite iterator that give the price of the bitcoin
fn main() {
    let mut bitcoin_price = BitcoinPrice {current_price: 4000}; // here the initial price, the first value of the iterator
    
    assert_eq!(Some(41990.4), bitcoin_price.nth(3)); // the fourth value of the iterator is 41990.4
}

struct BitcoinPrice {
    current_price: f64,
}

impl Iterator for BitcoinPrice {
    type Item = f64;
    
    fn next(&mut self) -> Option<f64> {
        // return here the next value of the iterator by increasing the current one of 80%
    }
}

````
<!-- .element: class="playground" -->


--


## LS 
#### Exercise <!-- .element: class="beige" -->

* Create an ```ls``` alternative called ````xe```` that prints the content of the current directory
* Add clap-rs dependency from crates.io in order to have ````--version````, ````--help```` and ````-la````
* Should be tested
* Release it with cargo (create a ````release```` version)
