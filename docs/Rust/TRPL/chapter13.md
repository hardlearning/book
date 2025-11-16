# 13. Functional Language Features: Iterators and Closures

Functional programming often includes using functions as values by passing them in arguments, returning them from other functions, assigning them to variables for later execution, and so forth.

## 13.1. Closures: Anonymous Functions that Capture Their Environment

### Capturing the Environment with Closures

```rust
#[derive(Debug, PartialEq, Copy, Clone)]
enum ShirtColor {
    Red,
    Blue,
}

struct Inventory {
    shirts: Vec<ShirtColor>,
}

impl Inventory {
    fn giveaway(&self, user_preference: Option<ShirtColor>) -> ShirtColor {
        // This is a closure that takes no parameters itself
        user_preference.unwrap_or_else(|| self.most_stocked())
    }

    fn most_stocked(&self) -> ShirtColor {
        let mut num_red = 0;
        let mut num_blue = 0;

        for color in &self.shirts {
            match color {
                ShirtColor::Red => num_red += 1,
                ShirtColor::Blue => num_blue += 1,
            }
        }
        if num_red > num_blue {
            ShirtColor::Red
        } else {
            ShirtColor::Blue
        }
    }
}

fn main() {
    let store = Inventory {
        shirts: vec![ShirtColor::Blue, ShirtColor::Red, ShirtColor::Blue],
    };

    let user_pref1 = Some(ShirtColor::Red);
    let giveaway1 = store.giveaway(user_pref1);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref1, giveaway1
    );

    let user_pref2 = None;
    let giveaway2 = store.giveaway(user_pref2);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref2, giveaway2
    );
}
```

The closure captures an immutable reference to the `self` Inventory instance and passes it with the code we specify to the `unwrap_or_else` method. Functions are not able to capture their environment in this way.

### Closure Type Inference and Annotation

```rust
let expensive_closure = |num: u32| -> u32 {
    println!("calculating slowly...");
    thread::sleep(Duration::from_secs(2));
    num
};
```

Here, we define a function that adds 1 to its parameter and a closure that has the same behavior, for comparison.

```rust
// a function definition
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
// a fully annotated closure definition
let add_one_v2 = |x: u32| -> u32 { x + 1 };
// remove the type annotations from the closure definition
let add_one_v3 = |x| { x + 1 };
// remove the brackets because the closure body has only one expression
let add_one_v4 = |x| x + 1;
```

### Capturing References or Moving Ownership

We define a closure that captures an immutable reference to the vector named `list` because it only needs an immutable reference to print the value.

```rust
fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {list:?}");

    let only_borrows = || println!("From closure: {list:?}");

    println!("Before calling closure: {list:?}");
    only_borrows();
    println!("After calling closure: {list:?}");
}
```

We change the closure body so that it adds an element to the `list` vector. The closure now captures a mutable reference.

```rust
fn main() {
    let mut list = vec![1, 2, 3];
    println!("Before defining closure: {list:?}");

    let mut borrows_mutably = || list.push(7);

    borrows_mutably();
    println!("After calling closure: {list:?}");
}
```

Between the closure definition and the closure call, an immutable borrow to print isn't allowed because no other borrows are allowed when there's a mutable borrow.

If you want to force the closure to take ownership of the values it uses in the environment even though the body of the closure doesn't strictly need ownership, you can use the `move` keyword before the parameter list.

```rust
use std::thread;

fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {list:?}");

    thread::spawn(move || println!("From thread: {list:?}"))
        .join()
        .unwrap();
}
```

### Moving Captured Values Out of Closures and the Fn Traits

