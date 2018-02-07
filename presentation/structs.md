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

``` rust
// Exercise with struc

```

--

### Exo 2

``` rust
// Exercise with struc

```

--

### Exo 3

``` rust
// Exercise with implems

```

--

### Exo 4

``` rust
// Exercise with trait

```

--

### Exo 5

``` rust
// Exercise with derivation

```
