# An in depth look at the compiler
*Note: If you are new to Crystal and/or programming, I recommend reading and understanding [the basics first](./index.md), before digging in to the details on this page.*
## Creating a dynamically-linked executable
The `build` command is used to create an executable file.
```
$ crystal build hello_world.cr
```
Which can then be run with the following command:
```
$ ./hello_world
```
These executables are not fully optimized however. To optimize them, use the `--release` flag. This flag should always be used for production ready executables and when performing benchmarks.
To decrease the binary size the `--no-debug` along with the `strip` command can be used.
## Creating a statically-linked executable (standalone)
Simply add the `--static` flag to the command.
```
$ crystal build hello_world.cr --release --static
```
And run it like a dynamically-linked executable.
```
$ ./hello_world
```
*Disclaimer! To create a standalone executable, all required libraries MUST be installed. A list of these libraries can be [found here.](https://github.com/crystal-lang/crystal/wiki/All-required-libraries)*
For all available commands, simply run `crystal` without any commands or flags in your terminal. For a list of options available on each command, add the `--help` flag after the command, e.g. `crystal build --help`.
The Crystal compiler supports the following input format: `crystal build [options] [programfile] [--] [arguments]`
