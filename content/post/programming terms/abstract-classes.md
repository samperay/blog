---
title: "Abstract Classes"
date: 2023-05-09T10:30:25+05:30
draft: False
tags: ["programming_terms"]
---

Abstract classes are those classes that can't be instantiated directly, it would only serve as a blue print. They are always designed to be `subclassed` and they would contain `abstractmethod` that must be implemented by their subclass. 

## Example

```
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass
```

When you are trying to instantiated `animal=Animal()`, it would throw an error.

```Error: Can't instantiate abstract class Animal with abstract methods make_sound```

Now, you would have an subclass of `Animal` that uses an `abstractmethod` 

```
class Dog(Animal):
    def make_sound(self):
        print("Woof")

class Cat(Animal):
    def make_sound(self):
        print("Meow")

dog=Dog()
dog.make_sound() # Output: Woof

cat=Cat()
cat.make_sound() # Output: Meow
```