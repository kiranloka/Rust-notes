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


### Pattern Matching

Pattern matching in Rust is a powerful feature that allows you to match values against patterns and execute code based on those matches. It's primary used with the match expression,but it also appears other constructs like if let while let, and function parameters. Let's break it down step by step 

```rust
enum Direction{
	North,
	South,
	East,
	West,
}

let dir=Direction::East;
match dir{
	Direction::North=>println!("Heading North"),
	Direction::South=>println!("Heading South"),
	Direction::East=>println!("Heading East"),
	Direction::West=>println!("Heading West")
}
```

. The match Expression

The match expression is the cornerstone of pattern matching in Rust. It’s similar to a switch statement in other languages but much more flexible. Here’s a basic example:

rust

```rust
fn main() {
    let number = 3;
    match number {
        1 => println!("One"),
        2 => println!("Two"),
        3 => println!("Three"),
        _ => println!("Something else"), // The underscore (_) is a wildcard
    }
}
```

- How it works: match compares number against each pattern (1, 2, 3, etc.) and executes the corresponding code block (=>).
    
- Exhaustiveness: Rust requires that match expressions cover all possible cases. The _ wildcard acts as a catch-all for unmatched values.
    
- Output: This prints "Three".
    

2. Matching Multiple Patterns

You can use the | operator to match multiple patterns in a single arm:

rust

```rust
let number = 5;
match number {
    1 | 3 | 5 | 7 | 9 => println!("Odd single digit"),
    2 | 4 | 6 | 8 => println!("Even single digit"),
    _ => println!("Something else"),
}
```

- Output: "Odd single digit".
    

3. Matching Ranges

Rust supports inclusive range patterns with ..=:

rust

```rust
let number = 42;
match number {
    0..=10 => println!("Between 0 and 10"),
    11..=50 => println!("Between 11 and 50"),
    _ => println!("Out of range"),
}
```

- Output: "Between 11 and 50".
    

4. Destructuring

with a tuple:

rust

```rust
let pair = (0, 5);
match pair {
    (0, y) => println!("x is 0, y is {}", y),
    (x, 0) => println!("x is {}, y is 0", x),
    (x, y) => println!("x is {}, y is {}", x, y),
}
```

- Output: "x is 0, y is 5".
    

5. Guards

You can add conditions to patterns using if:

rust

```rust
let number = 4;
match number {
    n if n > 0 => println!("Positive"),
    n if n < 0 => println!("Negative"),
    _ => println!("Zero"),
}
```

- Output: "Positive".
    

6. if let and while let

For simpler cases where you only care about one pattern, use if let:

rust

```rust
let some_value = Some(42);
if let Some(x) = some_value {
    println!("Got a value: {}", x);
} else {
    println!("Got nothing");
}
```

- Output: "Got a value: 42".
    

while let works similarly for loops:

rust

```rust
let mut stack = vec![1, 2, 3];
while let Some(top) = stack.pop() {
    println!("{}", top);
}
```

- Output: 3, 2, 1 (one per line).
    

7. Binding with @

You can bind a matched value to a name using @:

rust

```rust
let number = 7;
match number {
    n @ 1..=10 => println!("Number {} is between 1 and 10", n),
    _ => println!("Out of range"),
}
```

- Output: "Number 7 is between 1 and 10".
    

Key Points

- Safety: Rust ensures all patterns are exhaustive, preventing runtime errors from unmatched cases.
    
- Flexibility: Patterns can match literals, ranges, structs, enums, and more.
    
- Conciseness: Constructs like if let reduce boilerplate for single-case matches.
    

Pattern matching is one of Rust’s most expressive features, making code both safer and more readable. Want a specific example or deeper dive into any part? Let me know!