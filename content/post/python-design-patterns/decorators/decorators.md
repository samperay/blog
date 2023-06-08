---
title: "Decorators"
date: 2023-06-07T10:12:27+05:30
draft: False
---

## Functional Decorators 

Function decorators in Python are a way to modify the behavior of a function without changing its source code. Decorators are implemented using the concept of higher-order functions, where a function takes another function as an argument and returns a modified version of it.

```
def uppercase_decorator(func):
    def wrapper():
        result = func()
        return result.upper()
    return wrapper

@uppercase_decorator
def say_hello():
    return "Hello, World!"

print(say_hello())  # Output: "HELLO, WORLD!"

```

In this example, we define a decorator function called `uppercase_decorator`. It takes a function (func) as an argument and returns a new function called wrapper. The wrapper function modifies the behavior of the original function by calling it and returning the result in uppercase.

Function decorators are commonly used in Python for various purposes, such as logging, timing, authentication, and data validation. They provide a clean and reusable way to modify the functionality of functions without modifying their original code.

## Classic Decorators

```
class TextComponent:
	def render(self):
		pass

class BaseTextComponent(TextComponent):
	def __init__(self,text):
		self.text = text 

	def render(self):
		return self.text

	def __str__(self):
		return f'rendering the text {self.text}'


class BoldDecorator(TextComponent):
	def __init__(self,text_component):
		self.text_component=text_component

	def render(self):
		base_text=self.text_component.render()
		return f"<b>{base_text}</b>"

class ItalicDecorator(TextComponent):
	def __init__(self,text_component):
		self.text_component=text_component

	def render(self):
		base_text=self.text_component.render()
		return f"<i>{base_text}</i>"

text="Hello world"
component = BaseTextComponent(text)
bold_decorator=BoldDecorator(component)
italic_decorator=ItalicDecorator(component)

print(bold_decorator.render()) # Output: <b>Hello world</b>
print(italic_decorator.render()) # Output: <i>Hello world</i>
```

In this example, we have the TextComponent abstract class, which defines the common interface for rendering text components.

The BaseTextComponent class is a concrete implementation of the TextComponent class. It represents the base text that can be rendered.

The BoldDecorator and ItalicDecorator classes are concrete decorators that inherit from the TextComponent class. They wrap around existing text components and provide additional functionality. Each decorator adds its own formatting tags (<b> for bold, <i> for italic) around the base text.

In the usage section, we create an instance of the BaseTextComponent with the original text. We then wrap it with a BoldDecorator, followed by an ItalicDecorator. The decorators add the respective formatting tags around the base text.

When calling the render() method on the italic_decorator, it invokes the render() method of the wrapped bold_decorator, which in turn invokes the render() method of the wrapped component. This way, the decorators stack up, adding the desired formatting to the text.

The resulting output is the decorated text with both bold and italic formatting: "<i><b>Hello, World!</b></i>"

By using the Decorator pattern, you can dynamically add or modify the behavior of objects at runtime by wrapping them with different decorators. This allows for flexible and extensible composition of objects with additional features or behaviors.

## Dynamic decorators 

the flexibility of dynamic decorators, where the behavior of the decorator can be determined at runtime based on the provided options.

```
def dynamic_decorator(option):
    def decorator(func):
        def wrapper(*args, **kwargs):
            if option == 'uppercase':
                result = func(*args, **kwargs)
                return result.upper()
            elif option == 'reverse':
                result = func(*args, **kwargs)
                return result[::-1]
            else:
                return func(*args, **kwargs)
        return wrapper
    return decorator

@dynamic_decorator('uppercase')
def say_hello():
    return "Hello, World!"

print(say_hello())  # Output: "HELLO, WORLD!"

@dynamic_decorator('reverse')
def say_hi():
    return "Hi, there!"

print(say_hi())  # Output: "!ereht ,iH"

def do_nothing():
    return "Doing nothing."

print(do_nothing())  # Output: "Doing nothing."
```