---
title: "Single Responsibility Principle"
date: 2023-05-05T15:28:57+05:30
draft: False
---

The Single Responsibility Principle (SRP) states that a class or module should have only one reason to change. In other words, each class or module should have a single responsibility or purpose.

```
class Student:
    def __init__(self, name, id_number):
        self.name = name
        self.id_number = id_number

    def get_name(self):
        return self.name

    def get_id_number(self):
        return self.id_number

    def __str__(self):
        return f"name: {self.name} \nid: {self.id_number}\n"

    # Breaking SRP because, its saving to database and not associated with Student class,
    # so it should not be overloaded.
    def register(self, filename):
        with open(filename, "w") as fh:
            fh.write(f"name: {self.name} \nid: {self.id_number}\n")
```

In order not to use the above rule, you would be modifying the rule as below and re-writing the function. 

```
class StudentRegistration:
    def save_to_file(self,student, filename):
        with open(filename, "w") as fh:
            fh.write(f"name: {student.name} \nid: {student.id_number}\n")
```

Create couple of students

```
student1=Student("Sunil", "1")
student2=Student("Shiva", "2")
```

Save the student registration by using seperate class and save them.

```
register_student=StudentRegistration()
filename=r"/Users/sunilamperayani/sandbox/design-patterns/students.db"
print("saving the student to the database.")
register_student.save_to_file(student1,filename)
```

Another example, 

```
class FileReader:
    def __init__(self, file_path):
        self.file_path = file_path
    
    def read_file(self):
        with open(self.file_path, 'r') as f:
            return f.read()
```