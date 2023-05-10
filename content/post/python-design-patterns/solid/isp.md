---
title: "Interface Segregation Principle"
date: 2023-05-09T09:56:52+05:30
draft: False
---

The Interface Segregation Principle (ISP) states that clients should not be forced to depend on interfaces they do not use.

## Example - 1 [ Violation ]

```
class Animal:
    def move(self):
        pass

    def eat(self):
        pass

    def swim(self):
        pass


class Fish(Animal):
    def move(self):
        print("Swimming")

    def eat(self):
        print("Eating underwater")

    def swim(self):
        print("Swimming")


class Bird(Animal):
    def move(self):
        print("Flying")

    def eat(self):
        print("Eating insects")

    def swim(self):
        raise NotImplementedError()


class Client:
    def __init__(self, animal):
        self.animal = animal

    def move_animal(self):
        self.animal.move()

    def feed_animal(self):
        self.animal.eat()

    def swim_animal(self):
        self.animal.swim()


# Usage
fish = Fish()
bird = Bird()

fish_client = Client(fish)
bird_client = Client(bird)

fish_client.swim_animal() # Expected output: "Swimming"
bird_client.swim_animal() # Raises NotImplementedError
```

In this example, we have an Animal interface that defines three methods: move, eat, and swim. The Fish and Bird classes implement the Animal interface. `The Fish class implements all three methods, while the Bird class implements only move and eat`.

The Client class depends on the Animal interface, but it doesn't require all the methods defined in the interface. `The swim method is not relevant for birds, so it raises a NotImplementedError`.

This violates the Interface Segregation Principle because the `Animal interface is too broad and forces clients to depend on methods they don't need`. In this case, the Bird class is forced to implement a method it doesn't need.

In order to make this principle non-violating, we could create separate interfaces for `Swimmable, Flyable, and Eatable`, and let the clients depend on the specific interfaces they require.


## Example - 2 [ Non-Violation ]

```
from abc import ABC, abstractmethod


class Moveable(ABC):
    @abstractmethod
    def move(self):
        pass


class Eatable(ABC):
    @abstractmethod
    def eat(self):
        pass


class Swimmable(ABC):
    @abstractmethod
    def swim(self):
        pass


class Fish(Moveable, Eatable, Swimmable):
    def move(self):
        print("Swimming")

    def eat(self):
        print("Eating underwater")

    def swim(self):
        print("Swimming")


class Bird(Moveable, Eatable):
    def move(self):
        print("Flying")

    def eat(self):
        print("Eating insects")


class Client:
    def __init__(self, moveable_animal, eatable_animal=None, swimmable_animal=None):
        self.moveable_animal = moveable_animal
        self.eatable_animal = eatable_animal
        self.swimmable_animal = swimmable_animal

    def move_animal(self):
        self.moveable_animal.move()

    def feed_animal(self):
        if self.eatable_animal:
            self.eatable_animal.eat()

    def swim_animal(self):
        if self.swimmable_animal:
            self.swimmable_animal.swim()


# Usage
fish = Fish()
bird = Bird()

fish_client = Client(fish, fish, fish)
bird_client = Client(bird, bird)

fish_client.swim_animal()  # Expected output: "Swimming"
bird_client.swim_animal()  # No output (bird cannot swim)

```
