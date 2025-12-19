# Lecture 5: Loops in Python | While & For Loops

## লুপ কি? (What is a Loop?)

লুপ হলো একটি code block যা বারবার execute হয়। Python-এ দুই ধরনের লুপ আছে:
1. **while loop** - condition সত্য থাকা পর্যন্ত চলবে
2. **for loop** - একটা sequence এর প্রতিটা element এর জন্য চলবে

## While Loop

### Basic While Loop
```python
# 1 থেকে 5 পর্যন্ত প্রিন্ট করা
i = 1
while i <= 5:
    print(i)
    i += 1  # i = i + 1

# Output: 1 2 3 4 5
```

### While Loop এর Structure
```python
# Structure
while condition:
    # code block
    # update counter
```

### While Loop Examples
```python
# উদাহরণ ১: যোগফল বের করা
sum = 0
i = 1
while i <= 10:
    sum += i
    i += 1
print("যোগফল:", sum)  # 55

# উদাহরণ ২: গুণফল বের করা (Factorial)
n = 5
factorial = 1
i = 1
while i <= n:
    factorial *= i
    i += 1
print(f"{n}! = {factorial}")  # 120

# উদাহরণ ৩: Countdown
count = 5
while count > 0:
    print(count)
    count -= 1
print("শেষ!")

# উদাহরণ ৪: ব্যবহারকারীর ইনপুট নেওয়া
password = ""
while password != "secret":
    password = input("পাসওয়ার্ড দিন: ")
print("সঠিক পাসওয়ার্ড!")
```

### Infinite Loop (অসীম লুপ)
```python
# সাবধান! এটি কখনো শেষ হবে না
# while True:
#     print("চলতেই থাকবে")

# Ctrl+C চাপলে বন্ধ হবে
```

## For Loop

### Basic For Loop
```python
# List দিয়ে
fruits = ["আম", "কলা", "আপেল"]
for fruit in fruits:
    print(fruit)

# String দিয়ে
name = "Python"
for char in name:
    print(char)

# Range দিয়ে
for i in range(5):
    print(i)  # 0 1 2 3 4
```

### Range Function

#### range(stop)
```python
# 0 থেকে 4 পর্যন্ত
for i in range(5):
    print(i)  # 0 1 2 3 4
```

#### range(start, stop)
```python
# 1 থেকে 5 পর্যন্ত
for i in range(1, 6):
    print(i)  # 1 2 3 4 5
```

#### range(start, stop, step)
```python
# 0 থেকে 10, প্রতি 2 করে
for i in range(0, 11, 2):
    print(i)  # 0 2 4 6 8 10

# উল্টো গণনা
for i in range(10, 0, -1):
    print(i)  # 10 9 8 7 6 5 4 3 2 1

# জোড় সংখ্যা
for i in range(2, 11, 2):
    print(i)  # 2 4 6 8 10
```

### For Loop Examples
```python
# উদাহরণ ১: List এর যোগফল
numbers = [10, 20, 30, 40, 50]
total = 0
for num in numbers:
    total += num
print("যোগফল:", total)  # 150

# উদাহরণ ২: Multiplication Table
n = 5
for i in range(1, 11):
    print(f"{n} × {i} = {n * i}")

# উদাহরণ ৩: List এর প্রতিটা element double করা
numbers = [1, 2, 3, 4, 5]
doubled = []
for num in numbers:
    doubled.append(num * 2)
print(doubled)  # [2, 4, 6, 8, 10]

# উদাহরণ ৪: Dictionary iteration
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}
for key, value in student.items():
    print(f"{key}: {value}")
```

## Nested Loops (ভিতরে লুপ)

### Basic Nested Loop
```python
# Multiplication Table (1 থেকে 5)
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i} × {j} = {i*j}")
    print()  # খালি লাইন
```

