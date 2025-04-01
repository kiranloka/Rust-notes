#beginner #rust #ownership

Ownership in rust is for managing memroy safety and efficiently without a garbage collector. It's build around the core rules

- Each value in rust has an owner
- There can be only one owner at a time
- When the owner goes out of scope the value is dropped Rust automatically frees the memory when the owning variable is no longer accessible

### Why ownership matters

In languages like C or C++ with malloc and free which can lead to errors . In garbage collected language like Python or Java the runtime handles memory,but this adds overhead. Rust ownership model avoids both issues:
- No memory management done manually
- No garbage collector overhead
- Compile-time checks the catch mistakes before runtime

### Key concepts Related to Ownership

1. Scope: A variable owns its value only within the scope when scope ends the value is dropped
2. Moving: When you assign a value to another variable or pass it to a function ownership transfers to new owner , and the old variable can't be used
3. Copying: Simple types are copied instead of moved because they're cheap an live on the stack 
4. Borrowing : You can lead access to a value without transferring ownership 


```rust
fn main() {
    let s1 = String::from("Hello"); // s1 owns the String
    let s2 = s1;                    // Ownership moves to s2; s1 is invalidated
    // println!("{}", s1);          // Error! s1 no longer owns the value
    println!("{}", s2);             // Works fine, s2 is the owner
}                                   // s2 goes out of scope, memory is freed
```