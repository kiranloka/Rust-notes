**ID**: 2025-04-0113:27  
**Tags**: #rust #learning  #enums #beginner #pattern-matching
**Related**: 

---

## Content
Enums allow you to define a type that can be one of several variants . Each variant can optionally hold data, making enums more flexible than enums 

- Are defined with the enum keyword
- Can have variants with no data, named data , or tuple like data
- Are tied to ownership(moving a enum moves its data)


## Code
```rust
enum Message {
    Quit,                    // No data
    Move { x: i32, y: i32 }, // Named fields (like a struct)
    Write(String),           // Tuple-like with one field
    ChangeColor(i32, i32, i32), // Tuple-like with multiple fields
}
```
