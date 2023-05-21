---
title: "Builder Facets"
date: 2023-05-21T19:17:20+05:30
draft: False
---

Sometimes it would be difficuilt to build multiple attributes in the object and hence we would need to create a step-by-step process for builder creation object

## Person Example

let's assume, you have a person class in which the object person needs to have two builders i.e 
`personal` and `work`

```
class Person:
    def __init__(self):
        print(f"Creating person class interface")

        # personal

        self.address = None
        self.code = None
        self.city = None

        # professional
        self.company = None
        self.position = None
        self.salary = None

    def __str__(self):
        return f"address: {self.address} location in code {self.code} in city {self.city}\n" + \
                   f"Employed at {self.company} as {self.position} with salary {self.salary}"
```

We will create a two seperate builders one for the `personal` and another for `professional`

**Seperate Builder Class**

```
class PersonBuilder:
    def __init__(self, person=None):
        self.person = Person() if person is None else person

    # function for personal builder
    @property
    def personal(self):
        return PersonPersonalBuilder(self.person)

    # function for work builder
    @property
    def work(self):
        return PersonWorkBuilder(self.person)

    def build(self):
        return self.person
```

**PersonalBuilder**

```
class PersonPersonalBuilder(PersonBuilder):
    def __init__(self, person):
        super().__init__(person)

    def location_at(self, address):
        self.person.address = address
        return self

    def location_code(self, code):
        self.person.code = code
        return self

    def location_city(self, city):
        self.person.city = city
        return self
```

**Professional Work Builder**

```
class PersonWorkBuilder(PersonBuilder):
    def __init__(self, person):
        super().__init__(person)

    def work_company(self, company):
        self.person.company = company
        return self

    def work_position(self, position):
        self.person.position = position
        return self

    def work_salary(self, salary):
        self.person.salary = salary
        return self
```

Finally, start to build the person. 

```
pb = PersonBuilder()
person1 = pb.personal.location_at("Bang").location_city("Bang").location_code(560026)\
            .work.work_company("ino").work_position("engineer").work_salary("232323").build()
         
print(person1)
person2=PersonBuilder().build() # None object
print(person2)
```

**Output**

```
address: Bang location in code 560026 in city Bang
Employed at ino as engineer with salary 232323
address: None location in code None in city None
Employed at None as None with salary None
```
