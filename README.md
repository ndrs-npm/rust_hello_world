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
1. Install Rust using `apt`:

    ```bash
    sudo apt update
    sudo apt install -y rustc cargo
    ```

    This will install Rust and Cargo, the package manager and build tool for Rust, using the `apt` package manager.

    > Alternatively, you can use the Rust installation script:
    >
    >```bash
    >curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    >```
    >
    >- When prompted, choose the default option `(1)` to proceed with the installation.
    >- Wait for the installation to complete. This may take a few minutes depending on your internet connection.
    >- Once the installation is finished, you'll see a message indicating that Rust is installed and ready to use.

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

___

## Cross-Compilation Guide

This guide will walk you through cross-compiling a Rust program from an x86-64 machine to an ARM64 (aarch64) Linux target.

### Discalimer: Testing Environment

This guide has been tested on the following setup:

- Host Machine: x86-64 running Windows Subsystem for Linux (WSL) with Debian 11 (bullseye)
- Target Machine: aarch64 running Debian 11 (bullseye)

While the instructions should work on most x86-64 machines, you may need to adjust certain steps based on your specific setup.

### Prerequisites

- An x86-64 machine with Rust already installed and working
- Basic Rust project (hello world) already created and tested

### Steps to Cross-Compile

1. Install the ARM64 toolchain:

    For Debian-based systems (including Ubuntu), you can install the cross-compiler using apt:

    ```bash
    sudo apt update
    sudo apt install -y gcc-aarch64-linux-gnu
    ```

    > Make sure that the toolchain is installed correctly by running `aarch64-linux-gnu-gcc --version`.
    > If you installed the compiler via apt, it should already be in your PATH. Otherwise, add the cross-compiler's `bin` directory to your system's PATH:

1. In your existing Rust project directory, create a new folder named `.cargo` and create a configuration file named `config.toml` inside it:

    ```bash
    mkdir -p .cargo
    touch .cargo/config.toml
    ```

1. Edit the configuration file `.cargo/config.toml` and add the following lines to specify the linker for the ARM64 target:

    ```toml
    [target.aarch64-unknown-linux-gnu]
    linker = "aarch64-linux-gnu-gcc"
    ```

1. Add the ARM64 target to the Rust toolchain:

    ```bash
    rustup target add aarch64-unknown-linux-gnu
    ```

    > For a list of available targets, you can run `rustup target list`.

1. Cross-compile your Rust project for ARM64:

    ```bash
    cargo build --target aarch64-unknown-linux-gnu --release
    ```

    This command will compile your project for the ARM64 target and create a release build in the `target/aarch64-unknown-linux-gnu/release/` directory.

1. Transfer the compiled binary to the ARM64 machine:

    You can use any method to transfer the binary to the ARM64 machine, but in this example, we'll use `scp` to copy the binary over SSH to the ARM64 machine.

    ```bash
    scp target/aarch64-unknown-linux-gnu/release/hello_world user@arm64-machine:/path/to/destination
    ```

    > Replace `user@arm64-machine` with your ARM64 machine's SSH username and address, and `/path/to/destination` with the desired location on the ARM64 machine.

1. Run the binary on the ARM64 machine:

    **On your ARM64 machine**, navigate to the directory where you copied the binary and run it:

    ```bash
    ./hello_world
    ```

Congratulations! You've successfully cross-compiled your Rust program from an x86-64 machine to ARM64 Linux. This process can be adapted for other target platforms by changing the target triple and using appropriate toolchains. Always test your cross-compiled binary on the target system to ensure compatibility.