### Pattern Printing
```python
# Pattern 1: Square
for i in range(5):
    for j in range(5):
        print("*", end=" ")
    print()

# Output:
# * * * * *
# * * * * *
# * * * * *
# * * * * *
# * * * * *

# Pattern 2: Right Triangle
for i in range(1, 6):
    for j in range(i):
        print("*", end=" ")
    print()

# Output:
# *
# * *
# * * *
# * * * *
# * * * * *

# Pattern 3: Number Pattern
for i in range(1, 6):
    for j in range(1, i+1):
        print(j, end=" ")
    print()

# Output:
# 1
# 1 2
# 1 2 3
# 1 2 3 4
# 1 2 3 4 5
```

## Loop Control Statements

### break - লুপ থেকে বের হওয়া
```python
# উদাহরণ ১: নির্দিষ্ট সংখ্যা পেলে বন্ধ
for i in range(1, 11):
    if i == 5:
        break
    print(i)
# Output: 1 2 3 4

# উদাহরণ ২: ব্যবহারকারীর ইনপুট
while True:
    password = input("পাসওয়ার্ড (বা 'quit'): ")
    if password == "quit":
        break
    if password == "secret":
        print("সঠিক!")
        break
    print("ভুল! আবার চেষ্টা করুন")

# উদাহরণ ৩: List এ search
numbers = [10, 20, 30, 40, 50]
search = 30
found = False
for num in numbers:
    if num == search:
        print(f"{search} পাওয়া গেছে!")
        found = True
        break
if not found:
    print(f"{search} পাওয়া যায়নি")
```

### continue - বর্তমান iteration skip করা
```python
# উদাহরণ ১: বিজোড় সংখ্যা skip করা
for i in range(1, 11):
    if i % 2 != 0:
        continue
    print(i)
# Output: 2 4 6 8 10

# উদাহরণ ২: নির্দিষ্ট মান বাদ দেওয়া
numbers = [1, 2, 3, -1, 4, 5, -2, 6]
for num in numbers:
    if num < 0:
        continue
    print(num)
# Output: 1 2 3 4 5 6

# উদাহরণ ৩: 5 এর গুণিতক skip
for i in range(1, 21):
    if i % 5 == 0:
        continue
    print(i)
```

### pass - কিছু না করা (placeholder)
```python
# খালি loop (পরে লিখবেন)
for i in range(5):
    pass  # TODO: পরে implement করব

# খালি function
def my_function():
    pass  # পরে code লিখব

# Condition এ
if True:
    pass  # এখনো কিছু করব না
```

### else with Loops
```python
# for-else: loop সম্পূর্ণ শেষ হলে else চলবে
for i in range(5):
    print(i)
else:
    print("Loop শেষ!")

# break হলে else চলবে না
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("এটি print হবে না")

# while-else
count = 0
while count < 5:
    print(count)
    count += 1
else:
    print("While loop শেষ!")

# Practical example: Prime number check
num = 17
for i in range(2, num):
    if num % i == 0:
        print(f"{num} মৌলিক সংখ্যা নয়")
        break
else:
    print(f"{num} মৌলিক সংখ্যা")
```

## enumerate() এবং zip()

### enumerate() - Index এবং Value একসাথে
```python
fruits = ["আম", "কলা", "আপেল", "আঙুর"]

# Without enumerate
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# With enumerate (ভালো পদ্ধতি)
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Custom start index
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")

# Output:
# 1. আম
# 2. কলা
# 3. আপেল
# 4. আঙুর
```

### zip() - একাধিক List একসাথে iterate করা
```python
names = ["রহিম", "করিম", "জামাল"]
ages = [20, 22, 25]
cities = ["ঢাকা", "চট্টগ্রাম", "সিলেট"]

# zip দিয়ে
for name, age, city in zip(names, ages, cities):
    print(f"{name}, {age} বছর, {city}")

# Output:
# রহিম, 20 বছর, ঢাকা
# করিম, 22 বছর, চট্টগ্রাম
# জামাল, 25 বছর, সিলেট

# Dictionary তৈরি করা
person_dict = dict(zip(names, ages))
print(person_dict)
# {'রহিম': 20, 'করিম': 22, 'জামাল': 25}
```

