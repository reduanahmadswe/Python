# Lecture 8: OOPS in Python | Object Oriented Programming

## OOP কি? (What is OOP?)

Object Oriented Programming (OOP) হলো একটি programming paradigm যেখানে আমরা objects এবং classes ব্যবহার করে program design করি।

### OOP এর সুবিধা:
- **Code Reusability** - একবার লিখে বারবার ব্যবহার
- **Data Security** - data encapsulation
- **Easy Maintenance** - সহজে maintain করা
- **Real-world Modeling** - বাস্তব জগতের মত design

### OOP এর মূল Concepts:
1. Class (ক্লাস)
2. Object (অবজেক্ট)
3. Encapsulation (এনক্যাপসুলেশন)
4. Inheritance (ইনহেরিটেন্স)
5. Polymorphism (পলিমরফিজম)
6. Abstraction (অ্যাবস্ট্র্যাকশন)

## Class এবং Object

### Class কি?
Class হলো একটি blueprint বা template যা দিয়ে objects তৈরি করা হয়।

### Object কি?
Object হলো class এর একটি instance। এটি class এর সব properties এবং methods থাকে।

### Basic Class এবং Object
```python
# Class definition
class Student:
    pass  # খালি class

# Object creation
student1 = Student()
student2 = Student()

print(type(student1))  # <class '__main__.Student'>
```

## Attributes (অ্যাট্রিবিউট)

### Instance Attributes
```python
class Student:
    pass

# Create object
student1 = Student()

# Add attributes dynamically
student1.name = "রহিম"
student1.age = 20
student1.roll = 101

print(student1.name)  # রহিম
print(student1.age)   # 20
```

### Using __init__ Method (Constructor)
```python
class Student:
    # Constructor
    def __init__(self, name, age, roll):
        self.name = name
        self.age = age
        self.roll = roll

# Create objects
student1 = Student("রহিম", 20, 101)
student2 = Student("করিম", 22, 102)

print(student1.name)  # রহিম
print(student2.name)  # করিম
```

### Default Values in Constructor
```python
class Student:
    def __init__(self, name, age=18, city="ঢাকা"):
        self.name = name
        self.age = age
        self.city = city

student1 = Student("রহিম")
student2 = Student("করিম", 20, "চট্টগ্রাম")

print(student1.city)  # ঢাকা (default)
print(student2.city)  # চট্টগ্রাম
```

### Class Attributes (Shared by All Objects)
```python
class Student:
    # Class attribute
    school = "ABC School"
    
    def __init__(self, name, age):
        # Instance attributes
        self.name = name
        self.age = age

student1 = Student("রহিম", 20)
student2 = Student("করিম", 22)

print(student1.school)  # ABC School
print(student2.school)  # ABC School

# Changing class attribute
Student.school = "XYZ School"
print(student1.school)  # XYZ School
print(student2.school)  # XYZ School
```

## Methods (মেথড)

### Instance Methods
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    # Instance method
    def display_info(self):
        print(f"নাম: {self.name}")
        print(f"বয়স: {self.age}")
    
    def is_adult(self):
        return self.age >= 18

student1 = Student("রহিম", 20)
student1.display_info()
print("প্রাপ্তবয়স্ক:", student1.is_adult())
```

### Methods with Parameters
```python
class Calculator:
    def add(self, a, b):
        return a + b
    
    def subtract(self, a, b):
        return a - b
    
    def multiply(self, a, b):
        return a * b
    
    def divide(self, a, b):
        if b != 0:
            return a / b
        return "ভাগ করা যাবে না"

calc = Calculator()
print(calc.add(10, 5))       # 15
print(calc.subtract(10, 5))  # 5
print(calc.multiply(10, 5))  # 50
print(calc.divide(10, 5))    # 2.0
```

### Class Methods
```python
class Student:
    school = "ABC School"
    student_count = 0
    
    def __init__(self, name):
        self.name = name
        Student.student_count += 1
    
    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school
    
    @classmethod
    def get_student_count(cls):
        return cls.student_count

student1 = Student("রহিম")
student2 = Student("করিম")

print(Student.get_student_count())  # 2

