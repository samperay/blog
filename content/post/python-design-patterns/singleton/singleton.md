---
title: "Singleton"
date: 2023-06-06T08:34:51+05:30
draft: False
---

The Singleton pattern is a creational design pattern that ensures that a class has only one instance and provides a global point of access to that instance.

```
class Singleton:
    _instance = None

    def __new__(cls):
        if not cls._instance:
            cls._instance = super().__new__(cls)
        return cls._instance

# Usage
singleton1 = Singleton()
singleton2 = Singleton()

print(singleton1 is singleton2)  # Output: True

```

## Singleton using decorator

```
def singleton(cls):
    instances = {}

    def wrapper(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]

    return wrapper

@singleton
class Singleton:
    def __init__(self, value):
        self.value = value

# Usage
singleton1 = Singleton(42)
singleton2 = Singleton(24)

print(singleton1 is singleton2)  # Output: True
print(singleton1.value)  # Output: 42
print(singleton2.value)  # Output: 42

```

In this example, we define a singleton decorator function. The decorator function takes a class as an argument and returns a wrapper function that manages the creation and storage of instances.

The wrapper function checks if an instance of the class exists in the instances dictionary. If not, it creates a new instance of the class and stores it in the dictionary. Subsequent calls to the wrapper function return the existing instance.

The @singleton decorator is then applied to the Singleton class. This means that whenever we create an instance of the Singleton class, it goes through the singleton decorator and returns the existing instance if it has already been created.

## Another example for decorator

```
def singleton(cls):
    instances={}

    def get_instance(*args,**kwargs):
        if cls not in instances:
            instances[cls]=cls(*args,**kwargs)
        return instances[cls]

    return get_instance


@singleton
class Database:
    def __init__(self):
        print("loading from the database")

d1=Database()
d2=Database()

print(d1 is d2) # Output: true
```
