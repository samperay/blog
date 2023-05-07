---
title: "Open Closed Principle"
date: 2023-05-07T10:38:24+05:30
draft: False
tags: ["Python Design Principle"]
---

The Open-Closed Principle (OCP) states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, the behavior of a software entity should be easily extended without modifying its source code.

Let's explain by example...

You have a products, and you need to filter the products.

## Without OCP

```
class Product:
    def __init__(self, name,size,color):
        self.name = name 
        self.size = size
        self.color = color
    
class ProductFilter:
    def filter_by_size(self,product,size):
        for p in products:
            if p.size == size: yield p 
```

Let's say you need to `filter_by_color` / `filter_by_color_and_size` / `filter_by_color_or_size`. In future, you have more parameters like "weight, height, thickness etc" .. you can't scale the class as such. 

Hence once you create a **class you would need to close the class for modifications and open for extension**.

```
apple = Product("Apple", COLOR.GREEN, SIZE.SMALL)
tree = Product("Tree", COLOR.GREEN, SIZE.LARGE)
house = Product("House", COLOR.BLUE, SIZE.MEDIUM)

products = [apple,tree,house]

pf = ProductFilter()
print('Green products (old):')
for p in pf.filter_by_color(products,COLOR.GREEN):
    print(f' - {p.name} is green')
```

## With OCP

You create a new functionality for `specifications` which satisfies the criteria for filtering. We would create a two base classes which can be used to override logic in future cases. 

```
# Base class
class Specification:
    def is_satisfied(self, item):
        pass

# Overide the base class and use your logic for 
# future application.

class ColorSpecification(Specification):
    def __init__(self, color):
        self.color = color

    def is_satisfied(self, item):
        return item.color == self.color

class SizeSpecification(Specification):
    def __init__(self, size):
        self.size = size

    def is_satisfied(self, item):
        return item.size == self.size

class HeightSpecifcation(Specification):
    pass 

class WeightSpecification(Specification):
    pass

```

We will create filter specification and override from this section. 

```
# Base class
class Filter:
    def filter(self, items, spec):
        pass


# Overrise the baseclass and use for your application/business logic.

class BetterFilter(Filter):
    def filter(self, items, spec):
        for item in items:
            if spec.is_satisfied(item):
                yield item
```

```
apple = Product("Apple", COLOR.GREEN, SIZE.SMALL)
tree = Product("Tree", COLOR.GREEN, SIZE.LARGE)
house = Product("House", COLOR.BLUE, SIZE.MEDIUM)

products = [apple,tree,house]

bf = BetterFilter()

print('Green products (new):')
green = ColorSpecification(COLOR.GREEN)
for p in bf.filter(products,green):
    print(f' - {p.name} is green')

print('Blue products (new):')
blue = ColorSpecification(COLOR.BLUE)
for p in bf.filter(products,blue):
    print(f' - {p.name} is blue')

print('Large products:')
large = SizeSpecification(SIZE.LARGE)
for p in bf.filter(products, large):
    print(f' - {p.name} is large')
```

Another example, 

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


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius**2


def calculate_total_area(shapes):
    total_area = 0
    for shape in shapes:
        total_area += shape.area()
    return total_area
```