Student.change_school("XYZ School")
print(student1.school)  # XYZ School
```

### Static Methods
```python
class MathOperations:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def is_even(num):
        return num % 2 == 0
    
    @staticmethod
    def factorial(n):
        if n == 0 or n == 1:
            return 1
        result = 1
        for i in range(2, n + 1):
            result *= i
        return result

# No need to create object
print(MathOperations.add(5, 3))      # 8
print(MathOperations.is_even(10))    # True
print(MathOperations.factorial(5))   # 120
```

## Special/Magic Methods (Dunder Methods)

### __str__ এবং __repr__
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"Student: {self.name}, Age: {self.age}"
    
    def __repr__(self):
        return f"Student('{self.name}', {self.age})"

student = Student("রহিম", 20)
print(student)       # Student: রহিম, Age: 20
print(repr(student)) # Student('রহিম', 20)
```

### Comparison Methods
```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks
    
    def __eq__(self, other):
        return self.marks == other.marks
    
    def __lt__(self, other):
        return self.marks < other.marks
    
    def __gt__(self, other):
        return self.marks > other.marks

student1 = Student("রহিম", 85)
student2 = Student("করিম", 92)

print(student1 == student2)  # False
print(student1 < student2)   # True
print(student1 > student2)   # False
```

### Arithmetic Methods
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(4, 5)

v3 = v1 + v2
v4 = v2 - v1

print(v3)  # Vector(6, 8)
print(v4)  # Vector(2, 2)
```

### __len__ Method
```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs
    
    def __len__(self):
        return len(self.songs)

playlist = Playlist(["গান১", "গান২", "গান৩"])
print(len(playlist))  # 3
```

## Encapsulation (এনক্যাপসুলেশন)

### Public, Protected, Private
```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.account_number = account_number  # Public
        self._balance = balance               # Protected (convention)
        self.__pin = "1234"                   # Private (name mangling)
    
    def get_balance(self):
        return self._balance
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            print(f"{amount} টাকা জমা হয়েছে")
    
    def withdraw(self, amount, pin):
        if pin == self.__pin:
            if amount <= self._balance:
                self._balance -= amount
                print(f"{amount} টাকা উত্তোলন হয়েছে")
            else:
                print("যথেষ্ট টাকা নেই")
        else:
            print("ভুল PIN")

account = BankAccount("123456", 5000)
print(account.account_number)  # 123456 (Public - access করা যায়)
print(account.get_balance())   # 5000

account.deposit(1000)          # 1000 টাকা জমা হয়েছে
account.withdraw(500, "1234")  # 500 টাকা উত্তোলন হয়েছে

# print(account.__pin)  # Error! Private attribute
```

### Property Decorators (Getters and Setters)
```python
class Student:
    def __init__(self, name, age):
        self._name = name
        self._age = age
    
    # Getter
    @property
    def name(self):
        return self._name
    
    # Setter
    @name.setter
    def name(self, value):
        if value:
            self._name = value
        else:
            print("নাম খালি হতে পারবে না")
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if 0 < value < 100:
            self._age = value
        else:
            print("বয়স সঠিক নয়")

student = Student("রহিম", 20)
print(student.name)  # রহিম

student.name = "করিম"
print(student.name)  # করিম

student.age = 150    # বয়স সঠিক নয়
print(student.age)   # 20 (unchanged)
```

## Inheritance (ইনহেরিটেন্স)

### Single Inheritance
```python
# Parent class
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display_info(self):
        print(f"নাম: {self.name}")
        print(f"বয়স: {self.age}")

# Child class
class Student(Person):
    def __init__(self, name, age, roll):
        super().__init__(name, age)  # Parent constructor call
        self.roll = roll
    
    def display_info(self):
        super().display_info()  # Parent method call
        print(f"রোল: {self.roll}")

student = Student("রহিম", 20, 101)
student.display_info()
# নাম: রহিম
# বয়স: 20
# রোল: 101
```

### Multiple Inheritance
```python
class Father:
    def skills(self):
        print("ব্যবসা")

class Mother:
    def skills(self):
        print("রান্না")

class Child(Father, Mother):
    def my_skills(self):
        print("প্রোগ্রামিং")

