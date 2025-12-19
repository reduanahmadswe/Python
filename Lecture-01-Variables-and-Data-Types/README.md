# Lecture 1: Variables & Data Types

## ভেরিয়েবল (Variables)

ভেরিয়েবল হলো একটি কন্টেইনার যেখানে আমরা ডেটা সংরক্ষণ করি। Python-এ ভেরিয়েবল ডিক্লেয়ার করার জন্য কোন কীওয়ার্ড লাগে না।

### ভেরিয়েবল তৈরির নিয়ম:
```python
# সঠিক পদ্ধতি
name = "রহিম"
age = 25
price = 99.99
is_student = True

# ভেরিয়েবল নামকরণের নিয়ম
my_name = "করিম"      # ভালো
myName = "জামাল"       # ভালো (Camel Case)
_private = 10          # ভালো
name123 = "সালাম"      # ভালো

# ভুল নামকরণ
# 123name = "ভুল"      # সংখ্যা দিয়ে শুরু করা যাবে না
# my-name = "ভুল"      # হাইফেন ব্যবহার করা যাবে না
# my name = "ভুল"      # স্পেস ব্যবহার করা যাবে না
```

## ডেটা টাইপস (Data Types)

### ১. Integer (পূর্ণ সংখ্যা)
```python
age = 25
year = 2025
marks = -50
big_number = 1000000
```

### ২. Float (দশমিক সংখ্যা)
```python
price = 99.99
pi = 3.14159
temperature = -5.5
percentage = 85.5
```

### ৩. String (টেক্সট/স্ট্রিং)
```python
name = "বাংলাদেশ"
city = 'ঢাকা'
message = """এটি একটি
মাল্টি-লাইন
স্ট্রিং"""
```

### ৪. Boolean (সত্য/মিথ্যা)
```python
is_student = True
is_passed = False
has_license = True
```

### ৫. None (কিছু নেই)
```python
result = None
data = None
```

## টাইপ চেকিং (Type Checking)
```python
x = 10
print(type(x))  # <class 'int'>

y = 3.14
print(type(y))  # <class 'float'>

name = "Python"
print(type(name))  # <class 'str'>

flag = True
print(type(flag))  # <class 'bool'>
```

## টাইপ কনভার্সন (Type Conversion)
```python
# String থেকে Integer
age_str = "25"
age_int = int(age_str)
print(age_int)  # 25

# Integer থেকে Float
num = 10
num_float = float(num)
print(num_float)  # 10.0

# Integer থেকে String
marks = 95
marks_str = str(marks)
print(marks_str)  # "95"

# Float থেকে Integer
price = 99.99
price_int = int(price)
print(price_int)  # 99
```

## ইনপুট নেওয়া (Taking Input)
```python
# ব্যবহারকারী থেকে ইনপুট নেওয়া
name = input("আপনার নাম কি? ")
print("হ্যালো,", name)

# সংখ্যা ইনপুট নেওয়া
age = int(input("আপনার বয়স কত? "))
print("আপনার বয়স:", age)

# দশমিক সংখ্যা ইনপুট
price = float(input("দাম কত? "))
print("দাম:", price)
```

## অপারেটরস (Operators)

### ১. Arithmetic Operators (গাণিতিক অপারেটর)
```python
a = 10
b = 3

print(a + b)   # যোগ = 13
print(a - b)   # বিয়োগ = 7
print(a * b)   # গুণ = 30
print(a / b)   # ভাগ = 3.333...
print(a // b)  # পূর্ণ ভাগ = 3
print(a % b)   # ভাগশেষ = 1
print(a ** b)  # ঘাত = 1000
```

### ২. Comparison Operators (তুলনা অপারেটর)
```python
x = 5
y = 10

print(x == y)  # সমান কিনা? False
print(x != y)  # অসমান কিনা? True
print(x > y)   # বড় কিনা? False
print(x < y)   # ছোট কিনা? True
print(x >= y)  # বড় বা সমান? False
print(x <= y)  # ছোট বা সমান? True
```

### ৩. Logical Operators (লজিক্যাল অপারেটর)
```python
a = True
b = False

print(a and b)  # এবং = False
print(a or b)   # অথবা = True
print(not a)    # না = False
```

### ৪. Assignment Operators (অ্যাসাইনমেন্ট অপারেটর)
```python
x = 10
x += 5   # x = x + 5 = 15
x -= 3   # x = x - 3 = 12
x *= 2   # x = x * 2 = 24
x /= 4   # x = x / 4 = 6.0
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: দুইটি সংখ্যা যোগ করা
```python
num1 = int(input("প্রথম সংখ্যা: "))
num2 = int(input("দ্বিতীয় সংখ্যা: "))
sum = num1 + num2
print("যোগফল:", sum)
```

### প্রব্লেম ২: আয়তক্ষেত্রের ক্ষেত্রফল
```python
length = float(input("দৈর্ঘ্য: "))
width = float(input("প্রস্থ: "))
area = length * width
print("ক্ষেত্রফল:", area)
```

### প্রব্লেম ৩: তাপমাত্রা রূপান্তর (Celsius to Fahrenheit)
```python
celsius = float(input("সেলসিয়াস তাপমাত্রা: "))
fahrenheit = (celsius * 9/5) + 32
print("ফারেনহাইট:", fahrenheit)
```

## গুরুত্বপূর্ণ পয়েন্টস
- Python case-sensitive (বড় ছোট হাতের পার্থক্য আছে)
- ভেরিয়েবল নাম অর্থবহ হওয়া উচিত
- সংখ্যা দিয়ে ভেরিয়েবল শুরু করা যায় না
- input() ফাংশন সবসময় string রিটার্ন করে
- টাইপ কনভার্সন করার সময় সাবধান থাকতে হবে
