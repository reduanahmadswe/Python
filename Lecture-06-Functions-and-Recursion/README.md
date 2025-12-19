# Lecture 6: Functions & Recursion in Python

## ফাংশন কি? (What is a Function?)

ফাংশন হলো reusable code এর একটি block যা একটি নির্দিষ্ট কাজ করে। একবার define করে বারবার call করা যায়।

### ফাংশন এর সুবিধা:
- Code reusability (পুনরায় ব্যবহার)
- Code organization (সুসংগঠিত)
- Easy maintenance (সহজে maintain)
- Easy debugging (ডিবাগিং সহজ)

## Function Definition (ফাংশন তৈরি করা)

### Basic Function
```python
# Function definition
def greet():
    print("হ্যালো!")
    print("স্বাগতম!")

# Function call
greet()
# Output:
# হ্যালো!
# স্বাগতম!
```

### Function Syntax
```python
def function_name(parameters):
    """Docstring (optional)"""
    # code block
    return value  # optional
```

## Function Parameters (পরামিতি)

### Single Parameter
```python
def greet(name):
    print(f"হ্যালো, {name}!")

greet("রহিম")  # হ্যালো, রহিম!
greet("করিম")  # হ্যালো, করিম!
```

### Multiple Parameters
```python
def add(a, b):
    result = a + b
    print(f"{a} + {b} = {result}")

add(5, 3)   # 5 + 3 = 8
add(10, 20) # 10 + 20 = 30
```

### Default Parameters
```python
def greet(name, message="সুপ্রভাত!"):
    print(f"{message}, {name}!")

greet("রহিম")                    # সুপ্রভাত!, রহিম!
greet("করিম", "শুভ সন্ধ্যা")     # শুভ সন্ধ্যা, করিম!

# Multiple default parameters
def power(base, exponent=2):
    return base ** exponent

print(power(5))      # 25 (5²)
print(power(5, 3))   # 125 (5³)
```

### Keyword Arguments
```python
def person_info(name, age, city):
    print(f"নাম: {name}")
    print(f"বয়স: {age}")
    print(f"শহর: {city}")

# Positional arguments
person_info("রহিম", 25, "ঢাকা")

# Keyword arguments
person_info(age=30, city="চট্টগ্রাম", name="করিম")

# Mixed (positional first, then keyword)
person_info("জামাল", city="সিলেট", age=22)
```

### Arbitrary Arguments (*args)
```python
# যেকোনো সংখ্যক argument নেওয়া
def add_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(add_all(1, 2, 3))           # 6
print(add_all(10, 20, 30, 40))    # 100
print(add_all(5))                 # 5

# আরেকটি উদাহরণ
def print_names(*names):
    for name in names:
        print(f"হ্যালো, {name}!")

print_names("রহিম", "করিম", "জামাল")
```

### Arbitrary Keyword Arguments (**kwargs)
```python
def student_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

student_info(name="রহিম", age=20, city="ঢাকা")
# Output:
# name: রহিম
# age: 20
# city: ঢাকা

# Combined *args এবং **kwargs
def display_info(*args, **kwargs):
    print("Args:", args)
    print("Kwargs:", kwargs)

display_info(1, 2, 3, name="রহিম", age=25)
# Args: (1, 2, 3)
# Kwargs: {'name': 'রহিম', 'age': 25}
```

## Return Statement

### Single Return Value
```python
def square(num):
    return num * num

result = square(5)
print(result)  # 25

# Direct use
print(square(10))  # 100
```

### Multiple Return Values
```python
def arithmetic(a, b):
    add = a + b
    sub = a - b
    mul = a * b
    div = a / b
    return add, sub, mul, div

# Tuple unpacking
sum, diff, prod, quot = arithmetic(10, 5)
print(f"যোগ: {sum}")      # 15
print(f"বিয়োগ: {diff}")   # 5
print(f"গুণ: {prod}")      # 50
print(f"ভাগ: {quot}")      # 2.0

# Or as tuple
results = arithmetic(20, 4)
print(results)  # (24, 16, 80, 5.0)
```

