# Lecture 9: OOPS Part 2 | Advanced Object Oriented Programming

## Polymorphism (পলিমরফিজম)

Polymorphism মানে "অনেক রূপ"। একই interface দিয়ে বিভিন্ন implementation করা যায়।

### Method Overriding (মেথড ওভাররাইডিং)
```python
class Animal:
    def sound(self):
        print("প্রাণীর শব্দ")
    
    def move(self):
        print("প্রাণী নড়ে")

class Dog(Animal):
    def sound(self):
        print("ঘেউ ঘেউ")
    
    def move(self):
        print("কুকুর দৌড়ায়")

class Cat(Animal):
    def sound(self):
        print("মিউ মিউ")
    
    def move(self):
        print("বিড়াল লাফায়")

class Bird(Animal):
    def sound(self):
        print("চিঁচিঁ")
    
    def move(self):
        print("পাখি উড়ে")

# Polymorphism in action
animals = [Dog(), Cat(), Bird()]

for animal in animals:
    animal.sound()
    animal.move()
    print()
```

### Operator Overloading (অপারেটর ওভারলোডিং)
```python
class ComplexNumber:
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag
    
    def __add__(self, other):
        return ComplexNumber(
            self.real + other.real,
            self.imag + other.imag
        )
    
    def __sub__(self, other):
        return ComplexNumber(
            self.real - other.real,
            self.imag - other.imag
        )
    
    def __mul__(self, other):
        real = self.real * other.real - self.imag * other.imag
        imag = self.real * other.imag + self.imag * other.real
        return ComplexNumber(real, imag)
    
    def __str__(self):
        if self.imag >= 0:
            return f"{self.real} + {self.imag}i"
        return f"{self.real} - {abs(self.imag)}i"

c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, 2)

c3 = c1 + c2
c4 = c1 - c2
c5 = c1 * c2

print(f"{c1} + {c2} = {c3}")
print(f"{c1} - {c2} = {c4}")
print(f"{c1} * {c2} = {c5}")
```

### Duck Typing
```python
# "If it walks like a duck and quacks like a duck, it's a duck"

class Duck:
    def speak(self):
        print("Quack quack!")

class Dog:
    def speak(self):
        print("Woof woof!")

class Cat:
    def speak(self):
        print("Meow!")

def make_sound(animal):
    animal.speak()  # কোন টাইপ check করছি না

# সব object এই function use করতে পারবে
make_sound(Duck())  # Quack quack!
make_sound(Dog())   # Woof woof!
make_sound(Cat())   # Meow!
```

## Abstraction (অ্যাবস্ট্র্যাকশন)

Abstraction মানে implementation details লুকিয়ে রাখা এবং শুধু essential features দেখানো।

### Abstract Base Class (ABC)
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass
    
    def description(self):
        return "এটি একটি shape"

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

# shape = Shape()  # Error! Abstract class এর object তৈরি করা যায় না

rectangle = Rectangle(10, 5)
circle = Circle(7)

print(f"আয়তক্ষেত্র - ক্ষেত্রফল: {rectangle.area()}")
print(f"বৃত্ত - ক্ষেত্রফল: {circle.area():.2f}")
```

### Abstract Methods with Implementation
```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, name, color):
        self.name = name
        self.color = color
    
    @abstractmethod
    def start(self):
        print(f"{self.name} শুরু হচ্ছে...")
    
    @abstractmethod
    def stop(self):
        pass
    
    def display_info(self):
        print(f"নাম: {self.name}, রঙ: {self.color}")

class Car(Vehicle):
    def start(self):
        super().start()
        print("গাড়ির ইঞ্জিন চালু হয়েছে")
    
    def stop(self):
        print("গাড়ি থেমেছে")

class Bike(Vehicle):
    def start(self):
        super().start()
        print("বাইক চালু হয়েছে")
    
    def stop(self):
        print("বাইক থেমেছে")

