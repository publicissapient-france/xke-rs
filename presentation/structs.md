## Object Programming

--

### Structs

* Use `````struct````` to encapsulate data.

````rust
struct User {
    username: String,
    sign_in_count: u64,
    active: bool
}

fn main() {
    let bobby = User { 
      username: String::from("bobby@xebia.rs"),
      active: true,
      sign_in_count: 1,
    };
}
````

--

### Implems

* Use ```impl``` to define method over the struct.

````rust
struct Rectangle {width: u32, height: u32}
impl Rectangle {
    fn to_string(&self) -> String {
        format!("width={},height={}",self.width, self.height)
    }
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }
}

fn main() {
    let sq = Rectangle::square(3);
    println!("{}", sq.to_string());
}
````

--

### Traits

* Define shared behavior.

````rust
trait Summarizable {
    fn summary(&self) -> String;
}

struct Tweet {
    user: String, 
    content: String
}

impl Summarizable for Tweet {
    fn summary(&self) -> String {
        format!("{}: {}", self.user, self.content)
    }
}
````

--

### Derivation

* Use ````derive```` in order to implement by default trait.

````rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };
    println!("rect1 is {:?}", rect1);
}
````

--

### Example Trait Drop

* Drop a destructor trait.

````rust
struct ImportantResource {
    value: i64
}

impl Drop for ImportantResource {
    fn drop(&mut self) {
        println!("Do something with {} euros before the end.", self.value);
    }
}

fn main() {
    let bobby = ImportantResource {value: 1000000};
}
````

--

![triomphe](https://xebia-france.github.io/xke-rs/images/triomphe.png) <!-- .element: class="borderless medium" -->

--

### Exo 1

```rust
// Write a structure Point with to i32 inside x and y.
struct ???
fn main () {
    let point = ???
    assert_eq!(5, point.x);
    assert_eq!(10, point.y);
}

```

--

### Exo 2

```rust
// Use the same struct as previously and implement a 'new' method.
struct Point {
    x: i32,
    y: i32
}

impl ???

fn main () {
    let point = Point::new(5, 10);
    assert_eq!(5, point.x);
    assert_eq!(10, point.y);
}

```

--

### Exo 3

```rust
// Implement a translate_by_two method that multiply by two x and y.
struct Point {
    x: i32,
    y: i32
}

impl Point {
    fn new (x: i32, y: i32) -> Point {
        Point {x, y}
    }

    ???
}

fn main () {
    let mut point = Point::new(5, 10);
    assert_eq!(5, point.x);
    assert_eq!(10, point.y);

    point.translate_by_two();
    assert_eq!(10, point.x);
    assert_eq!(20, point.y);
}

```

--

### Exo 4

```rust
// Implement a generic Point struct that can hold either i32 or f64.
struct ???
fn main () {
    let point = Point { x: 5, y: 10};
    assert_eq!(5, point.x);
    assert_eq!(10, point.y);    
    
    let point_float = Point { x: 5.10, y: 10.10};
    assert_eq!(5.10, point_float.x);
    assert_eq!(10.10, point_float.y);
}








// Generic notation of struct is MyStruct<T>

```

--

### Exo 5

```rust
// Implement the trait Printable for Point, consider using the macro format! to create the String.
trait Printable {
    fn print(&self) -> String;
}

struct Point {
    x: i32,
    y: i32
}

???

fn main () {
    let point = Point { x: 5, y: 10 };
    assert_eq!("Point { x: 5, y: 10 }".to_string(), point.print())
}









// "impl Trait for Struct" is the right notation.

```
