# 3. Common Programming Concepts

## 3.1. Variables and Mutability

```rust
fn main() {
    // A variable is immutable
    // let x = 5;
    // Make variable mutable by adding mut
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

### Constants

There are a few differences between constants and variables:
1. You aren't allowed to use mut with constants. Constants aren't just immutable by default — they're always immutable.
2. Constants can be declared in any scope, including the global scope, which makes them useful for values that many parts of code need to know about.
3. Constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

### Shadowing

If you declare a new variable with the same name as a previous variable, we say that the first variable is shadowed by the second, which means that the second variable is what the compiler will see when you use the name of the variable.

```rust
fn main() {
    let x = 5;

    let x = x + 1;  // 6

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");  // 12
    }

    println!("The value of x is: {x}");  // 6
}
```

The other difference between `mut` and shadowing is that because we're creating a new variable when we use the `let` keyword again, we can change the type of the value but reuse the same name.

```rust
let spaces = "   ";        // string type
let spaces = spaces.len(); // number type
```

## 3.2. Data Types

When we converted a `String` to a numeric type using `parse`, we must add a type annotation:

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

### Scalar Types

Rust has four primary scalar types: integers, floating-point numbers, booleans, and characters.

#### Integer Types

|Length|Signed|Unsigned|
|--|--|--|
|8-bit|i8|u8|
|16-bit|i16|u16|
|32-bit|i32|u32|
|64-bit|i64|u64|
|128-bit|i128|u128|
|architecture dependent|isize|usize|

Each signed variant can store numbers from $-(2^{n-1})$ to $2^{n-1}-1$, where n is the number of bits that variant uses. So an i8 can store numbers from -128 to 127.

Unsigned variants can store numbers from 0 to $2^n-1$. So a u8 can store numbers from 0 to 255.

Number literals can also use `_` as a visual separator to make the number easier to read, such as 1_000, which will have the same value as if you had specified 1000.

|Number literals|Example|
|--|--|
|Decimal|98_222|
|Hex|0xff|
|Octal|0o77|
|Binary|0b1111_0000|
|Byte (u8 only)|b'A'|

If you're unsure which type of integer to use, Rust's defaults are generally good places to start: integer types default to i32. The primary situation in which you'd use isize or usize is when indexing some sort of collection.

#### Floating-Point Types

Rust's floating-point types are `f32` and `f64`, which are 32 bits and 64 bits in size, respectively. The default type is `f64`.

All floating-point types are signed.

#### Numeric Operations

```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```

#### The Boolean Type

```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```

#### The Character Type

```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
}
```

Note that we specify `char` literals with single quotes, as opposed to string literals, which use double quotes.

Rust's `char` type is four bytes in size and represents a Unicode scalar value, which means it can represent a lot more than just ASCII.

### Compound Types

Rust has two primitive compound types: tuples and arrays.

#### The Tuple Type

Tuples have a fixed length: once declared, they cannot grow or shrink in size.

Each position in the tuple has a type, and the types of the different values in the tuple don't have to be the same.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value:

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```

We can also access a tuple element directly by using a period (.) followed by the index:

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

#### The Array Type

Array in Rust have a fixed length and every element must have the same type.

```rust
fn main() {
    let months = ["January", "February", "March", "April", "May", "June", "July",
                 "August", "September", "October", "November", "December"];
    let a: [i32; 5] = [1, 2, 3, 4, 5];
    // initialize an array to contain the same value
    let a = [3; 5];
}
```

Accessing Array Elements

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

## 3.3. Functions

Rust code uses snake case as the conventional style for function and variable names, in which all letters are lowercase and underscores separate words.

### Parameters

```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```

### Statements and Expressions

- Statements are instructions that perform some action and do not return a value.
- Expressions evaluate to a resultant value.

Creating a variable and assigning a value to it with the let keyword is a statement.

```rust
fn main() {
    // statement
    let y = 6;
}
```

Function definitions are also statements; calling a function is an expression.

Consider a math operation, such as 5 + 6, which is an expression that evaluates to the value 11.

Calling a macro is an expression.

A new scope block created with curly brackets is an expression:

```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {y}");
}
```

Expressions do not include ending semicolons. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value.

### Functions with Return Values

You can return early from a function by using the `return` keyword and specifying a value, but most functions return the last expression implicitly.

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

If we place a semicolon at the end of the line containing x + 1, changing it from an expression to a statement, we'll get an error:

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
    // x + 1;  // error
}
```

## 3.5. Control Flow

### if Expressions

```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```

#### Handling Multiple Conditions with else if

```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

#### Using if in a let Statement

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

### Repetition with Loops

#### Returning Values from Loops

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

#### Loop Labels to Disambiguate Between Multiple Loops

You can specify a loop label on a loop that you can then use with break or continue to specify that those keywords apply to the labeled loop instead of the innermost loop. Loop labels must begin with a single quote.

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

#### Conditional Loops with while

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

#### Looping Through a Collection with for

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

Machine code generated from `for` loops can be more efficient than `whlie` loops, because the index doesn't need to be compared to the length of the array at every iteration.

Here's what the countdown would look like using a `for` loop and `rev` to reverse the range:

```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```
