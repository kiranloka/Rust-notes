**ID**: 2025-04-0416:54  
**Tags**: #rust #learning  #intermediate #error-handling
**Related**: 

---

## Content
Error handling in Rust is designed to be explicit , safe and ergonomic, leveraging the language's type system and ownership model. Unlinke languages that rely heavily on exceptions(like Java and python). Rust uses a combination of the Result and Option enums, along with powerful tools like the ? operator , to manage errors without runtime surprises .


### Core Concepts

1. Options enum

- used when a value might be absent 
- Some(T) (Contains a value of type T) or None(no value)

```rust 
fn find_first_a(s:&str)->Option<"char">{
	for c in s.chars(){
		if c=="a"{return Some(c);}
	}
	None
}

let result=find_first_a("hello");
match result{
	Some(val)=>println!("Found:{}",val);
	None=>prinln!("No 'a' found");
}
```

2. Result Enum

- Used in operations that might fail, returning eiter a success value or an error.
- Variants: Ok(T) (Success with value T) or Err(E)(failure with error E)

```rust 
fn divide(a:i32,b:i32)->Result<i32,String>{
	if b==0{
		Err(String::from("Division by 0"))
	}else{
		Ok(a/b)
	}
}

match divide(10,2){
	Ok(result)=>println!("Result:{}",result),
	Err(e)=>println!("Error:{}",e)
}
```


### Handling Errors

Rust encourages you to handle errors explicitly rather than letting them silently propagate. Here's how:

1. Match Expression
- The most straight forward way to handle Options and result
```rust
let result=divide(10,0);
match result{
	Ok(val)=>println!("Success:{}",val);
	Err(e)=>println!("Failed!:{}",e)
}
```


2. unwrap and expect

- Quick and dirty shortcuts to extract values, but they panic (crash ) on failure
- unwrap:Panics with a generic message
- expect: Panics with a custom message

```rust
let good = divide(10,2).unwrap();
let bad= divide(10,0).expect("Oh no!");
```


3. ? Operator

- a concise way to propogate errors up the call stack 
- Works in functions that return Result or Option: If the value is Err or None , it returns early, Otherwise , it unwraps the Ok or some

```rust
fn safe_divide(a:i32,b:i32)->Result<i32,String>{
	let result=divide(a,b)?;
	Ok(result*2);
}
println!("{:?}",safe_divide(10,0));
```

4. Combinators
- Methods like map,and_then and or_else allow funcional-style error handling

```rust
let result=divide(10,2)
	.map(|x|x*3)
	.unwrap_or(0);
println!("{}",result);
```




Philosophy of Rust Error Handling

- No Exceptions: Errors are values, not control flow jumps, making behavior predictable.
    
- Recoverable vs. Unrecoverable:
    
    - Recoverable errors use Result (e.g., file not found).
        
    - Unrecoverable errors use panic! (e.g., programmer mistakes like out-of-bounds access), though these are rare in well-written Rust.
        
- Type Safety: The compiler ensures you handle errors, reducing runtime surprises.