car = Car("Toyota", "লাল")
car.display_info()
car.start()
car.stop()
```

## Advanced Inheritance Concepts

### Multi-level Inheritance
```python
class GrandParent:
    def __init__(self, surname):
        self.surname = surname
    
    def show_surname(self):
        print(f"পদবি: {self.surname}")

class Parent(GrandParent):
    def __init__(self, surname, parent_name):
        super().__init__(surname)
        self.parent_name = parent_name
    
    def show_parent(self):
        print(f"পিতা/মাতা: {self.parent_name}")

class Child(Parent):
    def __init__(self, surname, parent_name, child_name):
        super().__init__(surname, parent_name)
        self.child_name = child_name
    
    def show_child(self):
        print(f"সন্তান: {self.child_name}")

child = Child("রহমান", "করিম রহমান", "সাকিব রহমান")
child.show_surname()  # পদবি: রহমান
child.show_parent()   # পিতা/মাতা: করিম রহমান
child.show_child()    # সন্তান: সাকিব রহমান
```

### Hierarchical Inheritance
```python
class Employee:
    def __init__(self, name, emp_id):
        self.name = name
        self.emp_id = emp_id
    
    def display_info(self):
        print(f"নাম: {self.name}, ID: {self.emp_id}")

class Manager(Employee):
    def __init__(self, name, emp_id, department):
        super().__init__(name, emp_id)
        self.department = department
    
    def show_department(self):
        print(f"বিভাগ: {self.department}")

class Developer(Employee):
    def __init__(self, name, emp_id, language):
        super().__init__(name, emp_id)
        self.language = language
    
    def show_language(self):
        print(f"ভাষা: {self.language}")

class Designer(Employee):
    def __init__(self, name, emp_id, tool):
        super().__init__(name, emp_id)
        self.tool = tool
    
    def show_tool(self):
        print(f"টুল: {self.tool}")

manager = Manager("রহিম", "E001", "IT")
developer = Developer("করিম", "E002", "Python")
designer = Designer("জামাল", "E003", "Figma")

manager.display_info()
manager.show_department()
```

### Hybrid Inheritance
```python
class School:
    def __init__(self, school_name):
        self.school_name = school_name

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Student(Person, School):
    def __init__(self, name, age, school_name, roll):
        Person.__init__(self, name, age)
        School.__init__(self, school_name)
        self.roll = roll
    
    def display_info(self):
        print(f"নাম: {self.name}")
        print(f"বয়স: {self.age}")
        print(f"স্কুল: {self.school_name}")
        print(f"রোল: {self.roll}")

student = Student("রহিম", 15, "ABC School", 101)
student.display_info()
```

## Method Types এবং Decorators

### Instance, Class, এবং Static Methods - বিস্তারিত
```python
class Employee:
    company = "ABC Company"
    raise_amount = 1.05
    
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
    
    # Instance method (self parameter)
    def apply_raise(self):
        self.salary = int(self.salary * self.raise_amount)
        print(f"{self.name} এর নতুন বেতন: {self.salary}")
    
    # Class method (@classmethod decorator)
    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount
        print(f"বেতন বৃদ্ধির হার: {cls.raise_amount}")
    
    # Alternative constructor
    @classmethod
    def from_string(cls, emp_string):
        name, salary = emp_string.split('-')
        return cls(name, int(salary))
    
    # Static method (@staticmethod decorator)
    @staticmethod
    def is_workday(day):
        if day.weekday() == 4 or day.weekday() == 5:  # Friday, Saturday
            return False
        return True

# Instance method
emp1 = Employee("রহিম", 30000)
emp1.apply_raise()

# Class method
Employee.set_raise_amount(1.10)

# Alternative constructor
emp2 = Employee.from_string("করিম-35000")
print(f"{emp2.name}: {emp2.salary}")

