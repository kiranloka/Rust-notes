#intermediate #rust #strings #text-procesing

Strings and text processing in Rust , a language known for its performance and safety guarantees.

### Strings in Rust :The Basic

- **String**
  - A growable,heap-allocated UTF-8 encoded string.
  - Owned,mutable,and managed by Rust's ownership system
- **&str**
	- An immutable , borrowed reference of a string
	- Typically a view into a String or a string literal 

String can be modified 
&str is a read-only and often used as a function parameter

### Common Text processing operations

1. Creating String

	```rust
	let s1:&str="hello,Rust";
	let s2:&str=String::from("Hello Rust!");

	let s3:String="hello rust".to_string();
	let mut s4 = String::new();
```

2. Concatenation

```rust
	let mut s= String::from("Hello");
	s.push_str(",Rust!");
```

Using + command consumes left operand

```rust
	let s1=String::from("hello");
	let s2=String::from("Rust");
	let s3 = s1+&s2;
```

Using format!

```rust
let s1="Hello"
let s2="Rust"
let s3=format!("{}{}!",s1,s2);
```


3. Accessing different characters and slices

Iterate over characters

```rust 
let s= String::from("hello,rust");
for c in s.chars(){
	println!("{}",c);
}

```

Iterate over bytes

```rust
for b in s.bytes(){
	println!("{},b");
}
```

Substring (via slicing)

```rust
let s="hello world"
let slice=&s[0..5];
```


4. Searching and Replacing
```rust
	let s= "Hello, Rust!";
	if s.contains("Rust"){
		println!("Found Rust!");
	}
```

```rust

	let s= String::from("Hello,Rust! Rust rocks!");
	let new_s=s.replace("Rust","World");
	println!("{}",new_s);
```

5. Splitting

```rust

let s= "Hello Rust world!";
let words:Vec<&str>=s.split_whitespace().collect();
println!("{:?}",words);
```