child = Child()
child.skills()     # ব্যবসা (Father এর method - MRO)
child.my_skills()  # প্রোগ্রামিং
```

### Method Resolution Order (MRO)
```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")

class C(A):
    def show(self):
        print("C")

class D(B, C):
    pass

d = D()
d.show()  # B
print(D.mro())  # [D, B, C, A, object]
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: Library Management System
```python
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.is_borrowed = False
    
    def __str__(self):
        status = "ধার নেওয়া" if self.is_borrowed else "উপলব্ধ"
        return f"{self.title} by {self.author} [{status}]"

class Library:
    def __init__(self, name):
        self.name = name
        self.books = []
    
    def add_book(self, book):
        self.books.append(book)
        print(f"'{book.title}' যোগ হয়েছে")
    
    def display_books(self):
        print(f"\n{self.name} এর বইসমূহ:")
        for book in self.books:
            print(f"  - {book}")
    
    def borrow_book(self, isbn):
        for book in self.books:
            if book.isbn == isbn:
                if not book.is_borrowed:
                    book.is_borrowed = True
                    print(f"'{book.title}' ধার নেওয়া হয়েছে")
                    return
                else:
                    print("বইটি ধার নেওয়া আছে")
                    return
        print("বই পাওয়া যায়নি")
    
    def return_book(self, isbn):
        for book in self.books:
            if book.isbn == isbn:
                if book.is_borrowed:
                    book.is_borrowed = False
                    print(f"'{book.title}' ফেরত দেওয়া হয়েছে")
                    return
                else:
                    print("বইটি ধার নেওয়া হয়নি")
                    return
        print("বই পাওয়া যায়নি")

# Usage
library = Library("জাতীয় গ্রন্থাগার")

book1 = Book("Python Programming", "John Doe", "12345")
book2 = Book("Data Science", "Jane Smith", "67890")

library.add_book(book1)
library.add_book(book2)

library.display_books()
library.borrow_book("12345")
library.display_books()
library.return_book("12345")
library.display_books()
```

### প্রব্লেম ২: Shape Calculator
```python
class Shape:
    def area(self):
        pass
    
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width
    
    def perimeter(self):
        return 2 * (self.length + self.width)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# Usage
rectangle = Rectangle(10, 5)
print(f"আয়তক্ষেত্র - ক্ষেত্রফল: {rectangle.area()}")
print(f"আয়তক্ষেত্র - পরিসীমা: {rectangle.perimeter()}")

circle = Circle(7)
print(f"বৃত্ত - ক্ষেত্রফল: {circle.area():.2f}")
print(f"বৃত্ত - পরিধি: {circle.perimeter():.2f}")
```

### প্রব্লেম ৩: Employee Management
```python
class Employee:
    company = "ABC Company"
    
    def __init__(self, name, emp_id, salary):
        self.name = name
        self.emp_id = emp_id
        self.__salary = salary
    
    def get_salary(self):
        return self.__salary
    
    def set_salary(self, new_salary):
        if new_salary > 0:
            self.__salary = new_salary
        else:
            print("বেতন ০ এর বেশি হতে হবে")
    
    def display_info(self):
        print(f"নাম: {self.name}")
        print(f"ID: {self.emp_id}")
        print(f"বেতন: {self.__salary} টাকা")

# Usage
emp1 = Employee("রহিম", "E001", 30000)
emp1.display_info()

emp1.set_salary(35000)
print(f"নতুন বেতন: {emp1.get_salary()} টাকা")
```

## গুরুত্বপূর্ণ পয়েন্টস
- Class হলো blueprint, Object হলো instance
- `__init__` হলো constructor
- `self` দিয়ে instance attributes এবং methods access করা হয়
- Class attributes সব objects এর মধ্যে shared
- Instance methods প্রথম parameter `self` নেয়
- Class methods `@classmethod` decorator ব্যবহার করে
- Static methods `@staticmethod` decorator ব্যবহার করে
- `__str__` method print() এর জন্য
- Private attributes এর জন্য `__` prefix
- Protected attributes এর জন্য `_` prefix (convention)
- Inheritance দিয়ে code reusability বাড়ে
- `super()` দিয়ে parent class access করা হয়
