---
title: "Factory Method"
date: 2023-05-26T10:27:55+05:30
draft: False
---

Design pattern that provides an interface for creating objects, but allows `subclasess to decide which class to instantiate`. It provides loose coupling and flexibility in object creation. Factory Method pattern can be implemented using a base class or an abstract class and allowing subclasses to override a factory method

```
from abc import ABC, abstractmethod 

# Abstract class representing the product
class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

# Concrete class implementing the product
class Dog(Animal):
    def speak(self):
        return "Woof !"

class Cat(Animal):
    def speak(self):
        return "Meow !"

class Fox(Animal):
    def speak(self):
        return "foxxx!"

# Creator class with factory method. 
class AnimalFactory(ABC):
    @abstractmethod
    def create_animal(self)->Animal:
        pass 

class DogFactory(AnimalFactory):
    def create_animal(self):
        return Dog()

class CatFactory(AnimalFactory):
    def create_animal(self):
        return Cat()

class FoxFactory(AnimalFactory):
    def create_animal(self):
        return Fox()

# Usage

dog_factory=DogFactory()
dog=dog_factory.create_animal()
print(dog.speak()) # Output: Woof !

fox_factory=FoxFactory()
fox=fox_factory.create_animal()
print(fox.speak()) # Output: Foxx !
```

