# 4. Understanding Ownership

## 4.1. What is Ownership?

Ownership is a set of rules that govern how a Rust program manages memory.

### The Stack and the Heap

The stack stores values in the order it gets them and removes the values in the opposite order. This is referred to as last in, first out.

Adding data is called pushing onto the stack, and removing data is called popping off the stack.

When you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer. This process is called allocating on the heap.

Accessing data in the heap is generally slower than accessing data on the stack because you have to follow a pointer to get there.

When your code calls a function, the values passed into the function (including, potentially, pointers to data on the heap) and the function's local variables get pushed onto the stack. When the function is over, those values get popped off the stack.

### Ownership Rules

- Each value in Rust has an owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

### Variable Scope

```rust
{                      // s is not valid here, since it's not yet declared
    let s = "hello";   // s is valid from this point forward

    // do stuff with s
}                      // this scope is now over, and s is no longer valid
```

### The String Type

String literals are immutable.

Rust has a `String` type. This type manages data allocated on the heap and can be mutated:

```rust
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() appends a literal to a String

println!("{s}"); // this will print `hello, world!`
```

### Memory and Allocation

Rust takes a different path: the memory is automatically returned once the variable that owns it goes out of scope.

```rust
{
    let s = String::from("hello"); // s is valid from this point forward

    // do stuff with s
}  
```

When a variable goes out of scope, Rust calls a special function for us. This function is called `drop`, and it's where the author of `String` can put the code to return the memory.

### Variables and Data Interacting with Move

Integers are simple values with a known, fixed size, and these two 5 values are pushed onto the stack.

```rust
// bind the value 5 to x
let x = 5;
// make a copy of the value in x and bind it to y
let y = x;
```

A String is made up of three parts: a pointer to the memory that holds the contents of the string, a length, and a capacity.

When we assign s1 to s2, the String data is copied, meaning we copy the pointer, the length, and the capacity that are on the stack. We do not copy the data on the heap that the pointer refers to.

```rust
let s1 = String::from("hello");
let s2 = s1;
```

To ensure memory safety, after the line `let s2 = s1;`, Rust considers s1 as no longer valid and s1 was moved into s2.

```rust
let s1 = String::from("hello");
let s2 = s1;

println!("{s1}, world!");  // error
```

### Scope and Assignment

When you assign a completely new value to an existing variable, Rust will call `drop` and free the original value's memory immediately.

```rust
let mut s = String::from("hello");
// free the "hello" immediately
s = String::from("ahoy");

println!("{s}, world!");
```

### Variables and Data Interacting with Clone

If we do want to deeply copy the heap data of the String, not just the stack data, we can use a common method called `clone`.

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {s1}, s2 = {s2}");
```

### Stack-Only Data: Copy

Rust has a special annotation called the `Copy` trait that we can place on types that are stored on the stack. If a type implements the `Copy` trait, variables that use it do not move, but rather are trivially copied, making them still valid after assignment to another variable.

Rust won't let us annotate a type with `Copy` if the type, or any of its parts, has implemented the `Drop` trait.

Here are some of the types that implement `Copy`:

- All the integer types, such as `u32`.
- The Boolean type, `bool`, with values `true` and `false`.
- All the floating-point types, such as `f64`.
- The character type, `char`.
- Tuples, if they only contain types that also implement `Copy`. For example, `(i32, i32)` implements `Copy`, but `(i32, String)` does not.

### Ownership and Functions

Passing a variable to a function will move or copy, just as assignment does.

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function
                                    // and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // Because i32 implements the Copy trait,
                                    // x does NOT move into the function,
                                    // so it's okay to use x afterward.

} // Here, x goes out of scope, then s. However, because s's value was moved,
  // nothing special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```

### Return Values and Scope

Returning values can also transfer ownership.

```rust
fn main() {
    let s1 = gives_ownership();        // gives_ownership moves its return
                                       // value into s1

    let s2 = String::from("hello");    // s2 comes into scope

    let s3 = takes_and_gives_back(s2); // s2 is moved into
                                       // takes_and_gives_back, which also
                                       // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {       // gives_ownership will move its
                                       // return value into the function
                                       // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                        // some_string is returned and
                                       // moves out to the calling
                                       // function
}

// This function takes a String and returns a String.
fn takes_and_gives_back(a_string: String) -> String {
    // a_string comes into scope

    a_string  // a_string is returned and moves out to the calling function
}
```

