# Local variables
Local variables start with a lowercase letter and are declared when they are first assigned a value. A variable name can start with an underscore `_`, but as these names are reserved for the compiler, it is not recommended to start a variable name with an underscore.
```
animal = "Cat"
age = 3
```

The variable type depends on its usage and not only from their initializer, thus it doesn't need to have a type specified. Usually, a variable is a value holder associated with the type it is expected to have according to its location and usage within the program. So if a variable is reassigned with a different expression it will inherit that expression's type instead.
`animal = "Cat" #=> animal is a String type`
`animal = 4 #=> animal is an Int32 type`
