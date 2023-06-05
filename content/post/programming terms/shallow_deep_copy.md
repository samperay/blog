---
title: "Shallow & Deep copy"
date: 2023-06-05T13:02:04+05:30
draft: False
tags: ["programming_terms"]
---

**Shallow Copy:**

A shallow copy creates a new object but references the same elements as the original object. In other words, it creates a new container object and fills it with references to the same elements as the original. The references point to the same memory addresses as the original elements. If any of the referenced elements are mutable, changes made to them will be reflected in both the original and the shallow copy.

You can think of "hardlink" in linux prespective. 

```
import copy

list1 = [1, 2, [3, 4]]
list2 = copy.copy(list1)

list2[0] = 5
list2[2].append(5)

print(list1)  # Output: [1, 2, [3, 4, 5]]
print(list2)  # Output: [5, 2, [3, 4, 5]]
```

## Usecases of shallow copy 

**Cloning mutable objects:** Shallow copy is often used when you want to create a new object that shares the internal state with the original object. This can be useful when working with mutable objects like lists or dictionaries, where you want to create a modified version while preserving the original.

**Performance optimization:** Shallow copy can be more efficient in terms of time and memory when dealing with large objects or data structures. Instead of duplicating the entire object, a shallow copy simply creates references to the existing elements.

**Nested data structures:** Shallow copy is appropriate when you have nested data structures, such as a list of lists or a dictionary of dictionaries. It allows you to create a new structure that maintains references to the original nested objects.

**Deep Copy:**

A deep copy creates a new object and recursively copies all the elements from the original object to the new object. It creates a completely independent copy with its own set of elements. Any changes made to the copied elements will not affect the original object.

softlink from linux prespective. 

```
import copy

list1 = [1, 2, [3, 4]]
list2 = copy.deepcopy(list1)

list2[0] = 5
list2[2].append(5)

print(list1)  # Output: [1, 2, [3, 4]]
print(list2)  # Output: [5, 2, [3, 4, 5]]
```

## usecases of deep copy

**Creating independent copies:** Deep copy is used when you want to create a completely independent copy of an object and its internal state. This is useful when you need to modify the copied object without affecting the original object.

**Avoiding unintended side effects:** Deep copy ensures that any modifications made to the copied object or its nested elements do not impact the original object. This can be important when dealing with complex data structures or when multiple objects need to maintain their own separate state.

**Immutable objects:** Deep copy is suitable for creating copies of immutable objects, such as strings or tuples, where modifying the object is not possible. Deep copy allows you to create a new object with the same value.

