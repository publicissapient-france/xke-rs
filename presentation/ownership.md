## Ownership

* Rust’s central feature
* Memory safety guarantees
* Without garbage collector (GC)


Note:
* Tous les programmes doivent gérer la façon dont ils utilisent la mémoire pendant l'exécution.
* Certaines langages ont une **Gargabe Collector (GC)** qui cherche constamment la mémoire non utilisée pendant l'exécution du programme;
dans d'autres langues, le programmeur doit **explicitement** allouer et libérer la mémoire.
* Rust utilise une troisième approche: la mémoire est gérée par un système de **Ownership** avec un ensemble de règles que le compilateur vérifie au moment de la **compilation**.
* **Aucun coût d'exécution** n'est engagé pour les fonctionnalités d'Ownership.
* Bien que cette fonctionnalité soit simple à expliquer, elle a de profondes implications pour le reste de la langage.

--

### Ownership rules

1. Each value in Rust has a ```owner```
1. There can only be ```one``` owner at a time
1. When the owner goes out of scope, the value will be ```dropped```

--

### Variable Scope

```rust

{                      // 's' is not valid here, not declared
    let s = "Hello";   // 's' is valid from this point

    // do stuff with s
}                      // this scope is now over, 
                       // and 's' is no longer valid
```

--

### Data types
Let's talk a bit about the Stack and the Heap. <!-- .element: class="beige" -->

Copy Type (stack)

```rust
fn main() {
    let x = 5; // i32
    let y = x;
    println!("x: {}, y: {}", x, y); 
    // ==> x: 5, y: 5
}
```
<!-- .element: class="fragment" data-fragment-index="2" -->

Move Type (heap)

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("s1: {}, s2: {}", s1, s2); 
    // ==> Compiler error: use of moved value: `s1`
}
```
<!-- .element: class="fragment" data-fragment-index="3" --> 

Note:
Petit rappel sur la stack et sur la heap - deux manière de gérer la mémoire pour un programme :
- La stack, très rapide, mais allocation des valeurs en LIFO.
- La heap, plus lente, mais possibilité d'allocation de très grosse valeurs.

En rust

Lors de l'affectation d'une variable à une autre ou lors de son passage à une fonction (sans référence), si son type de données est un

**Move type:**
- les types non primitives
- seulement le pointeur et la capacité sont copiés. Mais les données actuelles (référencés par le pointeur) ne sont pas copiés
- le state de l'ownership est setté comme "moved"

**Copy Type:**
- globalement les **types primitives**
- les donnée sont **copiés**
- le state de l'ownership est setté comme "copied".

--

Representation in memory <br/> after ```s1``` has been invalidated (move)

![ownership](images/ownership-1.png) <!-- .element: class="borderless medium" -->

Note:
- Rust considère que ``` s1``` n'est plus valide !
- Avec seulement ```s2``` valide, quand il sort de la scope, le mémoire est libérée.

Le concept de copier le pointeur, la longueur et la capacité sans copier les données ressemble probablement à une **Shallow copy**.
Mais parce que Rust invalide également la première variable, au lieu de l'appeler **Shallow copy**, on l'appele le **move**.

--

#### Deep copy (clone)

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

Note:
Peut être cher car toute la mémoire est copiée

--

### Ownership and Functions

Similar to assigning a value to a variable <!-- .element: class="beige" -->

```rust
fn main() {
  let x = 5;                                                   // x comes into scope.
  makes_copy(x);                                               // x would move into the function, but i32 is Copy, so it’s okay to still use x afterward.

  let s = String::from("hello");                               // s comes into scope.
  takes_ownership(s); // s's value moves into the function...  and so is no longer valid here.

  let s1 = String::from("hello");                              // s1 comes into scope.
  let s2 = takes_and_gives_back(s1);                           // s1 is moved into takes_and_gives_back, which also moves its return value into s2
}                                                              // Here, x goes out of scope, then s. But since s's value was moved, nothing special happens.