### Return without Value
```python
def check_age(age):
    if age < 18:
        print("নাবালক")
        return  # function থেকে বের হয়ে যাবে
    print("প্রাপ্তবয়স্ক")

check_age(15)  # নাবালক
check_age(25)  # প্রাপ্তবয়স্ক
```

## Variable Scope (ভেরিয়েবল এর পরিধি)

### Local Variables
```python
def my_function():
    x = 10  # Local variable
    print(x)

my_function()  # 10
# print(x)  # Error! x function এর বাইরে নেই
```

### Global Variables
```python
x = 100  # Global variable

def my_function():
    print(x)  # Global variable access করা

my_function()  # 100
print(x)       # 100
```

### Global Keyword
```python
count = 0

def increment():
    global count  # Global variable modify করার জন্য
    count += 1

increment()
increment()
print(count)  # 2

# Without global keyword
def increment_wrong():
    count = count + 1  # Error! Local variable এর আগে use

# increment_wrong()  # UnboundLocalError
```

### Local vs Global - Same Name
```python
x = "Global"

def my_function():
    x = "Local"
    print(x)

my_function()  # Local
print(x)       # Global
```

## Lambda Functions (Anonymous Functions)

### Basic Lambda
```python
# Normal function
def square(x):
    return x * x

# Lambda function
square_lambda = lambda x: x * x

print(square(5))         # 25
print(square_lambda(5))  # 25
```

### Lambda with Multiple Parameters
```python
# Addition
add = lambda a, b: a + b
print(add(5, 3))  # 8

# Maximum
maximum = lambda a, b: a if a > b else b
print(maximum(10, 20))  # 20
```

### Lambda in Sorting
```python
# List of tuples
students = [
    ("রহিম", 85),
    ("করিম", 92),
    ("জামাল", 78)
]

# নামের ভিত্তিতে sort
students.sort(key=lambda x: x[0])
print(students)

# নম্বরের ভিত্তিতে sort
students.sort(key=lambda x: x[1], reverse=True)
print(students)
```

### Lambda with map(), filter(), reduce()

#### map() - প্রতিটা element এ function apply
```python
numbers = [1, 2, 3, 4, 5]

# Square of each number
squares = list(map(lambda x: x*x, numbers))
print(squares)  # [1, 4, 9, 16, 25]

# Multiple lists
list1 = [1, 2, 3]
list2 = [10, 20, 30]
sums = list(map(lambda x, y: x+y, list1, list2))
print(sums)  # [11, 22, 33]
```

#### filter() - শর্ত অনুযায়ী filter করা
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# জোড় সংখ্যা
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# 5 এর বড় সংখ্যা
greater = list(filter(lambda x: x > 5, numbers))
print(greater)  # [6, 7, 8, 9, 10]
```

#### reduce() - একটা value তে reduce করা
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# যোগফল
sum = reduce(lambda x, y: x + y, numbers)
print(sum)  # 15

# গুণফল
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 120
```

## Recursion (পুনরাবৃত্তি)

Recursion হলো যখন একটা function নিজেকে call করে।

### Basic Recursion Example
```python
# Countdown
def countdown(n):
    if n <= 0:  # Base case
        print("শেষ!")
        return
    print(n)
    countdown(n - 1)  # Recursive call

countdown(5)
# Output: 5 4 3 2 1 শেষ!
```

### Factorial (গুণফল)
```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

print(factorial(5))  # 120
# 5! = 5 × 4 × 3 × 2 × 1 = 120
```

### Fibonacci Series
```python
def fibonacci(n):
    # Base cases
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    return fibonacci(n-1) + fibonacci(n-2)

# First 10 Fibonacci numbers
for i in range(10):
    print(fibonacci(i), end=" ")
# Output: 0 1 1 2 3 5 8 13 21 34
```

