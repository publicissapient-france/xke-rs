## Lifetimes
#### "Rust’s most distinctive feature."

--

## The truth on borrowing
* Borrow a variable == create a reference

--

## C++ and Dandling reference hell
* Lifetime to the rescue

--

## The Borrow checker
* Each reference has a lifetime, but most of them are implicit and inferred.

````rust
fn main() {
    let r;         // -------+-- 'a
                   //        |
    {              //        |
        let x = 5; // -+-----+-- 'b
        r = &x;    //  |     |
    }              // -+     |
                   //        |
    println!("r: {}", r); // |
                   //        |
                   // -------+
}
````

--

## Lifetime annotation

````rust
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
````

--

## Lifetime in function
* An interesting example.

````rust
fn main() {
    let result = longest("1.0", "10");
    println!("The longest string is {}", result);
}

fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
````

--

## Lifetime in struct
* An interesting example.

````rust
fn main() {
    let la_horde_du_contrevent = Book {code: 123456};
    let case = Bookcase {book: &la_horde_du_contrevent};
}

struct Book {
    code: i64
}

struct Bookcase<'a> {
    book: &'a Book
}
````
