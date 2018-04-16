# Type Inference
In Crystal, the goal is to have as few type annotations as possible, but there are some exceptions. If we have a class like this for example:
```
class Animal
  def initialize(@name)
    @age = 0
  end
end
```
It is clear to us, as programmers, that `@age` is an integer, while `@name` could be of any type. A compiler can assume the type by the variable's usage, but it is not wise to let it do so since when performing some compiler optimizations, like analyzing a method just once and incrimental compiltaion, will become almost impossible to perform. Also, a programmer would have to find all usages of the `@name` variable to be able to determine its type. The concrete impacts being, as the code base grow, more and more difficulty to understand a project as well as the compile times becoming longer and longer. Therefore we need to tell Crystal the types of instance and class variables. So how do we do that? Well, there are a few options!

## Using type annotations
The most obvious, yet probably the most tedious way.
```
class Animal
  @name : String
  @age : Int32

  def initialize(@name)
    @age = 0
  end
end
```
## Not using type annotations
If no type is explicitly declared, the compiler is going to try to infer the type of instance and class variables using some predefined syntactic rules. For a specific variable, if a rule can be applied and a type can be guessed, the type is added to a set. When no more rules can be applied, the inferred type will be a union of all those types. Also, if the compiler guess that an instance variable ins't always initialized it will include the `Nil` type as well. All of the following rules applies to both instance and class variables alike.

### Assigning a literal value
By assigning a literal to an instance variable, that literal's type is added to the set. All [literals](literals.md) have a type.


When a literal is assigned to an instance variable, the literal's type is added to the set. All literals have an associated type.
