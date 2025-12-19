# Lecture 2: Strings & Conditional Statements

## স্ট্রিং (Strings)

স্ট্রিং হলো ক্যারেক্টারের একটি সিকোয়েন্স। Python-এ স্ট্রিং তৈরি করতে single (''), double (""), বা triple (""" """) quotes ব্যবহার করা হয়।

### স্ট্রিং তৈরি করা
```python
# বিভিন্ন উপায়ে স্ট্রিং তৈরি
name = "বাংলাদেশ"
city = 'ঢাকা'
message = """এটি একটি
মাল্টি-লাইন
স্ট্রিং"""

# Empty String
empty = ""
```

### স্ট্রিং ইনডেক্সিং (String Indexing)
```python
text = "Python"
#       012345 (পজিটিভ ইনডেক্স)
#      -654321 (নেগেটিভ ইনডেক্স)

print(text[0])   # P
print(text[2])   # t
print(text[-1])  # n (শেষ ক্যারেক্টার)
print(text[-2])  # o
```

### স্ট্রিং স্লাইসিং (String Slicing)
```python
text = "Bangladesh"

print(text[0:5])    # Bangl
print(text[5:])     # adesh
print(text[:5])     # Bangl
print(text[-4:])    # desh
print(text[::2])    # Bnlds (প্রতি ২টা করে নিবে)
print(text[::-1])   # hsedalgnaB (উল্টো)
```

### স্ট্রিং মেথডস (String Methods)

#### ১. Case Conversion
```python
text = "Hello Bangladesh"

print(text.upper())        # HELLO BANGLADESH
print(text.lower())        # hello bangladesh
print(text.capitalize())   # Hello bangladesh
print(text.title())        # Hello Bangladesh
print(text.swapcase())     # hELLO bANGLADESH
```

#### ২. Searching & Checking
```python
text = "Python Programming"

print(text.find("Pro"))        # 7 (পজিশন)
print(text.find("Java"))       # -1 (না পেলে)
print(text.count("o"))         # 2 (কতবার আছে)
print(text.startswith("Py"))   # True
print(text.endswith("ing"))    # True
print("123".isdigit())         # True
print("abc".isalpha())         # True
print("abc123".isalnum())      # True
```

#### ৩. Whitespace Handling
```python
text = "  Hello World  "

print(text.strip())   # "Hello World" (দুই পাশের স্পেস)
print(text.lstrip())  # "Hello World  " (বাম পাশের স্পেস)
print(text.rstrip())  # "  Hello World" (ডান পাশের স্পেস)
```

#### ৪. Replace & Split
```python
text = "I love Java"
print(text.replace("Java", "Python"))  # I love Python

sentence = "Python is awesome"
words = sentence.split()  # ['Python', 'is', 'awesome']

csv = "apple,banana,orange"
fruits = csv.split(",")  # ['apple', 'banana', 'orange']
```

#### ৫. Join
```python
words = ["Python", "is", "fun"]
sentence = " ".join(words)  # "Python is fun"

fruits = ["apple", "banana", "orange"]
csv = ", ".join(fruits)  # "apple, banana, orange"
```

### স্ট্রিং কনক্যাটেনেশন (String Concatenation)
```python
first_name = "রহিম"
last_name = "করিম"

# + অপারেটর দিয়ে
full_name = first_name + " " + last_name
print(full_name)  # রহিম করিম

# String formatting
age = 25
message = "আমার নাম " + first_name + " এবং বয়স " + str(age)
```

### String Formatting

#### ১. f-strings (সবচেয়ে ভালো)
```python
name = "রহিম"
age = 25
city = "ঢাকা"

# f-string ব্যবহার
message = f"আমার নাম {name}, বয়স {age} এবং আমি {city} থেকে এসেছি"
print(message)

# Calculation in f-string
price = 100
quantity = 5
print(f"মোট: {price * quantity} টাকা")
```

#### ২. format() method
```python
name = "করিম"
age = 30
print("নাম: {}, বয়স: {}".format(name, age))
print("নাম: {0}, বয়স: {1}".format(name, age))
print("নাম: {n}, বয়স: {a}".format(n=name, a=age))
```

