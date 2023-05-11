---
title: "Builder"
date: 2023-05-11T09:02:23+05:30
draft: False
---

The Builder pattern is a well-known pattern in Python world. It’s especially useful when you need to create an object with lots of possible configuration options.

## Example - 1 [ Violation ]

```
class Product:
    def __init__(self):
        self.name = None
        self.price = None
        self.quantity = None

    def set_name(self, name):
        self.name = name

    def set_price(self, price):
        self.price = price

    def set_quantity(self, quantity):
        self.quantity = quantity

    def display(self):
        print(f"Product: {self.name}, Price: {self.price}, Quantity: {self.quantity}")



class ProductBuilder:
    def __init__(self):
        self.product = Product()

    def set_name(self, name):
        self.product.set_name(name)

    def set_price(self, price):
        self.product.set_price(price)

    def set_quantity(self, quantity):
        self.product.set_quantity(quantity)

    def build(self):
        return self.product

# the Product class exposes its setters publicly, 
# allowing the client to directly set the attributes 
# instead of going through the builder.

# Usage
builder = ProductBuilder()
builder.set_name("Widget")
builder.set_price(9.99)
builder.set_quantity(10)
product = builder.build()
product.display()  # Output: "Product: Widget, Price: 9.99, Quantity: 10"
```

To fix this violation and adhere to the Builder Pattern, we need to encapsulate the construction process within the builder class and make the attributes private.

```
class Product:
	def __init__(self,name, price, quantity):
		self.name=name
		self.price=price
		self.quantity=quantity

	def display(self):
		print(f"Product: {self.name}, Price: {self.price}, Quantity: {self.quantity}")

class ProductBuilder:
	def __init__(self):
		self.name=None
		self.price=None 
		self.quantity=None

	def set_name(self,name):
		self.name=name
		return self 

	def set_price(self,price):
		self.price=price
		return self 

	def set_quantity(self,quantity):
		self.quantity=quantity
		return self

	def build(self):
		return Product(self.name,self.price,self.quantity)


#Usage 
builder=ProductBuilder()
product=builder.set_name("Widget").set_price(9.99).set_quantity(10).build()
product.display() #Output: "Product: Widget, Price: 9.99, Quantity: 10"

```

## Example - 2 
https://refactoring.guru/design-patterns/builder/python/example



