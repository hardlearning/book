# 1. Getting Started

## 1.1 Installation

- Installing rustup on Linux

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
# install C compiler
sudo apt install build-essential
```

- Installing rustup on macOS

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
# install C compiler
xcode-select --install
```

- Installing rustup on Windows

1. Download [rustup-init.exe](https://www.rust-lang.org/tools/install) and install rustup.
2. To check whether you have Rust installed correctly:

```
rustc --version
```

#### Updating and Uninstalling

```
# Update to a newly released version
rustup update
# Uninstall Rust and rustup
rustup self uninstall
```

#### Local Documentation

```
# Open the local documentation in browser
rustup doc
```

## 1.2 Hello, World!

#### Writing and Running a Rust Program

Filename: main.rs

```rust
fn main() {
    // using ! means that you're calling a macro instead of a normal function
    println!("Hello, world!");
}
```

Compile and run the file:

```
rustc main.rs
./main
```

## 1.3. Hello, Cargo!

Check whether Cargo is installed:

```
cargo --version
```

#### Creating a Project with Cargo

```
cargo new hello_cargo
# You can override an existing Git repository
cargo new --vcs=git hello_cargo
```

#### Building and Running a Cargo Project

```
# Build your project
cargo build
# Run the executable
./target/debug/hello_cargo
# Compile the code and then run the resultant executable
cargo run
# This command quickly checks your code to make sure it compiles but doesn't produce an executable
cargo check
```

#### Building for Release

This command will compile the code with optimizations and create an executable in target/release instead of target/debug.

```
cargo build --release
```
