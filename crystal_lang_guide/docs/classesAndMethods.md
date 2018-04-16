# Classes and methods
A class is a blueprint from which objects are created. Class names, as with all type names, starts with a capital letter.
```
class Animal
end
```

By calling `.new` we can create an instance of a class.
```
animal = Animal.new
```

In this case, `animal` is an instance of `Animal`. To try this out, create a file named `animal.cr`, and add the following code:
```
animal = Animal.new

puts animal

class Animal
end
```
And run it by entering `crystal animal.cr` in a terminal within the directory that you saved the file. The output should be something like this: `#<Animal:0x1d88fe0>`.

Now, to spice things up a bit, we're going to add some methods to our `Animal` class.
The `initialize` method is being called when using the `.new` and creating an instance of the class. What it does is setting the instance variable (more on those further on) `@name` to the value of the parameter `name`, and setting the instance variable `@age` to 0.
```
def initialize(name : String)
    @name = name
    @age = 0
end
```
If we run this code now, we will still end up with the same output as before. So we need to add two more methods and update how we instanciate our `Animal` class.
These methods make the value within our instance variables available to use on our instance of the `Animal` class and can be used as such: `animal.name` and `animal.age`.
```
def name
  @name
end

def age
  @age
end
```
To create a new animal we can now update our previous instanciation of our `Animal` class.
```
cat = Animal.new "Floofkins"
dog = Animal.new "Pluto"
```
And print them
```
puts cat.name #=> Floofkins
puts cat.age #=> 0

puts dog.name #=> Pluto
puts dog.age #=> 0
```
*Note: In Crystal parameters are required to have a type specified, more on that topic [here](typeInference.md).*
