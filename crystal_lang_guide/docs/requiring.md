# Require files
While you can write all code within the same file, it is not very convinient to do so for many reasons I won't bring up here. To tell the Crystal compiler what other files to process, simply use the `require` macro. `require` takes a single argument, a string representing the file to be included. When a file is required, the compiler saves its absolute path. Thus, a file only has to be required once and every later inclution of that file will be ignored.

## How it works
### Require path
When using `require "some_file"`, the compiler will look up `some_file` in the require path. The require path is defaulted to the location of the standard library that comes with the compiler, and the lib directory relative to the current working directory.

When the compilation process is started, the following happens:
* A file named `some_file.cr` within the required path, will be required.
* A directory named `some_file` containing a file named `some_file.cr`, the file will be required. Regarding the typical structure of a project, see below, this feature is very handy.
* If none of the above conditions are met, a compile-time error will be issued.

*Typical project structure:*

```
- project
  - lib
    - foo
      foo.cr
    - bar
      bar.cr
  - src
    - project.cr
  - spec
    - project_spec.cr
```

### Relative
There is also the option of using `require "./some_file"`, which will look up the file some_file.cr relative to the file where the expression is used. This is mostly used to require files within the project, it is also used to refer to code from within specs.

When the compilation process is started, the following happens:
* A file named `some_file.cr` found relative to the current file will be required.
* A directory named `some_file` containing a file named `some_file.cr`, the file will be required.
* If none of the above conditions are met, a compile-time error will be issued.

### Other options
The possibility to use nested names is present for both the require path and when requiring relatively. For example:
* `require "foo/bar/baz"` will lookup "foo/bar/baz.cr" or "foo/bar/baz/baz.cr" in the require path.
* `require "./foo/bar/baz"` will lookup "foo/bar/baz.cr" or "foo/bar/baz/baz.cr" relative to the current file.

`../` is used to access parent directories relative to the current file. For example: `require "../foo"`.


For all of these cases, the special * and ** suffixes are available.
* `require "foo/*"` will require all ".cr" files below `/foo`, but not below directories inside `/foo`.
* `require "foo/**"` will require all ".cr" files below `/foo`, and below directories inside `/foo`.
