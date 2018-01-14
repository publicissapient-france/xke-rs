## Ownership

* Rust’s central feature
* Memory safety guarantees
* Without garbage collector (GC)


Note:
All programs have to manage the way they use a computer’s memory while running. 
Some languages have garbage collection that constantly looks for no longer used memory as the program runs; 
in other languages, the programmer must explicitly allocate and free the memory. 
Rust uses a third approach: memory is managed through a system of ownership with a set of rules that the compiler checks at compile time. 
No run-time costs are incurred for any of the ownership features.

--

### Ownership rules

1. Each value in Rust has a ```owner```.
1. There can only be ```one``` owner at a time.
1. When the owner goes out of scope, the value will be ```dropped```.

--

### Variable Scope

```rust

{                      // 's' is not valid here, not declared
    let s = "Hello";   // 's' is valid from this point

    // do stuff with s
}                      // this scope is now over, 
                       // and 's' is no longer valid
```

Note:
Variable bindings have ownership of what they’re bound to. A piece of data can only have one owner at a time. 
When a binding goes out of scope, Rust will free the bound resources. This is how Rust achieves memory safety.


--

### Borrowing

<div>
**Borrow (verb):** 
To _receive_ something </br>with the promise of _returning_ it
</div> <!-- .element: class="beige" -->


Note:
But in real life applications, most of the times we have to pass variable bindings to other functions 
or assign them to another variable bindings. In this case we referencing the original binding; borrow the data of it.

--

### Data types

Copy Type (stack)

```rust
fn main() {
    let a = "Hello Xebia";
    let b = a;
    println!("a: {}, b: {}", a, b); 
    // ==> a: Hello Xebia, b: Hello Xebia
}
```

Move type (heap) <!-- .element: class="fragment" data-fragment-index="2" -->

```rust
fn main() {
    let a = String::from("Hello Xebia");
    let b = a;
    println!("a: {}, b: {}", a, b); 
    // ==> Error: use of moved value: `a`
}
```
<!-- .element: class="fragment" data-fragment-index="2" --> 


Note:
When assigning a variable binding to another variable binding or when passing it to a function(Without referencing), if its data type is a
Copy Type:
    - Bound resources are made a copy and assign or pass it to the function.
    - The ownership state of the original bindings are set to “copied” state.
    - Mostly Primitive types
Copy the pointer, the length, and the capacity that are on the stack. We do not copy the data on the heap that the pointer refers to    
Move type:
    - Bound resources are moved to the new variable binding and we can not access the original variable binding anymore.
    - The ownership state of the original bindings are set to “moved” state.
    - Non-primitive type

--

### Types of borrowing
* Shared Borrowing ```(&T)```
<div>A piece of data can be borrowed by a **single or multiple** users,</br> but data should **not be altered**</div> <!-- .element: class="fragment small" data-fragment-index="2" -->
* <div>Mutable Borrowing ```(&mut T)```</div>
<div>A piece of data can be borrowed and altered by a **single user**, </br>but the data should **not be accessible** for any other users at that time.</div> <!-- .element: class="fragment small" data-fragment-index="3" -->

Note:
Types of borrowing:
- Shared Borrowing (&T) : A piece of data can be borrowed by a single or multiple users, but data should not be altered.
- Mutable Borrowing (&mut T) : A piece of data can be borrowed and altered by a single user, but the data should not be accessible for any other users at that time.

--

#### Examples

```rust
fn main() {
  let mut a = vec![1, 2, 3];
  let b = &mut a;  //  &mut borrow of 'a' starts here
                   //  ⁝
  // some code     //  ⁝
  // some code     //  ⁝
}                  //  &mut borrow of 'a' ends here

fn main() {
  let mut a = vec![1, 2, 3];
  let b = &mut a;  //  &mut borrow of 'a' starts here
  // some code
  
  println!("{:?}", a); // trying to access 'a' as a 
                       // shared borrow, so giving error
}                  //  &mut borrow of 'a' ends here

fn main() {
  let mut a = vec![1, 2, 3];
  {
    let b = &mut a;  //  &mut borrow of 'a' starts here
    // any other code
  }                  //  &mut borrow of 'a' ends here
  
  println!("{:?}", a); // allow to borrow 'a' as a shared borrow
}
```

--

#### Deep copy (clone)

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

--

## References and Borrowing

TBD

--

## Exercises

![triomphe](../images/triomphe.png) <!-- .element: class="borderless medium" -->
