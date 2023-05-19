---
title: "Property Decorator"
date: 2023-05-07T19:03:31+05:30
draft: False
tags: ["programming_terms"]
---

The @property decorator in Python is used to define methods that are accessed like attributes, providing a way to implement computed properties or control access to class attributes. It allows you to define a method that can be accessed as if it were an attribute, without the need to explicitly call it as a method.

```
class Circle:
    def __init__(self,radius):
        self.radius = radius

    @property
    def diameter(self):
        return self.radius

    @diameter.setter
    def diameter(self,value):
        if value > 0:
             self.radius=value

    @diameter.deleter
    def diameter(self):
        del self.radius

    @property
    def area(self):
        return 3.14 * self.radius**2

mycircle=Circle(2)
mycircle.diameter=10  # you can use method as an attribute.
print(mycircle.diameter)

print("setter")

mycircle.diameter=0  
print(mycircle.diameter) # Output: 10, since the value is set to 0, it would output the previous value associated in the object.

print("deleter")
del mycircle.diameter
print(mycircle.diameter)  # raise an exception as the circle object has deleted the 'radius' attribute

```


