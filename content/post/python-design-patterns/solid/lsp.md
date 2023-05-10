---
title: "Liskov Substitution Principle"
date: 2023-05-07T18:02:32+05:30
draft: False
---

In this principle, if the program is using the base class, it should be able to work correctly with any derived class of that base class without needing to know the specific subclass. 

let's read using demo

## LSP Violation

we would calculate the area of `rectangle` and `square`. A rectable would have a `height` and `width` where as square would have all the sides as same so we would equate height=width and then calculate the result of the area. 

```
# Base class
class Rectangle:
    def __init__(self, width, height)
        self.width=width
        self.height=height

    def set_width(self,width):
        self.width=width 

    def set_height(self,height):
        self.height=height

    def area(self):
        return self.height * self.width

# Derived/subclass
class Square(Rectangle):
    # Override from the base class

    # This breaks the LSP principle, you can see the output
    def __init__(self,length):
        super().__init__(length,length)

    def set_width(self,width):
        self.width=width 
        self.height=height

    def set_height(self,height):
        self.height=height
        self.width = height

def print_area(rectangle):
    rectangle.set_width(5)
    rectangle.set_height(4)
    print("Area", rectangle.area())

rectangle=Rectangle(5,4) # Area: 20
square=Square(5) # Area: 16 
```

You might have seen the above square method, since its being overridden from the rectangle class, the value has been changed completely in violation of LSP. 

We would rectify now and see how we can use that prunciple. 

## With LSP

we would define the base class `shape` which can be overridden and calculates the area of the shape. 

```
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Shape):
    def __init__(self, length):
        self.side_length = length

    def area(self):
        return self.side_length**2

def print_area(shape):
    print("Area:", shape.area())

rectangle=Rectangle(5,3)
square=Square(5)

print_area(rectangle) # Output: Area: 15
print_area(square) # Output: Area: 25
```