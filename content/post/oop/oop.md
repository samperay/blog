---
title: "Object Oriented Programming"
date: 2023-05-23T17:16:31+05:30
draft: False
tags: ["oop"]
---
## Objects and Classes

## Encapsulation

Bundling data and methods within a single unit.
when you create a class, it means you are `implementing encapsulation`

encapsulation allows us to restrict accessing variables and methods directly and prevent accidental data modification by creating private data members and methods within a class. 

**public** : accessable anywhere form outside the class. 

**private** : Accessible within the class

**Protected** : within the class and its sub-classes(inheritance)


### Getters and Setters

getter method to access data members and the setter methods to modify the data members

private variables are not hidden fields like in other programming languages. The getters and setters methods are often used when:

When we want to avoid direct access to private variables
To add validation logic for setting a value

```
class Employee:

    def __init__(self,name,salary,age):
        # public members
        self.name = name

        # private members
        self.__salary=salary
        self.__age=age

        # protected members
        self._project="Oracle pvt ltd"

    # getters
    def get_age(self):
        print(self.__age)

    # setters
    def set_age(self,age):
        # you can use the logic before changing 
        # the object
        if age > 130:
            print("not sure anyone is alive.. please submit proof of living!")
        self.__age = age

    def show(self):
        print(f"{self.name}'s age is {self.__age} drawing salry of {self.__salary}")


class EmployeeDepartment(Employee):
    def __init__(self,name):
        Employee().__init__(self)
        self.name = name

    def show(self):
        print(f"{self.name} employee working in project {self._project}")


emp=Employee("employee",100000,33)
emp.show()

emp.set_age(29) #Private members can be accessed by using public methods.
emp.get_age()
print(emp._Employee__age) #Name mangling.

print(f"Employee project details: {emp._project}")


sunil=Employee("Sunil",100000,34)
sunil.set_age(32)
```
