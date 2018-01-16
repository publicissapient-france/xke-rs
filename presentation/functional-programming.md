## Functional Programming

--

### Optional

* There is no ```null``` (or ```undefined```).
* Use ````Some```` or presence or ```None``` for absence.

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

### Exercice 1

--
