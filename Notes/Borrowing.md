A concept that builds directly on ownership and is key to understanding how Rust manages data access safely. 


### What is borrowing in Rust

Borrowing in rust is a mechanism for allowing temporary access to a value wihtour transferring ownership .Instead moving ownership or copying data


Borrowing comes with strict rules enforced by Rust’s compiler (the borrow checker):

1. You can have either one mutable reference (&mut) or any number of immutable references (&) to a value at a time, but not both simultaneously.
    
2. References must always be valid (no dangling pointers).


```rust
fn main() {
    let mut s = String::from("Hello"); // s owns the String

    // Immutable borrow
    let r1 = &s;         // Borrow s immutably
    let r2 = &s;         // Another immutable borrow is fine
    println!("{}, {}", r1, r2); // Both work

    // Mutable borrow
    let r3 = &mut s;     // Borrow s mutably
    r3.push_str(", world");     // Modify via mutable reference
    println!("{}", r3);  // Works

    // This would fail:
    // let r4 = &s;      // Error: can't borrow immutably while r3 (mutable) is active
}
```


```rust
fn main() {
    let mut s = String::from("Hello");
    {
        let r1 = &mut s; // Mutable borrow in inner scope
        r1.push_str(" there");
    } // r1 goes out of scope here
    let r2 = &s;       // Immutable borrow is now allowed
    println!("{}", r2); // "Hello there"
}
```