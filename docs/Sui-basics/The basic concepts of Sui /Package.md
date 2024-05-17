---
id: tbcos_package
sidebar_position: 2
title: Package
---

# What is Package ? 
The main unit of move code organization is **Package**. 

A package is published on the blockchain and is identified by an [address](https://move-book.com/concepts/address.html).  It consists a set of **modules.** To understand the **package** in Sui, I divide the contents into elements:

- Package Layout
- Published Package
- Manifest Structure( Move.toml )
- Usage and Artifact

##  Package Layout
The Package consists of modules that contain functions, types, and other items.

```jsx
package HELLO_WORLD
    module a
        struct A1
        fun hello_world()
    module b
        struct B1
        fun hello_package()
```

To create a new package, use the `sui move new <NAME_package>` command. To learn more about the command, run `sui move new --help`.

The Move package system's purpose is to allow developers to easily define a package containing Move code. It also enables a package to be parameterized by [named addresses](https://move-book.com/reference/primitive-types/address.html). Moreover, it allows the import and use of packages in other Move code and the instantiation of named addresses.

## Published Package

A package, when published on-chain, is identified by an address. During development, the package doesn't have an address and must be set to `0x0`.

Once a package is published, the package receives a unique [address](https://move-book.com/concepts/address.html) on the blockchain, which contains its modules bytecode. Once published, a package becomes _immutable_ and can interact with transactions.
```
0xHELLO_WORLD
    my_module: <bytecode>
    another_module: <bytecode>
   
```


## Manifest Structure (Move.toml)

A Move package source directory contains a `Move.toml` package manifest file. This `Move.toml` file, referred to as the "package manifest," includes metadata about the package.

A typical package looks like this:
![Example the move project](/img/the_move_project.png)


The structure of a Move project is detailed in the graph below:

- The root of the project is `Your_Move_Project`. This serves as the foundation from which all other files and folders stem, providing the base for your Move project.
- Directly under `Your_Move_Project`, there are three critical components: `Move.toml`, `Move.lock`, and a directory named `sources`. These play essential roles in the project's configuration and organization.
- `Move.toml` and `Move.lock` are responsible for managing dependencies and ensuring a stable environment for your Move project.
- The `sources` directory is where you'll find the `module.move` file. This file is where the core logic of your Move code resides. It's the heart of your project, where you'll be spending most of your coding time.
- In addition to these, there is also a directory named `tests` located under `Your_Move_Project`. This directory is where you'll put all your test cases for your Move code, ensuring that your project runs as expected and helping you maintain a high-quality codebase.

This structure is designed to efficiently organize the project's code, making it easier for you to navigate and manage as your Move project grows in complexity. However, the structure isn't complete. It also includes doc_templates and examples, further enhancing the overall structure of the project.

```TOML
Your_Move_Project
├── Move.toml      (required)
├── Move.lock      (generated)
├── sources        (required)
├── doc_templates  (optional)
├── examples       (optional, test & dev mode)
└── tests          (optional, test mode)
```

To successfully build a Move package, there are certain directories and files, tagged as "required," that must be present. Additionally, there are optional directories that may be included in the build process depending on the mode in which the package is being built. For instance, when the package is being built in "development" or "test" modes, the `tests` and `examples` directories are also included in the compilation process.


Let's break down each part:

1. `Move.toml` file: This is like the ID  of the package. It tells the system what the package is and what it needs to work properly. Without it, the package can't be identified.
2. `Move.lock` file: This file is made by the Move CLI. It keeps track of the versions of the package and its needs. It's like a diary for your package, recording any changes made.
3. `sources` directory: This is where the Move modules, the building blocks of the package, are stored. They're always involved in the package creation process.
4. `doc_templates` directory: This is a place for documentation templates. If given, they will be used when making documentation for the package.
5. `examples` directory: Here, you can store extra code for development or tutorials. It's a great place for developers to try things out and learn.
6. `tests` directory: This is where you can put test modules. These are only used when the package is in 'test' mode. It's for making sure your package is working properly and catching problems early.


The example below features the "Hello World" package project:

```TOML title="Hello world move.toml"
[package]
name = "helloworld"
edition = "2024.beta" # edition = "legacy" to use legacy (pre-2024) Move
# license = ""           # e.g., "MIT", "GPL", "Apache 2.0"
# authors = ["..."]      # e.g., ["Joe Smith (joesmith@noemail.com)", "John Snow (johnsnow@noemail.com)"]

[dependencies]
Sui = { git = "https://github.com/MystenLabs/sui.git", subdir = "crates/sui-framework/packages/sui-framework", rev = "framework/testnet" }

# For remote import, use the `{ git = "...", subdir = "...", rev = "..." }`.
# Revision can be a branch, a tag, and a commit hash.
# MyRemotePackage = { git = "https://some.remote/host.git", subdir = "remote/path", rev = "main" }

# For local dependencies use `local = path`. Path is relative to the package root
# Local = { local = "../path/to" }

# To resolve a version conflict and force a specific version for dependency
# override use `override = true`
# Override = { local = "../conflicting/version", override = true }

[addresses]
helloworld = "0x0"

# Named addresses will be accessible in Move as `@name`. They're also exported:
# for example, `std = "0x1"` is exported by the Standard Library.
# alice = "0xA11CE"

[dev-dependencies]
# The dev-dependencies section allows overriding dependencies for `--test` and
# `--dev` modes. You can introduce test-only dependencies here.
# Local = { local = "../path/to/dev-build" }

[dev-addresses]
# The dev-addresses section allows overwriting named addresses for the `--test`
# and `--dev` modes.
# alice = "0xB0B"

```

I will explain each section in Move.toml and why you should consider it when starting a new project in Sui Move.
### Move.toml 

The primary number of sections in the manifest: 


- `[package]` : The first section in [Move](http://Move.ml).toml file. In the metadata for [package], we have some elements:
    
```jsx
[package]
name = <string>
edition* = <string> # "2024.alpha" to use the Move 2024 edition,
license* = <string>   # e.g., "MIT", "GPL", "Apache 2.0"
authors* = [<string>,+]  # e.g.,["Hien Phan([phanhoangvinhhien@gmail.com](mailto:phanhoangvinhhien@gmail.com))", "Phu Qui([phuqui@gmail.com](mailto:phuqui@gmail.com))"].

# Additional fields may be added to this section by external tools.
published-at* = "<hex-address>
```

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The explain elements  this 
<!-- <Tabs groupId="operating-systems">
  <TabItem value="name" label="name">This is the name of your package, created by the Sui Move compiler.</TabItem>
  <TabItem value="Edition" label="Edition*">This allows you to choose the version of Move for your code. The default for all new Move packages will be `edition = "2024"`.
  :::warning
  Features released under `alpha` will be unstable! Each time you update the compiler, code with `edition = "2024.alpha"` may fail to compile, even if it previously did.  You can read it in the [sui developer Road map 2024](https://arc.net/l/quote/fxwvuxaq) 
  :::
  </TabItem>
  <TabItem value="License*" label="License*">This allows you to choose the version of Move for your code. The default for all new Move packages will be `edition = "2024"`.</TabItem>
  <TabItem value="Edition" label="Edition">This allows you to choose the version of Move for your code. The default for all new Move packages will be `edition = "2024"`.</TabItem>
</Tabs>
 -->



<Tabs>
  <TabItem value="name" label="name" default>
   This is the name of your package, created by the Sui Move compiler.
  </TabItem>
  <TabItem value="Edition*" label="Edition*">
    This is an orange 🍊
  </TabItem>
  <TabItem value="License*" label="License*">
    This is a banana 🍌
  </TabItem>
  <TabItem value="authors*" label="authors*">
    This is a banana 🍌
  </TabItem>
  <TabItem value="published-at*" label="published-at*">
    This is a banana 🍌
  </TabItem>

</Tabs>








   






- License* = `<string>` This is optional. Choose, for example, "MIT", "GPL", "Apache 2.0".
- Version* = `<string>` The version you need. For instance, `version = "0.0.1"`.
- Authors* = `[<string>,+]` This indicates the author of the contract. The `+` means you can add more. For example: ["Hien Phan([phanhoangvinhhien@gmail.com](mailto:phanhoangvinhhien@gmail.com))", "Phu Qui([phuqui@gmail.com](mailto:phuqui@gmail.com))"].
- Published-at* = `<hex-address>`: This is a special field. *# The address where the package is published. It should be set after the first publication.*