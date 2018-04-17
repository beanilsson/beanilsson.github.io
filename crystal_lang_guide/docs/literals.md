# Literals
This is a list of all Crystal literals.

## Nil
**Sample value:** `nil`
**Details:** Represents the absence of a value. Nil only has one possible value as listed above.
## Bool
**Sample values:** `true`, `false`
**Details:** Bool only has two possible values as listed above.
## Integers
**Sample values:** `-3, 6, 19_i64, 14_u32,64_u8`
**Details:** An integer literal consists of an optional + or -, followed by a series of digits and optional underscores, optionally followed by a suffix. There are four signed integer types and four unsigned integer types.

| Type          | Length        | Min value      | Max value     |
| ------------- | ------------- | -------------- | ------------- |
| Int8          | 8             | -128           | 128           |
| Int16         | 16            | −32,768        | 32,768        |
| Int32         | 32            | −2,147,483,648 | 2,147,483,648 |
| Int64         | 64            | −2^63          | 2^63-1        |
| UInt8         | 8             | 0              | -255          |
| UInt16        | 16            | 0              | 65,535        |
| UInt32        | 32            | 0              | 4,294,967,295 |
| UInt64        | 64            | 0              | 2^64 - 1      |

If the suffix is omitted, the literal's type is automatically set to the lowest between Int32, Int64 and UInt64.
```
1 #=> Int32
1_i8 #=> Int8
1_u8 #=> UInt8
+15 #=> Int32
-15 #=> Int32
2147483648 #=> Int64
9223372036854775808 #=> UInt64
```
The underscore before the suffix is optional, and it is used by some to make the number more readable: `500_000_000`.
* Binary numbers starts with `0b`, `0b1101 #=> 13`
* Octal numbers start with `0o`, `0o123 #=> 83`
* Hexadecimal numbers start with `0x`, `0xFE012D #=> 16646445`
## Floats
**Sample values:** `-1.6, 5, 1.0_f32, 1e10`
**Details:** In Crystal there are two floating point types; `Float32` and `Float64` which both correspond to the binary32 and binary64 types as defined by IEEE. A floating point literal consists of an optional + or -, followed by a series of digits and optional underscores, optionally followed by a exponent suffix, optionally followed by a type suffix. If the suffix is omitted, the literal's type is automatically set to Float64.
```
1.0 #=> Float64
1.0_f32 #=> Float32
1_f32 #=> Float32
1e10 #=> Float64
1.5e10 #=> Float64
1.5e-7 #=> Float64
+1.3 #=> Float64
-0.5 #=> Float64
```
The underscore before the suffix is optional, and it is used by some to make the number more readable: `123_456.789_000`.
## Char
**Sample values:** `'a', '\t', 'ö'`
**Details:** A Char represents a 32-bit Unicode code point, and a char literal is usually created by enclosing an UTF-8 character within single quotes. Like so:
```
'a'
'b'
'0'
'ö'
'+'
```
Backslash gives us the option of using escape sequences, and numerical representations of unicode codepoints. These are the available escape sequences:
```
'\'' #=> single quote
'\\' #=> backslash
'\b' #=> backspace
'\e' #=> escape
'\f' #=> form feed
'\n' #=> newline
'\r' #=> carriage return
'\t' #=> tab
'\v' #=> vertical tab
'\uNNNN' #=> hexadecimal unicode character
'\u{NNNN...}' #=> hexadecimal unicode character
```
The format for unicode codepoints is as follows:
```
'\u0041' #=> 'A'
'\u{41}' #=> 'A'
'\u{1F52E}' #=> '&#x1F52E;'
```
## String
**Sample values:** `"Hello World!"`
**Details:** The string literal is an immutable series of UTF-8 characters enclosed within double quotes, like so:
```
"This is a string literal."
```
Backslash gives us the option of using escape sequences, and numerical representations of unicode codepoints. These are the available escape sequences:
```
"\"" #=> double quote
"\\" #=> backslash
"\b" #=> backspace
"\e" #=> escape
"\f" #=> form feed
"\n" #=> newline
"\r" #=> carriage return
"\t" #=> tab
"\v" #=> vertical tab
"\NNN" #=> octal ASCII character
"\xNN" #=> hexadecimal ASCII character
"\uNNNN" #=> hexadecimal unicode character
"\u{NNNN...}" #=> hexadecimal unicode character
```
All other characters trailing a backslash is interpreted as the character itself.

