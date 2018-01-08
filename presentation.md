<!-- .slide: data-background="#2C374C" -->

# Welcome in xke-rs <!-- .element: class="grisFonce2" -->
For those who didn't had time to install rust.
```
curl https://sh.rustup.rs -sSf | sh
```

Note:
    This is the speaker notes

---

# Rust

**From hero to zero** <!-- .element: class="grisFonce2" -->

---

### Hands On

Organization:
1. Language presentation
2. Exercise
3. Question

Animators:
* PODYACHIY Dimitry
* PETIT Jean-Baptiste

---

### What is rust ?
* Programing language
* GC less
* Low level
* Abstractions (iterators, closure, types...)
* Version 1 in may 2015
* In production in mozilla, Atlassian, npm, clever cloud, dropbox...

---

Why rust instead of go ? (or the differences between Rust and Go).

||Rust|Go|
|---|---|---|
|Runtime|[lightweight](https://www.rust-lang.org/en-US/faq.html#does-rust-have-a-runtime)|[pretty big](https://www.quora.com/How-does-the-Go-runtime-work-What-does-it-consist-of-What-functionalities-does-it-provide-and-what-can-be-expected-from-a-developer-perspective)|
|GC|no|yes|
|Types|strong|soft|
|LC|hard|easy|
|Goal|replace C ([a safe, modern and fearless concurrent C](https://www.rust-lang.org/en-US/faq.html#what-is-this-projects-goal))|[tool with fast compilation time and easy concurrency](https://talks.golang.org/2012/splash.article)|

--

They are not on the same field. Rust isn't better than Go. Go isn't better than rust.

--

But, why docker has choose Go if it wasn't a C replacement ?? Because [various](https://fr.slideshare.net/jpetazzo/docker-and-go-why-did-we-decide-to-write-docker-in-go/18-Why_GoThe_Five_Reasons_Why) reasons but none of them is: Go is a drop in replacement to C/C++).

---

Why would we learn Rust ? Why it would be nice to know rust in Xebia ?
* Learn Rust, increase your computer comprehension.
* IOT guys, rust is for you.
* Rust is growing.
* Wanna: true performance && security && low memory usage && memory predictability, for a new project ?

---

## Cargo

The Rust package manager <!-- .element: class="beige" -->

--

### Cargo

* Bootstrap a project
* Build code
* Manage dependencies

--


Bootstrap

```bash
$ cargo new hello_cargo --bin
$ cd hello_cargo
$ tree .
.
├─ Cargo.toml
└─ src
    └─ main.rs
```

Build / run

```bash
$ cargo build
$ cargo run
```

--

## Exercises

![triomphe](images/triomphe.png) <!-- .element: class="borderless medium" -->

--

1. Create a new project with cargo
2. Execute it
3. Try to change ```src/main.rs``` 

```rust
println!("Hello, world!");
// to 
println("Hello, world!");
```

and build it   

---

## Functional Programming
Is possible in rust <!-- .element: class="beige" -->

--
