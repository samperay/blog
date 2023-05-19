---
title: "Python Closures"
date: 2023-05-08T17:17:58+05:30
draft: False
tags: ["programming_terms"]
---

## Example 1

 Python closure is a nested function that allows us to access variables of the outer function even after the outer function is closed.

 ```
 def outer_function():
	messge="Hi"

	def inner_function():
		print(messge) # you would be able to access the variable of outer function.

	return inner_function()

hi=outer_function() # Output: Hi
```

## Example 2

let's modify the code and we could store the `inner_function` as variable and then call return value

```
def outer_function(message):
	messge=message

	def inner_function():
		print(messge) # you would be able to access the variable of outer function.

	return inner_function

print_hi=outer_function("hi")
print_hello=outer_function("hello")

print(print_hi.__name__) # Output: inner_function
print(print_hello.__name__) # Output: inner_function

print_hi() # Output: hi
print_hello()  # Output: hello
```

## Example 3

let's use closure to add and subtract example, additionally while doing so, we could log it in the file `example.log`

```
import logging
logging.basicConfig(filename="example.log",level=logging.DEBUG)

def logger(func):
	def log_func(*args):
		logging.info(f"logging {func.__name__} with arguments {args}")
		print(func(*args))
	return log_func

def add(x,y):
    return x+y

def sub(x,y):
    return x-y

add_logger=logger(add)
sub_logger=logger(sub)

print(add_logger.__name__) # Output: log_func  
print(sub_logger.__name__) # Output: log_func

add_logger(4,5) # Output: 9
sub_logger(20,10) # Output: 10
```