fn makes_copy(some_integer: i32) {                             // some_integer comes into scope.
    println!("{}", some_integer);
}                                                              // Here, some_integer goes out of scope. Nothing special happens.

fn takes_ownership(some_string: String) {                      // some_string comes into scope.
    println!("{}", some_string);
}                                                              // Here, some_string goes out of scope and `drop` is called. The backing memory is freed.

fn takes_and_gives_back(a_string: String) -> String {          // a_string comes into scope.
    a_string                                                   // a_string is returned and moves out to the calling function.
}
```

--

### Borrowing

<div>
**Borrow (verb):** 
To _receive_ something </br>with the promise of _returning_ it
</div> <!-- .element: class="beige" -->


Note:
Mais dans les applications réelles, la plupart du temps nous devons passer les variables à d'autres fonctions
ou les affecter à une autre variable. Dans ce cas, nous référençons le binding d'origin; permettant d'emprunter les données de celui-ci.

--

### Types of borrowing
* Shared Borrowing ```(&T)```
<div>A piece of data can be borrowed by a **single or multiple** users,</br>
but data should **not be altered**.</div> <!-- .element: class="fragment small" data-fragment-index="2" -->
```
let s1 = String::from("hello");
let s2 = &s1;
let s3 = &s1;
``` 
<!-- .element: class="fragment small" data-fragment-index="2" -->

* <div>Mutable Borrowing ```(&mut T)```</div>
<div>A piece of data can be borrowed and altered by a **single user**, <br/>
but the data should **not be accessible** for any other users at that time.<br/>
</div> <!-- .element: class="fragment small" data-fragment-index="3" -->
```
let mut s1 = String::from("hello");
let s2 = &mut s1;
```
<!-- .element: class="fragment small" data-fragment-index="3" -->

Note:
Types of borrowing:
- Shared Borrowing (&T) : un élément peut être emprunté par un ou plusieurs utilisateurs, mais les données ne doivent pas être modifiées.
- Mutable Borrowing (&mut T) : Un élément peut être emprunté et modifié par un seul utilisateur, mais les données ne doivent pas être accessibles à d'autres utilisateurs à ce moment-là.

--

#### Examples

```rust
// 1
fn main() {
  let mut a = vec![1, 2, 3];
  let b = &mut a;      // &mut borrow of 'a' starts here
  // some code         // ⁝
}                      // &mut borrow of 'a' ends here

// 2
fn main() {
  let mut a = vec![1, 2, 3];
  let b = &mut a;      // &mut borrow of 'a' starts here
  // some code
  println!("{:?}", &mut a); // trying to access 'a' as a 
                       // shared borrow, so giving error
}