## 4.2. References and Borrowing

A reference is like a pointer in that it's an address we can follow to access the data stored at that address; that data is owned by some other variable.

The ampersand (&) represent references, and they allow you to refer to some value without taking ownership of it.

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

We call the action of creating a reference borrowing. As in real life, if a person owns something, you can borrow it from them. When you're done, you have to give it back. You don’t own it.

### Mutable References

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

Mutable references have one big restriction: if you have a mutable reference to a value, you can have no other references to that value.

```rust
let mut s = String::from("hello");

// This code that attempts to create two mutable references to s will fail
let r1 = &mut s;
let r2 = &mut s;

println!("{r1}, {r2}");
```

A data race is similar to a race condition and happens when these three behaviors occur:

- Two or more pointers access the same data at the same time.
- At least one of the pointers is being used to write to the data.
- There's no mechanism being used to synchronize access to the data.

Data races cause undefined behavior and can be difficult to diagnose and fix; Rust prevents this problem by refusing to compile code with data races!

We can use curly brackets to create a new scope, allowing for multiple mutable references, just not simultaneous ones:

```rust
let mut s = String::from("hello");

{
    let r1 = &mut s;
} // r1 goes out of scope here, so we can make a new reference with no problems.

let r2 = &mut s;
```

Rust enforces a similar rule for combining mutable and immutable references. This code results in an error:

```rust
let mut s = String::from("hello");

let r1 = &s; // no problem
let r2 = &s; // no problem
let r3 = &mut s; // BIG PROBLEM

println!("{r1}, {r2}, and {r3}");
```

This code will compile because the last usage of the immutable references is in the `println!`, before the mutable reference is introduced:

```rust
let mut s = String::from("hello");

let r1 = &s; // no problem
let r2 = &s; // no problem
println!("{r1} and {r2}");
// Variables r1 and r2 will not be used after this point.

let r3 = &mut s; // no problem
println!("{r3}");
```

### Dangling References

In languages with pointers, it's easy to create a dangling pointer — a pointer that references a location in memory that may have been given to someone else — by freeing some memory while preserving a pointer to that memory.

In Rust, the compiler guarantees that references will never be dangling references: if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.

Let's try to create a dangling reference:

```rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope and is dropped, so its memory goes away.
  // Danger!
```

## 4.3. The Slice Type

Slices let you reference a contiguous sequence of elements in a collection. A slice is a kind of reference, so it does not have ownership.

### String Slices

```rust
let s = String::from("hello world");

let hello = &s[0..5];
// starting at index 6 with a length value of 5
let world = &s[6..11];
```

If you want to start at index 0, you can drop the value before the two periods.

```rust
let s = String::from("hello");

let slice = &s[0..2];
let slice = &s[..2];
```

By the same token, if your slice includes the last byte of the String, you can drop the trailing number.

```rust
let s = String::from("hello");

let len = s.len();

let slice = &s[3..len];
let slice = &s[3..];
```

You can also drop both values to take a slice of the entire string.

```rust
let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
```

Let's rewrite `first_word` to return a slice. The type that signifies "string slice" is written as `&str`:

```rust
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}

fn main() {
    let mut s = String::from("hello world");

    let word = first_word(&s);

    s.clear(); // error!

    println!("the first word is: {word}");
}
```

Because `clear` needs to truncate the `String`, it needs to get a mutable reference. The `println!` after the call to `clear` uses the immutable reference in `word`. Rust disallows the mutable reference in `clear` and the immutable reference in `word` from existing at the same time, and compilation fails.

### String Literals as Slices

The type of `s` here is `&str`: it's a slice pointing to that specific point of the binary.

```rust
let s = "Hello, world!";
```

This is also why string literals are immutable, `&str` is an immutable reference.

### String Slices as Parameters

Defining a function to take a string slice (`&str`) instead of a reference to a String (`&String`) makes our API more general and useful without losing any functionality:

```rust
// If we have a string slice, we can pass that directly. If we have a String,
// we can pass a slice of the String or a reference to the String.
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}

fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole.
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s.
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or whole.
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```

### Other Slices

```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];

assert_eq!(slice, &[2, 3]);
```

This slice has the type `&[i32]`. It stores a reference to the first element and a length.