### Sum of Digits
```python
def sum_digits(n):
    # Base case
    if n == 0:
        return 0
    # Recursive case
    return n % 10 + sum_digits(n // 10)

print(sum_digits(1234))  # 10 (1+2+3+4)
print(sum_digits(9876))  # 30 (9+8+7+6)
```

### Power Calculation
```python
def power(base, exp):
    # Base case
    if exp == 0:
        return 1
    # Recursive case
    return base * power(base, exp - 1)

print(power(2, 5))  # 32 (2⁵)
print(power(3, 4))  # 81 (3⁴)
```

### Sum of List
```python
def sum_list(lst):
    # Base case
    if len(lst) == 0:
        return 0
    # Recursive case
    return lst[0] + sum_list(lst[1:])

numbers = [1, 2, 3, 4, 5]
print(sum_list(numbers))  # 15
```

### Binary Search (Recursive)
```python
def binary_search(arr, target, left, right):
    # Base case
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search(arr, target, left, mid - 1)
    else:
        return binary_search(arr, target, mid + 1, right)

numbers = [1, 3, 5, 7, 9, 11, 13, 15]
result = binary_search(numbers, 7, 0, len(numbers) - 1)
print(result)  # 3 (index)
```

## Docstring এবং Help

### Docstring লেখা
```python
def greet(name):
    """
    এই ফাংশন একটি অভিবাদন বার্তা প্রিন্ট করে।
    
    Parameters:
        name (str): ব্যক্তির নাম
    
    Returns:
        None
    """
    print(f"হ্যালো, {name}!")

# Docstring দেখা
print(greet.__doc__)

# help() function
help(greet)
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: Prime Number Check
```python
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

# Test
for num in range(1, 21):
    if is_prime(num):
        print(num, end=" ")
# Output: 2 3 5 7 11 13 17 19
```

### প্রব্লেম ২: Palindrome Check
```python
def is_palindrome(text):
    text = text.lower().replace(" ", "")
    return text == text[::-1]

print(is_palindrome("madam"))        # True
print(is_palindrome("hello"))        # False
print(is_palindrome("A man a plan a canal Panama"))  # True
```

### প্রব্লেম ৩: GCD (Greatest Common Divisor)
```python
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

print(gcd(48, 18))   # 6
print(gcd(100, 50))  # 50
```

### প্রব্লেম ৪: List Reverse (Recursive)
```python
def reverse_list(lst):
    if len(lst) == 0:
        return []
    return [lst[-1]] + reverse_list(lst[:-1])

numbers = [1, 2, 3, 4, 5]
print(reverse_list(numbers))  # [5, 4, 3, 2, 1]
```

### প্রব্লেম ৫: Temperature Converter
```python
def celsius_to_fahrenheit(celsius):
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

print(f"25°C = {celsius_to_fahrenheit(25)}°F")
print(f"77°F = {fahrenheit_to_celsius(77)}°C")
```

### প্রব্লেম ৬: Calculator
```python
def calculator(a, b, operation):
    operations = {
        '+': lambda x, y: x + y,
        '-': lambda x, y: x - y,
        '*': lambda x, y: x * y,
        '/': lambda x, y: x / y if y != 0 else "ভাগ করা যাবে না"
    }
    
    if operation in operations:
        return operations[operation](a, b)
    return "ভুল অপারেশন"

print(calculator(10, 5, '+'))  # 15
print(calculator(10, 5, '-'))  # 5
print(calculator(10, 5, '*'))  # 50
print(calculator(10, 5, '/'))  # 2.0
```

## গুরুত্বপূর্ণ পয়েন্টস
- Function code reusability বাড়ায়
- Default parameters optional arguments দেয়
- *args যেকোনো সংখ্যক positional arguments নেয়
- **kwargs যেকোনো সংখ্যক keyword arguments নেয়
- Lambda functions ছোট anonymous functions
- map() সব elements এ function apply করে
- filter() শর্ত অনুযায়ী filter করে
- Recursion এ base case অবশ্যই থাকতে হবে
- Recursion memory বেশি ব্যবহার করে
- Docstring documentation এর জন্য গুরুত্বপূর্ণ
