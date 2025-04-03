ust projects are organized as crates (either binaries or libraries), managed by Cargo, Rust’s build tool and package manager. This contrasts with Turborepo’s monorepo structure, where multiple apps and packages coexist. Let’s explore common layouts.

1. Single Binary Crate

- Purpose: A standalone executable (like http-backend).
    
- Structure:
    
    ```text
    my_project/
    ├── Cargo.toml
    ├── src/
    │   ├── main.rs
    ```
    
- Cargo.toml:
    
    toml
    
    ```toml
    [package]
    name = "my_project"
    version = "0.1.0"
    edition = "2021"
    
    [dependencies]
    ```
    
- src/main.rs:
    
    rust
    
    ```rust
    fn main() {
        println!("Hello, Rust!");
    }
    ```
    
- Build/Run:
    
    bash
    
    ```bash
    cargo build
    cargo run
    ```
    

2. Single Library Crate

- Purpose: A reusable library (like backend-common).
    
- Structure:
    
    ```text
    my_lib/
    ├── Cargo.toml
    ├── src/
    │   ├── lib.rs
    ```
    
- Cargo.toml:
    
    toml
    
    ```toml
    [package]
    name = "my_lib"
    version = "0.1.0"
    edition = "2021"
    ```
    
- src/lib.rs:
    
    rust
    
    ```rust
    pub fn say_hello() {
        println!("Hello from lib!");
    }
    ```
    
- Test:
    
    bash
    
    ```bash
    cargo test
    ```
    

3. Combined Binary and Library

- Purpose: A project with both an executable and a library (e.g., http-backend using backend-common locally).
    
- Structure:
    
    ```text
    my_project/
    ├── Cargo.toml
    ├── src/
    │   ├── main.rs
    │   ├── lib.rs
    ```
    
- Cargo.toml:
    
    toml
    
    ```toml
    [package]
    name = "my_project"
    version = "0.1.0"
    edition = "2021"
    ```
    
- src/lib.rs:
    
    rust
    
    ```rust
    pub fn say_hello() {
        println!("Hello from lib!");
    }
    ```
    
- src/main.rs:
    
    rust
    
    ```rust
    use my_project::say_hello;
    
    fn main() {
        say_hello();
    }
    ```
    

4. Workspace (Monorepo Equivalent)

- Purpose: Multiple crates in one repo, like Turborepo’s apps/ and packages/.
    
- Structure:
    
    ```text
    my_workspace/
    ├── Cargo.toml
    ├── backend_common/
    │   ├── Cargo.toml
    │   ├── src/
    │       ├── lib.rs
    ├── http_backend/
    │   ├── Cargo.toml
    │   ├── src/
    │       ├── main.rs
    ```
    
- Root Cargo.toml:
    
    toml
    
    ```toml
    [workspace]
    members = [
        "backend_common",
        "http_backend"
    ]
    ```
    
- backend_common/Cargo.toml:
    
    toml
    
    ```toml
    [package]
    name = "backend_common"
    version = "0.1.0"
    edition = "2021"
    ```
    
- backend_common/src/lib.rs:
    
    rust
    
    ```rust
    pub fn get_jwt_secret() -> String {
        String::from("my_secret")
    }
    ```
    
- http_backend/Cargo.toml:
    
    toml
    
    ```toml
    [package]
    name = "http_backend"
    version = "0.1.0"
    edition = "2021"
    
    [dependencies]
    backend_common = { path = "../backend_common" }
    ```
    
- http_backend/src/main.rs:
    
    rust
    
    ```rust
    use backend_common::get_jwt_secret;
    
    fn main() {
        println!("JWT Secret: {}", get_jwt_secret());
    }
    ```
    
- Build/Run:
    
    bash
    
    ```bash
    cd my_workspace
    cargo build --workspace
    cargo run -p http_backend
    ```
    

---

Connecting to Your Project

For excali-draw, you could structure a Rust backend like this:

- Workspace:
    
    - backend_common: Library with shared logic (e.g., JWT handling, Prisma-like DB access).
        
    - http_backend: Binary using axum for an HTTP server, depending on backend_common.
        
- Example:
    
    rust
    
    ```rust
    // backend_common/src/lib.rs
    pub fn get_jwt_secret() -> String {
        std::env::var("JWT_SECRET").unwrap_or(String::from("123123"))
    }
    ```
    
    rust
    
    ```rust
    // http_backend/src/main.rs
    use axum::{routing::get, Router};
    use backend_common::get_jwt_secret;
    
    #[tokio::main]
    async fn main() {
        let app = Router::new().route("/", get(|| async { get_jwt_secret() }));
        let listener = tokio::net::TcpListener::bind("0.0.0.0:3000").await.unwrap();
        axum::serve(listener, app).await.unwrap();
    }
    ```
    

---