# Static method
import datetime
my_date = datetime.date(2025, 12, 19)
print(Employee.is_workday(my_date))
```

## Property Decorators - বিস্তারিত

### @property, @setter, @deleter
```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        print("Getting celsius...")
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        print("Setting celsius...")
        if value < -273.15:
            raise ValueError("তাপমাত্রা -273.15°C এর কম হতে পারে না")
        self._celsius = value
    
    @celsius.deleter
    def celsius(self):
        print("Deleting celsius...")
        del self._celsius
    
    @property
    def fahrenheit(self):
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self._celsius = (value - 32) * 5/9
    
    @property
    def kelvin(self):
        return self._celsius + 273.15

# Usage
temp = Temperature(25)
print(temp.celsius)      # Getting celsius... 25
print(temp.fahrenheit)   # 77.0
print(temp.kelvin)       # 298.15

temp.celsius = 30        # Setting celsius...
print(temp.celsius)      # Getting celsius... 30

temp.fahrenheit = 86
print(temp.celsius)      # Getting celsius... 30.0

# del temp.celsius       # Deleting celsius...
```

## Special Methods - আরও বিস্তারিত

### Container Methods
```python
class ShoppingCart:
    def __init__(self):
        self.items = []
    
    def add_item(self, item, price):
        self.items.append({"item": item, "price": price})
    
    def __len__(self):
        return len(self.items)
    
    def __getitem__(self, index):
        return self.items[index]
    
    def __setitem__(self, index, value):
        self.items[index] = value
    
    def __delitem__(self, index):
        del self.items[index]
    
    def __contains__(self, item):
        for cart_item in self.items:
            if cart_item["item"] == item:
                return True
        return False
    
    def __iter__(self):
        return iter(self.items)
    
    def total_price(self):
        return sum(item["price"] for item in self.items)

# Usage
cart = ShoppingCart()
cart.add_item("কলম", 10)
cart.add_item("খাতা", 30)
cart.add_item("বই", 100)

print(len(cart))          # 3
print(cart[0])            # {'item': 'কলম', 'price': 10}
print("কলম" in cart)      # True

for item in cart:
    print(f"{item['item']}: {item['price']} টাকা")

print(f"মোট: {cart.total_price()} টাকা")
```

### Call Method (__call__)
```python
class Multiplier:
    def __init__(self, factor):
        self.factor = factor
    
    def __call__(self, number):
        return number * self.factor

# Object কে function এর মত call করা
double = Multiplier(2)
triple = Multiplier(3)

print(double(5))   # 10
print(triple(5))   # 15

# লাম্বদা এর বিকল্প
numbers = [1, 2, 3, 4, 5]
doubled = list(map(double, numbers))
print(doubled)  # [2, 4, 6, 8, 10]
```

## Composition (কম্পোজিশন)

Inheritance এর বিকল্প হিসেবে Composition ব্যবহার করা যায়। "has-a" relationship.

```python
class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower
    
    def start(self):
        print(f"{self.horsepower} HP ইঞ্জিন চালু হয়েছে")
    
    def stop(self):
        print("ইঞ্জিন বন্ধ হয়েছে")

class Wheels:
    def __init__(self, count):
        self.count = count
    
    def rotate(self):
        print(f"{self.count}টি চাকা ঘুরছে")

class Car:
    def __init__(self, model, horsepower, wheels):
        self.model = model
        self.engine = Engine(horsepower)  # Composition
        self.wheels = Wheels(wheels)      # Composition
    
    def drive(self):
        print(f"{self.model} চালানো হচ্ছে...")
        self.engine.start()
        self.wheels.rotate()
    
    def park(self):
        print(f"{self.model} পার্ক করা হচ্ছে...")
        self.engine.stop()

