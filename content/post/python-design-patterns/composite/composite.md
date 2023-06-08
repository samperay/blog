---
title: "Composite"
date: 2023-06-08T08:24:49+05:30
draft: False
---

The Composite pattern is a structural design pattern that allows you to treat individual objects and groups of objects uniformly. It composes objects into tree-like structures to represent part-whole hierarchies. The pattern enables clients to work with individual objects and groups of objects in a consistent manner.

```
from abc import ABC, abstractmethod

# Component
class FileComponent(ABC):
    @abstractmethod
    def get_size(self):
        pass

# Leaf
class File(FileComponent):
    def __init__(self, name, size):
        self.name = name
        self.size = size

    def get_size(self):
        return self.size

# Composite
class Directory(FileComponent):
    def __init__(self, name):
        self.name = name
        self.children = []

    def add_child(self, child):
        self.children.append(child)

    def remove_child(self, child):
        self.children.remove(child)

    def get_size(self):
        total_size = 0
        for child in self.children:
            total_size += child.get_size()
        return total_size

# Usage
root = Directory("Root")

file1 = File("File1.txt", 10)
file2 = File("File2.txt", 15)
file3 = File("File3.txt", 20)

subdirectory = Directory("Subdirectory")
file4 = File("File4.txt", 5)

subdirectory.add_child(file4)

root.add_child(file1)
root.add_child(file2)
root.add_child(file3)
root.add_child(subdirectory)

print(root.get_size())  # Output: 50
```

In this example, we have the FileComponent interface that defines the common operations for both individual files and directories. The File class represents a leaf component, which is an individual file with a specific size. The Directory class represents a composite component, which is a directory containing other files and subdirectories.

The File class implements the get_size() method to return its own size.

The Directory class implements the get_size() method, which recursively calculates the total size of all its children. It maintains a list of children and provides methods to add and remove them.

In the usage section, we create instances of files and directories and organize them into a hierarchy. We add individual files and a subdirectory to the root directory. When we call the get_size() method on the root directory, it recursively calculates the total size of all its children, including the files in the subdirectory.

The resulting output is the total size of all the files and subdirectories within the root directory: 50.

By using the Composite pattern, we can treat individual files and directories uniformly as FileComponent objects. This allows us to work with complex tree-like structures in a unified manner, enabling easy traversal and manipulation of the hierarchy.