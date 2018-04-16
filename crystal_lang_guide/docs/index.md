# Hello World!
```
puts "Hello World!"
```
That's it, that's how you write a Hello World program in Crystal. Pretty neat huh? But how do I run it? You might ask, well, come along and I'll show you!
*Note: I am writing this guide as I am learning Crystal myself. So I reserve the right to change and edit as much as I want as I learn more. Also, my primary resources are [the official documentation](https://crystal-lang.org/docs/) and [the official API](https://crystal-lang.org/api/0.24.2/) if nothing else is stated. The version I'm using is `0.24.2`, the latest version as of date.*
# Installing the Crystal Compiler
There are distributions available for a wide range of operating systems, below I shall list instructions for Debian and Ubuntu. For a complete list, or more installation details, [please refer to this page.](https://crystal-lang.org/docs/installation/)
## Debian and Ubuntu
First, add the repository to your APT config.
```
curl https://dist.crystal-lang.org/apt/setup.sh | sudo bash
```
And second, install the Crystal compiler.
```
sudo apt-get install build-essential -y // This command is not always needed, but better safe than sorry I guess
sudo apt-get install crystal -y
```
Done! You can check if your installation was successful by running:
```
crystal -v
```
It should display something along the lines of:
```
Crystal 0.24.2 [4f9ed8d03] (2018-03-08)
```
If you want to upgrade your Crystal version, run the following.
```
sudo apt-get update
sudo apt-get install crystal
```
## Crystal Box
I've created a Vagrant box with a Crystal installation for the ones, including myself, who are into that sort of thing. Which can be found [here](https://github.com/beanilsson/crystal_development).

# Using the Crystal Compiler
A Crystal file ends with `.cr`, and there are two ways to compile and run a Crystal program.
```
$ crystal hello_world.cr
```
and
```
$ crystal run hello_world.cr
```
The difference between these two are unbeknownst to me as of date.
For more details on the compiler and what it is capable of, [read this section!](./compilerDetails.md)
# Hello World pt.2
So, utilizing the information we've gathered up until now, we should now be able to create our Hello World program and run it!
Start by creating a file named `hello_world.cr`. Write `puts "Hello World!"` to the file and save it. Then, in your terminal, go to the directory where you saved the file, type $ crystal hello_world.cr and press enter.
After the compiler has done its magic, the text **Hello World!** should be visible in the terminal window.
Good job! You've just created and run your first Crystal program.

# Want more?
* An analysis of the [simple server example](helloServer.md).
* Read about [requiring files](requiring.md).
