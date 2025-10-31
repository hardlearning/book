# 5. Using Structs to Structure Related Data

## 5.1. Defining and Instantiating Structs

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```

### Using the Field Init Shorthand

Because the parameter names and the struct field names are the same, we can use the field init shorthand syntax to write `build_user`:

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```

### Creating Instances from Other Instances with Struct Update Syntax

The syntax `..` specifies that the remaining fields not explicitly set should have the same value as the fields in the given instance.

```rust
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

In this example, we can no longer use `user1` after creating `user2` because the String in the username field of `user1` was moved into `user2`. We can also still use `user1.email`, because its value was not moved out of `user1`.

### Using Tuple Structs Without Named Fields to Create Different Types

Rust also supports structs that look similar to tuples, called tuple structs. Tuple structs don't have names associated with their fields; rather, they just have the types of the fields.

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);

    // destructure the values into variables named x, y, and z.
    let Point(x, y, z) = origin;
}
```

### Unit-Like Structs Without Any Fields

You can also define structs that don't have any fields. These are called unit-like structs.

```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

## 5.2. An Example Program Using Structs

### Refactoring with Structs: Adding More Meaning

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

### Adding Useful Functionality with Derived Traits

Putting the specifier `:?` inside the curly brackets tells `println!` we want to use an output format called `Debug`. The `Debug` trait enables us to print our struct so we can see its value while we're debugging our code.

Rust does include functionality to print out debugging information, but we have to explicitly make that functionality available for our struct. To do that, we add the outer attribute `#[derive(Debug)]` just before the struct definition.

When we have larger structs, we can use `{:#?}` instead of `{:?}` in the `println!` string to have output that's a bit easier to read.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {rect1:?}");
}
```

Another way to print out a value using the Debug format is to use the `dbg!` macro, which takes ownership of an expression (as opposed to `println!`, which takes a reference).

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

## 5.3. Method Syntax

### Defining Methods

The `&self` is actually short for `self: &Self`. Within an `impl` block, the type `Self` is an alias for the type that the `impl` block is for.

If we wanted to change the instance that we've called the method on as part of what the method does, we'd use `&mut self` as the first parameter.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

### Methods with More Parameters

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

### Associated Functions

All functions defined within an `impl` block are called associated functions because they're associated with the type named after the `impl`.

We can define associated functions that don't have `self` as their first parameter (and thus are not methods) because they don't need an instance of the type to work with.

```rust
impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```

To call this associated function, we use the `::` syntax with the struct name:

```rust
let sq = Rectangle::square(3);
```

### Multiple impl Blocks

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```