# Usage
car = Car("Toyota", 150, 4)
car.drive()
car.park()
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: Bank Account System with Polymorphism
```python
from abc import ABC, abstractmethod

class BankAccount(ABC):
    def __init__(self, account_number, holder_name, balance=0):
        self.account_number = account_number
        self.holder_name = holder_name
        self._balance = balance
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            print(f"{amount} টাকা জমা হয়েছে")
        else:
            print("ভুল পরিমাণ")
    
    @abstractmethod
    def withdraw(self, amount):
        pass
    
    def get_balance(self):
        return self._balance
    
    def display_info(self):
        print(f"অ্যাকাউন্ট নং: {self.account_number}")
        print(f"নাম: {self.holder_name}")
        print(f"ব্যালেন্স: {self._balance} টাকা")

class SavingsAccount(BankAccount):
    def __init__(self, account_number, holder_name, balance=0, interest_rate=0.05):
        super().__init__(account_number, holder_name, balance)
        self.interest_rate = interest_rate
    
    def withdraw(self, amount):
        if amount > 0 and amount <= self._balance:
            self._balance -= amount
            print(f"{amount} টাকা উত্তোলন হয়েছে")
        else:
            print("অপর্যাপ্ত ব্যালেন্স বা ভুল পরিমাণ")
    
    def add_interest(self):
        interest = self._balance * self.interest_rate
        self._balance += interest
        print(f"{interest} টাকা সুদ যোগ হয়েছে")

class CurrentAccount(BankAccount):
    def __init__(self, account_number, holder_name, balance=0, overdraft_limit=5000):
        super().__init__(account_number, holder_name, balance)
        self.overdraft_limit = overdraft_limit
    
    def withdraw(self, amount):
        if amount > 0 and amount <= (self._balance + self.overdraft_limit):
            self._balance -= amount
            print(f"{amount} টাকা উত্তোলন হয়েছে")
        else:
            print("Overdraft limit অতিক্রম করেছে বা ভুল পরিমাণ")

# Usage
savings = SavingsAccount("SAV001", "রহিম", 10000)
current = CurrentAccount("CUR001", "করিম", 5000)

savings.display_info()
savings.deposit(2000)
savings.add_interest()
savings.withdraw(3000)
print(f"নতুন ব্যালেন্স: {savings.get_balance()}")

print("\n")

current.display_info()
current.withdraw(8000)  # Overdraft ব্যবহার
print(f"নতুন ব্যালেন্স: {current.get_balance()}")
```

### প্রব্লেম ২: E-commerce System
```python
from abc import ABC, abstractmethod

class Product(ABC):
    def __init__(self, name, price):
        self.name = name
        self.price = price
    
    @abstractmethod
    def get_details(self):
        pass
    
    def __str__(self):
        return f"{self.name} - {self.price} টাকা"

class Electronics(Product):
    def __init__(self, name, price, warranty):
        super().__init__(name, price)
        self.warranty = warranty
    
    def get_details(self):
        return f"{self.name} (Electronics)\nদাম: {self.price} টাকা\nওয়ারেন্টি: {self.warranty} মাস"

class Clothing(Product):
    def __init__(self, name, price, size):
        super().__init__(name, price)
        self.size = size
    
    def get_details(self):
        return f"{self.name} (Clothing)\nদাম: {self.price} টাকা\nসাইজ: {self.size}"

class ShoppingCart:
    def __init__(self):
        self.products = []
    
    def add_product(self, product):
        self.products.append(product)
        print(f"{product.name} যোগ হয়েছে")
    
    def remove_product(self, product_name):
        for product in self.products:
            if product.name == product_name:
                self.products.remove(product)
                print(f"{product_name} মুছে গেছে")
                return
        print("পণ্য পাওয়া যায়নি")
    
    def calculate_total(self):
        return sum(product.price for product in self.products)
    
    def display_cart(self):
        if not self.products:
            print("কার্ট খালি")
            return
        
        print("\n=== Shopping Cart ===")
        for i, product in enumerate(self.products, 1):
            print(f"{i}. {product.get_details()}\n")
        print(f"মোট: {self.calculate_total()} টাকা")

# Usage
cart = ShoppingCart()

laptop = Electronics("Laptop", 50000, 12)
phone = Electronics("Smartphone", 25000, 6)
shirt = Clothing("T-Shirt", 500, "M")
jeans = Clothing("Jeans", 1200, "32")

cart.add_product(laptop)
cart.add_product(phone)
cart.add_product(shirt)
cart.add_product(jeans)

cart.display_cart()

cart.remove_product("T-Shirt")
cart.display_cart()
```

