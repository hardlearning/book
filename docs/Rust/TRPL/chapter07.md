# 7. Managing Growing Projects with Packages, Crates, and Modules

## 7.1. Packages and Crates

A crate is the smallest amount of code that the Rust compiler considers at a time.

Crates can contain modules, and the modules may be defined in other files that get compiled with the crate.

A crate can come in one of two forms:

1. Binary crates are programs you can compile to an executable that you can run, such as a command line program or a server.
2. Library crates define functionality intended to be shared with multiple projects.

A package is a bundle of one or more crates that provides a set of functionality. A package contains a Cargo.toml file that describes how to build those crates.

A package can contain as many binary crates as you like, but at most only one library crate.

After we run `cargo new my-project`, there's a Cargo.toml file in the project directory, giving us a package.

Cargo follows a convention that `src/main.rs` is the crate root of a binary crate with the same name as the package. Likewise, Cargo knows that if the package directory contains `src/lib.rs`, the package contains a library crate with the same name as the package, and `src/lib.rs` is its crate root. Cargo passes the crate root files to `rustc` to build the library or binary.

## 7.2. Defining Modules to Control Scope and Privacy

### Modules Cheat Sheet

Here, we create a binary crate named backyard:

```
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

Filename: src/main.rs

```rust
use crate::garden::vegetables::Asparagus;

// include the code finds in src/garden.rs
pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {plant:?}!");
}
```

Filename: src/garden.rs

```rust
// the code in src/garden/vegetables.rs
pub mod vegetables;
```

Filename: src/garden/vegetables.rs

```rust
#[derive(Debug)]
pub struct Asparagus {}
```

### Grouping Related Code in Modules

Create a new library named restaurant by running:

```
cargo new restaurant --lib
```

Filename: src/lib.rs

```rust
// define a module
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
}
```

The module tree for the structure:

```
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```

This tree shows how some of the modules nest inside other modules, for example, `hosting` nests inside `front_of_house`.

The tree also shows that some modules are siblings, meaning they're defined in the same module; `hosting` and `serving` are siblings defined within `front_of_house`.

Notice that the entire module tree is rooted under the implicit module named `crate`.

## 7.3. Paths for Referring to an Item in the Module Tree

A path can take two forms:

- An absolute path is the full path starting from a crate root; for code from an external crate, the absolute path begins with the crate name, and for code from the current crate, it starts with the literal `crate`.
- A relative path starts from the current module and uses `self`, `super`, or an identifier in the current module.

Filename: src/lib.rs

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```

Items in a parent module can't use the private items inside child modules, but items in child modules can use the items in their ancestor modules.

The `pub` keyword on a module only lets code in its ancestor modules refer to it, not access its inner code.

### Starting Relative Paths with super

We can construct relative paths that begin in the parent module by using `super` at the start of the path.

```rust
fn deliver_order() {}

mod back_of_house {
    fn fix_incorrect_order() {
        cook_order();
        super::deliver_order();
    }

    fn cook_order() {}
}
```

### Making Structs and Enums Public

If we use `pub` before a struct definition, we make the struct public, but the struct's fields will still be private.

```rust
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}

pub fn eat_at_restaurant() {
    // Order a breakfast in the summer with Rye toast.
    let mut meal = back_of_house::Breakfast::summer("Rye");
    // Change our mind about what bread we'd like.
    meal.toast = String::from("Wheat");
    println!("I'd like {} toast please", meal.toast);

    // The next line won't compile if we uncomment it; we're not allowed
    // to see or modify the seasonal fruit that comes with the meal.
    // meal.seasonal_fruit = String::from("blueberries");
}
```

In contrast, if we make an enum public, all of its variants are then public.

```rust
mod back_of_house {
    pub enum Appetizer {
        Soup,
        Salad,
    }
}

pub fn eat_at_restaurant() {
    let order1 = back_of_house::Appetizer::Soup;
    let order2 = back_of_house::Appetizer::Salad;
}
```

## 7.4. Bringing Paths Into Scope with the use Keyword

We can create a shortcut to a path with the `use` keyword once, and then use the shorter name everywhere else in the scope.

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

### Providing New Names with the as Keyword

```rust
use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {
    // --snip--
}

fn function2() -> IoResult<()> {
    // --snip--
}
```

### Re-exporting Names with pub use

When we bring a name into scope with the `use` keyword, the name is private to the scope into which we imported it. To enable code outside that scope to refer to that name as if it had been defined in that scope, we can combine `pub` and `use`. This technique is called re-exporting.

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

External code would have to call the `add_to_waitlist` function:

```rust
// Before this change
restaurant::front_of_house::hosting::add_to_waitlist();
// After re-exporting
restaurant::hosting::add_to_waitlist();
```

### Using External Packages

To use `rand` in our project, we added this line to Cargo.toml:

```
rand = "0.8.5"
```

Then, to bring `rand` definitions into the scope of our package, we added a `use` line starting with the name of the crate:

```rust
use rand::Rng;

fn main() {
    let secret_number = rand::thread_rng().gen_range(1..=100);
}
```

### Using Nested Paths to Clean Up Large use Lists

We can use nested paths to bring the same items into scope in one line.

```rust
use std::{cmp::Ordering, io};
```

This line brings `std::io` and `std::io::Write` into scope.

```rust
use std::io::{self, Write};
```

### The Glob Operator

If we want to bring all public items defined in a path into scope, we can specify that path followed by the `*` glob operator:

```rust
use std::collections::*;
```

## 7.5. Separating Modules into Different Files

Filename: src/lib.rs

```rust
mod front_of_house;

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

Filename: src/front_of_house.rs

```rust
pub mod hosting;
```

Filename: src/front_of_house/hosting.rs

```rust
pub fn add_to_waitlist() {}
```

### Alternate File Paths

For a module named `front_of_house` declared in the crate root, the compiler will look for the module's code in:

- src/front_of_house.rs (what we covered)
- src/front_of_house/mod.rs (older style, still supported path)

For a module named `hosting` that is a submodule of `front_of_house`, the compiler will look for the module's code in:

- src/front_of_house/hosting.rs (what we covered)
- src/front_of_house/hosting/mod.rs (older style, still supported path)