A backslash followed by no more than three digits, denotes a code point written in octal format:
```
"\101" # => "A"
"\123" # => "S"
"\12"  # => "\n"
"\1"   # string with one character with code point 1
```
The format for unicode codepoints is as follows:
```
"\u0041" # => "A"
"\u{41}" # => "A"
"\u{1F52E}" # => "&#x1F52E;"
```
Last but not least, one curly brace can contain multiple unicode characters each separated by a whitespace.
```
"\u{48 45 4C 4C 4F}" # => "HELLO"
```
### Interpolation
To embed expressions within a string, interpolation can be used.
```
name = "Floofkins"
age = 2
"Animal info: #{name} is #{age} years old."  #=> "Floofkins is 2 years old."
```
Any expression can be interpolated, but it’s recommended to keep them as small as possible for readability's sake.
It is possible to disable interpolation by escaping the # character with a backslash or by using a non-interpolating string literal like %q().
```
"\#{a + b}"  # => "#{a + b}"
%q(#{a + b}) # => "#{a + b}"
```
### Percent string literals
It is also possible to use string literals indicated by a `%` and a pair of delimiters; `(), [], {}, <>, ||` All delimiters, except for `||` can be nested.
```
%(hello ("world")) # => "hello (\"world\")"
%[hello ["world"]] # => "hello [\"world\"]"
%{hello {"world"}} # => "hello {\"world\"}"
%<hello <"world">> # => "hello <\"world\">"
%|hello "world"|   # => "hello \"world\""
```
A literal preceeded by %q does not invoke interpolation or escapes, while %Q has the same meaning as %.
```
name = "world"
%q(hello \n #{name}) # => "hello \\n \#{name}"
%Q(hello \n #{name}) # => "hello \n world"
```
### Multiline strings
A string literal can span multiple lines.
```
"Cats
      are awesome" #=> "Cats\n      are awesome"
```
To avoid including new lines, trailing and leading spaces within the string, it can be split into multiple lines by joining multiple literals with a backslash.
```
"Cats " \
"are " \
"awesome" #=> "Cats are awesome"
```
or
```
"Cats \
     are \
     awesome" #=> "Cats are awesome"
```
### Heredoc
Heredocs can also be used to write strings across multiple lines. Read more about them [here.](https://crystal-lang.org/docs/syntax_and_semantics/literals/string.htm)
## Symbol
**Sample values:**
```
:hello
:"123"
:"cats are awesome"
```
**Details:**
Symbols are constants, identified by a name without having to give them a numeric value. Internally a symbol is represented as an Int32. They can't be dynamically created.
## Array
**Sample values:** `[1, 2, 3]`, %w(one two three)
**Details:** Arrays are ordered and integer-indexed generic collections of a specific type `T`. They are usualy created using an array literal defined by `[]` and elements separated by `,`.
### Generic Type Argument
The elements within the literal decide the array's generic type argument `T`. If all elements are of the same type, `T` will equal to that, if the elements are of different types, `T` will be a union of all those types.
```
[1, 2, 3] #=> Array(Int32)
[1, "hello", 'x'] #=> Array(Int32 | String | Char)
```
It is possible to explicitly specify a type by adding the keyword `of` and the desired type. For example: ``


An explicit type can be specified by immediately following the closing bracket with of and a type, each separated by whitespace. This overwrites the inferred type and can be used for example to create an array that holds only some types initially but can accept other types later.

array_of_numbers = [1, 2, 3] of Number  # => Array(Number)
array_of_numbers + [0.5]                # => [1, 2, 3, 0.5]

array_of_int_or_string = [1, 3, 4] of Int32 | String  # => Array(Int32 | String)
array_of_int_or_string + ["foo"]                      # => [1, 2, 3, "foo"]

Empty array literals always need a type specification::

[] of Int32  # => Array(Int32).new