## Conditional Statements (শর্ত)

### if Statement
```python
age = 18

if age >= 18:
    print("আপনি ভোট দিতে পারবেন")
```

### if-else Statement
```python
marks = 55

if marks >= 60:
    print("পাস")
else:
    print("ফেল")
```

### if-elif-else Statement
```python
marks = 75

if marks >= 80:
    print("গ্রেড: A+")
elif marks >= 70:
    print("গ্রেড: A")
elif marks >= 60:
    print("গ্রেড: A-")
elif marks >= 50:
    print("গ্রেড: B")
else:
    print("গ্রেড: F")
```

### Nested if (ভিতরে if)
```python
age = 25
has_license = True

if age >= 18:
    if has_license:
        print("আপনি গাড়ি চালাতে পারবেন")
    else:
        print("আপনার লাইসেন্স লাগবে")
else:
    print("আপনি নাবালক")
```

### Logical Operators in Conditions
```python
age = 25
salary = 30000

# and - দুইটাই সত্য হতে হবে
if age >= 18 and salary >= 25000:
    print("লোন পাবেন")

# or - যেকোনো একটা সত্য হলেই হবে
if age < 18 or age > 60:
    print("বিশেষ ছাড়")

# not - উল্টা
is_student = True
if not is_student:
    print("ছাত্র নয়")
```

### Ternary Operator (এক লাইনে if-else)
```python
age = 20
status = "প্রাপ্তবয়স্ক" if age >= 18 else "নাবালক"
print(status)

# আরেকটি উদাহরণ
marks = 75
result = "পাস" if marks >= 60 else "ফেল"
print(result)
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: ইমেইল ভ্যালিডেশন
```python
email = input("ইমেইল লিখুন: ")

if "@" in email and "." in email:
    print("সঠিক ইমেইল")
else:
    print("ভুল ইমেইল")
```

### প্রব্লেম ২: পাসওয়ার্ড চেক
```python
password = input("পাসওয়ার্ড দিন: ")
length = len(password)

if length >= 8:
    print("শক্তিশালী পাসওয়ার্ড")
elif length >= 6:
    print("মাঝারি পাসওয়ার্ড")
else:
    print("দুর্বল পাসওয়ার্ড")
```

### প্রব্লেম ৩: লিপ ইয়ার চেক
```python
year = int(input("বছর লিখুন: "))

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"{year} লিপ ইয়ার")
else:
    print(f"{year} লিপ ইয়ার নয়")
```

### প্রব্লেম ৪: সবচেয়ে বড় সংখ্যা খুঁজুন
```python
a = int(input("প্রথম সংখ্যা: "))
b = int(input("দ্বিতীয় সংখ্যা: "))
c = int(input("তৃতীয় সংখ্যা: "))

if a >= b and a >= c:
    print(f"সবচেয়ে বড়: {a}")
elif b >= a and b >= c:
    print(f"সবচেয়ে বড়: {b}")
else:
    print(f"সবচেয়ে বড়: {c}")
```

### প্রব্লেম ৫: BMI ক্যালকুলেটর
```python
weight = float(input("ওজন (kg): "))
height = float(input("উচ্চতা (m): "))

bmi = weight / (height ** 2)

print(f"BMI: {bmi:.2f}")

if bmi < 18.5:
    print("কম ওজন")
elif bmi < 25:
    print("স্বাভাবিক ওজন")
elif bmi < 30:
    print("বেশি ওজন")
else:
    print("স্থূলতা")
```

## গুরুত্বপূর্ণ পয়েন্টস
- স্ট্রিং immutable (পরিবর্তন করা যায় না)
- ইনডেক্স 0 থেকে শুরু হয়
- নেগেটিভ ইনডেক্স শেষ থেকে গণনা করে
- f-string সবচেয়ে আধুনিক এবং সহজ
- if-elif-else এর ক্রম গুরুত্বপূর্ণ
- Indentation (স্পেস) খুবই গুরুত্বপূর্ণ Python-এ
- and, or, not লজিক্যাল অপারেটর
