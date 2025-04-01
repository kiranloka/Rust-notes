#ownership #rust #beginner 

What are the Stack and Heap?

The stack and heap are two regions of memory that programs use to store data, each with distinct characteristics:

1. Stack
    
    - Fast: Memory allocation and deallocation are quick because it follows a Last-In-First-Out (LIFO) structure.
        
    - Fixed Size: Data must have a known, fixed size at compile time.
        
    - Scope-Based: Variables are automatically cleaned up when they go out of scope.
        
    - Used For: Local variables, function call frames, and small, simple data like integers or booleans.
        
2. Heap
    
    - Flexible: Memory can be allocated and deallocated dynamically, with sizes determined at runtime.
        
    - Slower: Allocation requires finding a suitable block of memory, and deallocation isn’t automatic (except in Rust, thanks to ownership).
        
    - Persistent: Data persists until explicitly dropped or moved.
        
    - Used For: Dynamic data like String, Vec, or anything with a variable size.
        

In Rust, the ownership system governs how data on both the stack and heap is managed, ensuring memory safety without a garbage collector.

---

How Rust Uses Stack and Heap

- Stack: Rust puts simple, fixed-size types (e.g., i32, bool, or structs with known sizes) on the stack. When you assign or pass these values, they’re copied (if they implement the Copy trait) because stack operations are cheap.
    
- Heap: Rust uses the heap for dynamic data (e.g., String, Vec), which are managed through pointers on the stack. The pointer (e.g., a String’s memory address) lives on the stack, but the actual data it points to lives on the heap. When ownership moves, only the pointer moves, not the heap data.
    

---

Ownership and Stack vs. Heap

- Stack Data: When a stack variable goes out of scope, it’s popped off automatically. For Copy types, this is trivial since copies are independent.
    
- Heap Data: When a heap-allocated value’s owner goes out of scope, Rust calls its drop method to free the heap memory. If ownership moves (e.g., let s2 = s1), the stack pointer moves to the new owner, and the old variable is invalidated—no heap copy occurs.
    

---

Example in Rust

Here’s how stack and heap interact:

rust

```rust
fn main() {
    // Stack: Fixed-size integer
    let x = 42;         // x is on the stack, copied if assigned
    let y = x;          // y gets a copy of 42, both x and y are valid
    println!("{}, {}", x, y);

    // Heap: Dynamic String
    let s1 = String::from("Hello"); // s1 on stack (pointer), "Hello" on heap
    let s2 = s1;                    // s2 takes ownership, s1 invalidated
    // println!("{}", s1);          // Error: s1 no longer owns the heap data
    println!("{}", s2);             // s2 owns the heap data
} // s2 goes out of scope, heap memory for "Hello" is freed
```

- x and y are stack-allocated integers; y = x copies the value.
    
- s1 is a String with a stack-allocated pointer to heap data; s2 = s1 moves the pointer, not the heap data.