### প্রব্লেম ৩: University System
```python
class Person:
    def __init__(self, name, age, email):
        self.name = name
        self.age = age
        self.email = email
    
    def display_info(self):
        print(f"নাম: {self.name}")
        print(f"বয়স: {self.age}")
        print(f"ইমেইল: {self.email}")

class Student(Person):
    student_count = 0
    
    def __init__(self, name, age, email, student_id):
        super().__init__(name, age, email)
        self.student_id = student_id
        self.courses = []
        Student.student_count += 1
    
    def enroll_course(self, course):
        if course not in self.courses:
            self.courses.append(course)
            print(f"{self.name} '{course}' কোর্সে ভর্তি হয়েছে")
        else:
            print("ইতিমধ্যে ভর্তি হয়ে গেছে")
    
    def display_info(self):
        super().display_info()
        print(f"Student ID: {self.student_id}")
        print(f"কোর্সসমূহ: {', '.join(self.courses) if self.courses else 'কোন কোর্স নেই'}")
    
    @classmethod
    def get_student_count(cls):
        return cls.student_count

class Teacher(Person):
    def __init__(self, name, age, email, employee_id, subject):
        super().__init__(name, age, email)
        self.employee_id = employee_id
        self.subject = subject
    
    def display_info(self):
        super().display_info()
        print(f"Employee ID: {self.employee_id}")
        print(f"বিষয়: {self.subject}")

# Usage
student1 = Student("রহিম", 20, "rahim@mail.com", "S001")
student2 = Student("করিম", 22, "karim@mail.com", "S002")

student1.enroll_course("Python Programming")
student1.enroll_course("Data Science")
student2.enroll_course("Web Development")

print("=== Student 1 ===")
student1.display_info()

print("\n=== Student 2 ===")
student2.display_info()

print(f"\nমোট ছাত্র: {Student.get_student_count()}")

teacher = Teacher("জামাল", 35, "jamal@mail.com", "T001", "Computer Science")
print("\n=== Teacher ===")
teacher.display_info()
```

## গুরুত্বপূর্ণ পয়েন্টস
- **Polymorphism** - একই interface, বিভিন্ন implementation
- **Method Overriding** - child class এ parent method পরিবর্তন
- **Abstraction** - ABC module ব্যবহার করে abstract class তৈরি
- **Abstract methods** - child class এ অবশ্যই implement করতে হবে
- **Composition** - "has-a" relationship
- **@property** - getter method হিসেবে
- **@setter** - value set করার জন্য
- **@deleter** - value delete করার জন্য
- **__call__** - object কে function এর মত call করা
- **Container methods** - __len__, __getitem__, __setitem__, __contains__
- **Inheritance vs Composition** - কখন কোনটা ব্যবহার করবেন বুঝতে হবে

## OOP Design Principles (SOLID)
- **S** - Single Responsibility (একটা class একটা কাজ করবে)
- **O** - Open/Closed (extension এর জন্য open, modification এর জন্য closed)
- **L** - Liskov Substitution (child object parent এর জায়গায় ব্যবহার করা যাবে)
- **I** - Interface Segregation (বড় interface ভেঙে ছোট করা)
- **D** - Dependency Inversion (abstraction এর উপর নির্ভর করা)

## সমাপ্তি
Python এর OOP খুবই শক্তিশালী এবং flexible। এই concepts গুলো ভালোভাবে বুঝে practice করলে আপনি complex software design করতে পারবেন। সবসময় মনে রাখবেন:
- Keep it simple
- Reuse code
- Encapsulate data
- Use abstraction
- Follow SOLID principles