// 3
fn main() {
  let mut a = vec![1, 2, 3];
  {
    let b = &mut a;    // &mut borrow of 'a' starts here
    // any other code
  }                    // &mut borrow of 'a' ends here
  
  println!("{:?}", &mut a); // allow to borrow 'a' as a shared borrow
}
```

--

#### Examples 
Functions <!-- .element: class="beige" -->

```rust
fn main() {
    let s1 = String::from("hello");
    let len = calculate_length(&s1);
    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

```rust
fn main() {
    let mut s = String::from("hello");
    change(&mut s);
    println!("{}", s); // ==> hello, world 
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```
<!-- .element: class="fragment" data-fragment-index="2" -->

--

## Exercises

![triomphe](https://xebia-france.github.io/xke-rs/images/triomphe.png) <!-- .element: class="borderless medium" -->

--


### Exo 1

<div>
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Ownership</a> & 
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Borrowing</a>
</div> <!-- .element: class="small" -->

```rust
// Make me compile without changing line 9! Scroll down for hints :)

pub fn main() {
    let vec0 = Vec::new();

    let vec1 = fill_vec(vec0);

    // Do not change the following line!
    println!("{} has length {} content `{:?}`", "vec0", vec0.len(), vec0);

    vec1.push(88);

    println!("{} has length {} content `{:?}`", "vec1", vec1.len(), vec1);

}

fn fill_vec(vec: Vec<i32>) -> Vec<i32> {
    let mut vec = vec;

    vec.push(22);
    vec.push(44);
    vec.push(66);

    vec
}














// Part 1
// So you've got the "cannot borrow immutable local variable `vec1` as mutable" error on line 11,
// right? The fix for this is going to be adding one keyword, and the addition is NOT on line 11
// where the error is.

// Part 2
// So `vec0` is being *moved* into the function `fill_vec` when we call it on
// line 6, which means it gets dropped at the end of `fill_vec`, which means we
// can't use `vec0` again on line 9 (or anywhere else in `main` after the
// `fill_vec` call for that matter). We could fix this in a few ways, try them
// all!
// 1. Make another, separate version of the data that's in `vec0` and pass that
// to `fill_vec` instead.
// 2. Make `fill_vec` borrow its argument instead of taking ownership of it,
// and then copy the data within the function in order to return an owned
// `Vec<i32>`
// 3. Make `fill_vec` *mutably* borrow its argument (which will need to be
// mutable), modify it directly, then not return anything. Then you can get rid
// of `vec1` entirely -- note that this will change what gets printed by the
// first `println!`
```
<!-- .element: class="playground" -->

--

### Exo 2

<div>
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Ownership</a> & 
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Borrowing</a>
</div> <!-- .element: class="small" -->

```rust
// Make me compile without adding new lines-- just changing existing lines!
// (no lines with multiple semicolons necessary!)
// Scroll down for hints :)

pub fn main() {
    let vec0 = Vec::new();

    let mut vec1 = fill_vec(vec0);

    println!("{} has length {} content `{:?}`", "vec1", vec1.len(), vec1);

    vec1.push(88);

    println!("{} has length {} content `{:?}`", "vec1", vec1.len(), vec1);

}

fn fill_vec(vec: Vec<i32>) -> Vec<i32> {
    vec.push(22);
    vec.push(44);
    vec.push(66);

    vec
}

















// The difference between this one and the previous ones is that the first line
// of `fn fill_vec` that had `let mut vec = vec;` is no longer there. You can,
// instead of adding that line back, add `mut` in one place that will change
// an existing binding to be a mutable binding instead of an immutable one :)
```
<!-- .element: class="playground" -->

--

### Exo 3

<div>
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Ownership</a> & 
<a href="https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html" target="_blank">Borrowing</a>
</div> <!-- .element: class="small" -->

```rust
// Refactor this code so that instead of having `vec0` and creating the vector
// in `fn main`, we instead create it within `fn fill_vec` and transfer the
// freshly created vector from fill_vec to its caller. Scroll for hints!

pub fn main() {
    let vec0 = Vec::new();

    let mut vec1 = fill_vec(vec0);

    println!("{} has length {} content `{:?}`", "vec1", vec1.len(), vec1);

    vec1.push(88);

    println!("{} has length {} content `{:?}`", "vec1", vec1.len(), vec1);

}

fn fill_vec(vec: Vec<i32>) -> Vec<i32> {
    let mut vec = vec;

    vec.push(22);
    vec.push(44);
    vec.push(66);

    vec
}












// Stop reading whenever you feel like you have enough direction :) Or try
// doing one step and then fixing the compiler errors that result!
// So the end goal is to:
// - get rid of the first line in main that creates the new vector
// - so then `vec0` doesn't exist, so we can't pass it to `fill_vec`
// - we don't want to pass anything to `fill_vec`, so its signature should
//   reflect that it does not take any arguments
// - since we're not creating a new vec in `main` anymore, we need to create
//   a new vec in `fill_vec`, similarly to the way we did in `main`
```
<!-- .element: class="playground" -->

