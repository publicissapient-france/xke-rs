## Cargo

The Rust package manager <!-- .element: class="beige" -->

--

### Cargo

* Bootstrap a project
* Build code
* Manage dependencies

Note:
Cargo gère trois choses: 
* **construction** de notre code, 
* téléchargement (**gestion**) des dépendances dont notre code a besoin
* **construction des ces dépendances**.

Il est egalement capable de initialiser une application ou une dépendance. 

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
$ cargo run
```

Note:
Cargo.toml(capital c) est le fichier de configuration qui contient tous les **meta-données** que Cargo a besoin pour compiler votre projet. 

--

## Exercises

![triomphe](https://xebia-france.github.io/xke-rs/images/triomphe.png) <!-- .element: class="borderless medium" -->

--

1. Create a new project with cargo
2. Execute it
3. Try to change ```src/main.rs``` 

```rust
// from
println!("Hello, world!");
// to 
println("Hello, world!");
```

and build it   