## List Comprehension (লুপ এর ছোট রূপ)
```python
# Traditional for loop
squares = []
for i in range(1, 6):
    squares.append(i * i)
print(squares)  # [1, 4, 9, 16, 25]

# List comprehension (এক লাইনে)
squares = [i * i for i in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# With condition
evens = [i for i in range(1, 11) if i % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# String manipulation
fruits = ["আম", "কলা", "আপেল"]
upper_fruits = [fruit.upper() for fruit in fruits]
print(upper_fruits)

# Nested list comprehension
matrix = [[i*j for j in range(1, 4)] for i in range(1, 4)]
print(matrix)
# [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: Fibonacci Series
```python
n = 10
a, b = 0, 1
print("Fibonacci Series:")
for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
# Output: 0 1 1 2 3 5 8 13 21 34
```

### প্রব্লেম ২: Prime Numbers (1 থেকে 50)
```python
print("মৌলিক সংখ্যা:")
for num in range(2, 51):
    is_prime = True
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            is_prime = False
            break
    if is_prime:
        print(num, end=" ")
```

### প্রব্লেম ৩: Palindrome Check
```python
text = input("শব্দ লিখুন: ")
is_palindrome = True

for i in range(len(text) // 2):
    if text[i] != text[-(i+1)]:
        is_palindrome = False
        break

if is_palindrome:
    print("Palindrome!")
else:
    print("Palindrome নয়")
```

### প্রব্লেম ৪: Armstrong Number
```python
# Armstrong: 153 = 1³ + 5³ + 3³ = 1 + 125 + 27 = 153
num = int(input("সংখ্যা দিন: "))
original = num
sum = 0
digits = len(str(num))

while num > 0:
    digit = num % 10
    sum += digit ** digits
    num //= 10

if sum == original:
    print(f"{original} Armstrong সংখ্যা")
else:
    print(f"{original} Armstrong সংখ্যা নয়")
```

### প্রব্লেম ৫: Pattern Printing (Pyramid)
```python
n = 5
# Upper part
for i in range(1, n+1):
    print(" " * (n-i) + "*" * (2*i-1))

# Output:
#     *
#    ***
#   *****
#  *******
# *********
```

### প্রব্লেম ৬: Guess the Number Game
```python
import random

secret = random.randint(1, 100)
attempts = 0
max_attempts = 7

print("1 থেকে 100 এর মধ্যে একটা সংখ্যা guess করুন!")

while attempts < max_attempts:
    guess = int(input("আপনার guess: "))
    attempts += 1
    
    if guess == secret:
        print(f"অভিনন্দন! {attempts} attempt এ সফল!")
        break
    elif guess < secret:
        print("আরো বড় সংখ্যা try করুন")
    else:
        print("আরো ছোট সংখ্যা try করুন")
else:
    print(f"দুঃখিত! সংখ্যাটি ছিল {secret}")
```

## While vs For Loop

| বৈশিষ্ট্য | While Loop | For Loop |
|---------|-----------|----------|
| ব্যবহার | শর্তের উপর নির্ভর করে | নির্দিষ্ট সংখ্যক iteration |
| Syntax | while condition: | for item in sequence: |
| Counter | নিজে manage করতে হয় | automatic |
| Infinite Loop | সহজে হতে পারে | কঠিন |
| Use Case | অজানা iteration সংখ্যা | জানা iteration সংখ্যা |

## গুরুত্বপূর্ণ পয়েন্টস
- While loop শর্ত সত্য থাকলে চলবে
- For loop sequence এর প্রতিটা element iterate করে
- range() দিয়ে সংখ্যার sequence তৈরি করা যায়
- break লুপ বন্ধ করে
- continue বর্তমান iteration skip করে
- pass placeholder হিসেবে ব্যবহার হয়
- enumerate() index এবং value একসাথে দেয়
- zip() একাধিক sequence একসাথে iterate করে
- List comprehension লুপের ছোট রূপ
- Infinite loop থেকে সাবধান থাকুন
