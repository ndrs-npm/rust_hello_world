# Installing Rust and Creating a Hello World Project on Debian

This tutorial will guide you through the process of installing Rust on Debian and creating a basic "Hello, World!" project. We'll start by verifying the operating system and then proceed with the Rust installation.

## Disclaimer: Testing Environment

This tutorial was tested on a specific environment:

- Operating System: Debian 11 (bullseye)
- Platform: Windows Subsystem for Linux (WSL)
- Architecture: x86-64

While the instructions should work on most Debian-based systems, you may encounter slight differences depending on your specific setup. If you're using a different environment, some steps might need to be adjusted.

## Installing Rust

Now that we've clarified the testing environment, let's proceed with installing Rust:

1. Open terminal.
1. Run the following command to download and run the Rust installation script:

    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

1. The script will start and present you with installation options. For most users, the default option `(1)` is suitable. *Press Enter* to proceed with the default installation.
1. Wait for the installation to complete. This may take a few minutes depending on your internet connection.
1. Once the installation is finished, you'll see a message saying that Rust is installed now.
1. To start using Rust, you need to reload your shell. You can do this by running:

    ```bash
    source $HOME/.cargo/env
    ```

    > Alternatively, you can close and reopen your terminal.

1. Verify that Rust is installed correctly by checking its version:

    ```bash
    rustc --version
    ```

    You should see the installed Rust version printed on the screen which similar to `rustc x.y.z (abcabcabc yyyy-mm-dd)`.

## Creating a Hello World Project

Now that Rust is installed, let's create a simple "Hello, World!" program:

1. Create a new Rust project using the following command:

    ```bash
    cargo new hello_world
    ```

    This command will create a new directory named `hello_world`. Inside this directory, you'll find the project configuration file `Cargo.toml` and the main Rust source file `main.rs`.

    ```plaintext
    hello_world/
    ├── Cargo.toml      # Project configuration file
    └── src/
        └── main.rs     # Main Rust source file
    ```

    > This `main.rs` file contains the default "Hello, World!" program.

1. Navigate into the project directory:

    ```bash
    cd hello_world
    ```

1. You can quickly test the project by running:

    ```bash
    cargo run
    ```

    This command will compile and run the project. You should see the output **`Hello, world!`** printed on the screen.

    Or you can build the project without running it:

    ```bash
    cargo build
    ```

    The compiled binary will be available in the `target/debug/` directory. You can run the binary directly by executing:

    ```bash
    ./target/debug/hello_world
    ```

Congratulations! You've successfully installed Rust and created a basic "Hello, World!" project on Debian. You're now ready to explore more complex Rust applications and libraries.
