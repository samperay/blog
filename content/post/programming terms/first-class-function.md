---
title: "First Class Function"
date: 2023-05-08T10:31:27+05:30
draft: False
tags: ["programming_terms"]
---

 If a function can be assigned to a variable or passed as object/variable to other function, that function is called as `first class function` 

 ## Example 1 

 ```
 def square(x):
    return x*x 

def cube(x):
    return x*x*x

# Receives a function, executes and returns result. 
# You will provide as an list here
def mymap(func,args):
    result = []
    for each_item in args:
        result.append(func(each_item))

    return result 

sqr=mymap(square,[1,2,3]) # Output: [1,4,9]
cub=mymap(cube,[1,2,3]) # Output: [1,8,27]

# provide a single value to get the result.
def print_result(x, func):
    """recieve a function and execute it and return result"""
    return func(x)

do_square = square     # assigning square function to a variable
do_cube = cube         # assigning cube function to a variable

res = print_result(5, do_square)   # passing function to another function

```
## Example 2

We would use first-class function to create an html tag

```
def create_html(tag):
    def wrap_text(text):
        print(f"<{tag}>{msg}/<{tag}>")
    return wrap_text
```

`create_html` would return the fucntion(`wrap_text`), we would use that function to call our msg wrapped in the html msg. 

```
print_h1=create_html("h1")
print_h1("Heading1") # Output: <h1>Heading1</h1> 
```