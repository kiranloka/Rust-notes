# 202504011815 - Modules and Project Structure - 2025-04-0323:40
**ID**: 2025-04-0323:40  
**Tags**: #rust #learning  #intermediate #modules

**Related**: 

---

## Content

Rust module system organises code into logical units, controlling visiblility and namespaces.Unlike JS esm or commonjs , Rust's modules are file-based and hierarchial, defined explicitly with mod, use and visibility keywords


1. **Module Declaration**
2. **Visibility(pub)**
3. **Using modules(use)**
4. **Paths**
5. **Nested Modules**

### File Based Modules
- By default, Rust looks for module files in specific locations:
    
    - mod my_module; in main.rs loads my_module.rs or my_module/mod.rs.
        
    - Example structure:
        
        ```text
        src/
        ├── main.rs
        ├── my_module.rs
        ```
        
        rust
        
        ```rust
        // src/main.rs
        mod my_module;
        
        fn main() {
            my_module::say_hello();
        }
        ```
        
        rust
        
        ```rust
        // src/my_module.rs
        pub fn say_hello() {
            println!("Hello!");
        }
        ```
        
- Submodules with mod.rs:
    
    ```text
    src/
    ├── main.rs
    ├── my_module/
    │   ├── mod.rs
    ```
    
    rust
    
    ```rust
    // src/main.rs
    mod my_module;
    
    fn main() {
        my_module::say_hello();
    }
    ```
    
    rust
    
    ```rust
    // src/my_module/mod.rs
    pub fn say_hello() {
        println!("Hello!");
    }
    ```
    

---


[[Project Structure in rust]]
