---
title: "Prototype"
date: 2023-06-06T08:10:58+05:30
draft: False
---

The Prototype design pattern is a creational design pattern that allows you to create new objects by cloning existing ones, rather than creating them from scratch.It promotes object reuse and reduces the need for subclassing

```
import copy

class Prototype:
    def clone(self):
        return copy.copy(self)

class Sheep(Prototype):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(f"Sheep: {self.name}, Age: {self.age}")

# Usage
original_sheep = Sheep("Shawn", 2)
original_sheep.display()  # Output: "Sheep: Shawn, Age: 2"

cloned_sheep = original_sheep.clone()
cloned_sheep.display()  # Output: "Sheep: Shawn, Age: 2"

cloned_sheep.name = "Dolly"
cloned_sheep.age = 3

cloned_sheep.display()  # Output: "Sheep: Dolly, Age: 3"
```

In this example, we have a Prototype base class that defines the clone() method. The clone() method makes use of the copy.copy() function from the copy module to create a shallow copy of the object. This creates a new instance of the same class and copies the attributes of the original object to the clone.

We can modify the cloned sheep's attributes independently. In the example, we change the cloned sheep's name to "Dolly" and age to 3. Calling the display() method on the cloned sheep shows the updated attribute values.

## Prototype using factory method

```
import copy

class AnimalPrototype:
    def clone(self):
        return copy.copy(self)

    def speak(self):
        pass

class Dog(AnimalPrototype):
    def speak(self):
        return "Woof!"

class Cat(AnimalPrototype):
    def speak(self):
        return "Meow!"

class AnimalFactory:
    def __init__(self):
        self.prototypes = {}

    def register_prototype(self, animal_type, prototype):
        self.prototypes[animal_type] = prototype

    def create_animal(self, animal_type):
        if animal_type in self.prototypes:
            return self.prototypes[animal_type].clone()
        else:
            raise ValueError("Invalid animal type")

# Usage
animal_factory = AnimalFactory()

dog_prototype = Dog()
animal_factory.register_prototype("Dog", dog_prototype)

cat_prototype = Cat()
animal_factory.register_prototype("Cat", cat_prototype)

dog = animal_factory.create_animal("Dog")
print(dog.speak())  # Output: "Woof!"

cat = animal_factory.create_animal("Cat")
print(cat.speak())  # Output: "Meow!"

```

In this example, we have the AnimalPrototype base class that serves as the prototype for creating animal objects. It defines the clone() method to create a shallow copy of the object using copy.copy().

The Dog and Cat classes inherit from AnimalPrototype and provide their own implementation of the speak() method.

The AnimalFactory class acts as a factory that registers and creates animal objects based on their types. It maintains a dictionary of registered prototypes. The register_prototype() method allows new prototypes to be registered with their respective animal types, and the create_animal() method creates a new animal object based on the requested type by cloning the corresponding prototype.

In the usage section, we create an instance of the AnimalFactory class. We then create instances of the Dog and Cat classes and register them as prototypes with their respective animal types using the register_prototype() method.

Finally, we use the create_animal() method of the factory to create instances of animals by specifying their types. The factory retrieves the corresponding prototype, clones it, and returns the cloned object.

By combining the Prototype and Factory Method patterns, we can create new animal objects by cloning existing prototypes, which promotes object reuse and avoids the need to create objects from scratch.

