# Lecture 3: List & Tuple in Python

## লিস্ট (List)

লিস্ট হলো Python-এর একটি ডেটা স্ট্রাকচার যেখানে একাধিক আইটেম সংরক্ষণ করা যায়। লিস্ট **mutable** (পরিবর্তনযোগ্য)।

### লিস্ট তৈরি করা
```python
# খালি লিস্ট
empty_list = []
empty_list2 = list()

# বিভিন্ন টাইপের লিস্ট
numbers = [1, 2, 3, 4, 5]
names = ["রহিম", "করিম", "জামাল"]
mixed = [1, "Python", 3.14, True]
nested = [[1, 2], [3, 4], [5, 6]]

print(numbers)  # [1, 2, 3, 4, 5]
print(len(numbers))  # 5 (লিস্টের দৈর্ঘ্য)
```

### লিস্ট ইনডেক্সিং (List Indexing)
```python
fruits = ["আম", "কলা", "আপেল", "আঙুর"]
#         0      1      2       3     (পজিটিভ)
#        -4     -3     -2      -1     (নেগেটিভ)

print(fruits[0])    # আম
print(fruits[2])    # আপেল
print(fruits[-1])   # আঙুর (শেষ আইটেম)
print(fruits[-2])   # আপেল
```

### লিস্ট স্লাইসিং (List Slicing)
```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[2:5])     # [2, 3, 4]
print(numbers[:5])      # [0, 1, 2, 3, 4]
print(numbers[5:])      # [5, 6, 7, 8, 9]
print(numbers[::2])     # [0, 2, 4, 6, 8] (প্রতি ২টা করে)
print(numbers[::-1])    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] (উল্টো)
print(numbers[2:8:2])   # [2, 4, 6]
```

### লিস্ট মেথডস (List Methods)

#### ১. Adding Elements (যোগ করা)
```python
fruits = ["আম", "কলা"]

# append() - শেষে একটা যোগ
fruits.append("আপেল")
print(fruits)  # ["আম", "কলা", "আপেল"]

# insert() - নির্দিষ্ট জায়গায় যোগ
fruits.insert(1, "আঙুর")
print(fruits)  # ["আম", "আঙুর", "কলা", "আপেল"]

# extend() - একাধিক যোগ
more_fruits = ["লিচু", "জাম"]
fruits.extend(more_fruits)
print(fruits)  # ["আম", "আঙুর", "কলা", "আপেল", "লিচু", "জাম"]
```

#### ২. Removing Elements (মুছে ফেলা)
```python
numbers = [1, 2, 3, 4, 5, 3]

# remove() - প্রথম occurrence মুছবে
numbers.remove(3)
print(numbers)  # [1, 2, 4, 5, 3]

# pop() - শেষ আইটেম মুছবে এবং রিটার্ন করবে
last = numbers.pop()
print(last)     # 3
print(numbers)  # [1, 2, 4, 5]

# pop(index) - নির্দিষ্ট ইনডেক্সের আইটেম মুছবে
second = numbers.pop(1)
print(second)   # 2
print(numbers)  # [1, 4, 5]

# clear() - সব মুছে দেবে
numbers.clear()
print(numbers)  # []

# del - আইটেম বা পুরো লিস্ট মুছবে
nums = [1, 2, 3, 4, 5]
del nums[0]     # প্রথম আইটেম মুছবে
print(nums)     # [2, 3, 4, 5]
del nums[1:3]   # ইনডেক্স 1 থেকে 2 মুছবে
print(nums)     # [2, 5]
```

#### ৩. Searching & Counting
```python
numbers = [1, 2, 3, 4, 3, 5, 3]

# index() - প্রথম occurrence এর ইনডেক্স
pos = numbers.index(3)
print(pos)  # 2

# count() - কতবার আছে
count = numbers.count(3)
print(count)  # 3

# in operator - আছে কিনা
if 4 in numbers:
    print("4 আছে")

if 10 not in numbers:
    print("10 নেই")
```

#### ৪. Sorting & Reversing
```python
numbers = [5, 2, 8, 1, 9, 3]

# sort() - ascending order (ছোট থেকে বড়)
numbers.sort()
print(numbers)  # [1, 2, 3, 5, 8, 9]

# sort(reverse=True) - descending order (বড় থেকে ছোট)
numbers.sort(reverse=True)
print(numbers)  # [9, 8, 5, 3, 2, 1]

# reverse() - উল্টো করবে
numbers.reverse()
print(numbers)  # [1, 2, 3, 5, 8, 9]

# sorted() - নতুন sorted লিস্ট রিটার্ন করে (original unchanged)
original = [5, 2, 8, 1]
sorted_list = sorted(original)
print(original)     # [5, 2, 8, 1]
print(sorted_list)  # [1, 2, 5, 8]
```

#### ৫. Other Methods
```python
numbers = [1, 2, 3]

# copy() - লিস্ট কপি করা
numbers_copy = numbers.copy()
print(numbers_copy)  # [1, 2, 3]

# + operator - দুইটা লিস্ট জোড়া
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # [1, 2, 3, 4, 5, 6]

# * operator - লিস্ট repeat করা
zeros = [0] * 5
print(zeros)  # [0, 0, 0, 0, 0]
```

### লিস্ট কম্প্রিহেনশন (List Comprehension)
```python
# Traditional way
squares = []
for i in range(1, 6):
    squares.append(i * i)
print(squares)  # [1, 4, 9, 16, 25]

# List Comprehension (এক লাইনে)
squares = [i * i for i in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# With condition
evens = [i for i in range(1, 11) if i % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# String manipulation
names = ["রহিম", "করিম", "জামাল"]
upper_names = [name.upper() for name in names]
print(upper_names)
```

## টাপল (Tuple)

টাপল হলো লিস্টের মতোই কিন্তু **immutable** (পরিবর্তন করা যায় না)। একবার তৈরি হলে আর পরিবর্তন করা যায় না।

### টাপল তৈরি করা
```python
# বিভিন্ন উপায়ে টাপল তৈরি
empty_tuple = ()
single = (1,)  # একটা আইটেমের জন্য কমা লাগবে
numbers = (1, 2, 3, 4, 5)
mixed = (1, "Python", 3.14, True)
nested = ((1, 2), (3, 4), (5, 6))

# Without parentheses
coordinates = 10, 20, 30
print(coordinates)  # (10, 20, 30)
print(type(coordinates))  # <class 'tuple'>
```

### টাপল ইনডেক্সিং এবং স্লাইসিং
```python
fruits = ("আম", "কলা", "আপেল", "আঙুর")

# Indexing
print(fruits[0])    # আম
print(fruits[-1])   # আঙুর

# Slicing
print(fruits[1:3])  # ("কলা", "আপেল")
print(fruits[:2])   # ("আম", "কলা")
print(fruits[2:])   # ("আপেল", "আঙুর")
```

### টাপল মেথডস (Tuple Methods)
```python
numbers = (1, 2, 3, 2, 4, 2, 5)

# count() - কতবার আছে
count = numbers.count(2)
print(count)  # 3

# index() - প্রথম occurrence এর ইনডেক্স
pos = numbers.index(3)
print(pos)  # 2

# len() - দৈর্ঘ্য
length = len(numbers)
print(length)  # 7

# in operator
if 3 in numbers:
    print("3 আছে")
```

### টাপল আনপ্যাকিং (Tuple Unpacking)
```python
# Basic unpacking
coordinates = (10, 20)
x, y = coordinates
print(x)  # 10
print(y)  # 20

# Multiple values
person = ("রহিম", 25, "ঢাকা")
name, age, city = person
print(f"নাম: {name}, বয়স: {age}, শহর: {city}")

# Swapping values
a = 5
b = 10
a, b = b, a
print(a, b)  # 10 5

# * operator
numbers = (1, 2, 3, 4, 5)
first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5
```

### লিস্ট vs টাপল (List vs Tuple)

| বৈশিষ্ট্য | লিস্ট | টাপল |
|---------|------|------|
| Syntax | [1, 2, 3] | (1, 2, 3) |
| Mutable | হ্যাঁ | না |
| Add/Remove | পারবেন | পারবেন না |
| Speed | একটু ধীর | একটু দ্রুত |
| Memory | বেশি | কম |
| Use Case | পরিবর্তনশীল ডেটা | স্থির ডেটা |

```python
# List - পরিবর্তন করা যায়
my_list = [1, 2, 3]
my_list[0] = 10
my_list.append(4)
print(my_list)  # [10, 2, 3, 4]

# Tuple - পরিবর্তন করা যায় না
my_tuple = (1, 2, 3)
# my_tuple[0] = 10  # Error!
# my_tuple.append(4)  # Error!
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: লিস্টের সর্বোচ্চ এবং সর্বনিম্ন সংখ্যা
```python
numbers = [45, 12, 78, 23, 91, 5, 67]

maximum = max(numbers)
minimum = min(numbers)
total = sum(numbers)
average = total / len(numbers)

print(f"সর্বোচ্চ: {maximum}")
print(f"সর্বনিম্ন: {minimum}")
print(f"যোগফল: {total}")
print(f"গড়: {average:.2f}")
```

### প্রব্লেম ২: লিস্ট থেকে ডুপ্লিকেট মুছুন
```python
numbers = [1, 2, 3, 2, 4, 3, 5, 1]

# Method 1: Using set
unique = list(set(numbers))
print(unique)

# Method 2: Using loop
unique = []
for num in numbers:
    if num not in unique:
        unique.append(num)
print(unique)
```

### প্রব্লেম ৩: দুইটা লিস্ট মার্জ এবং সর্ট
```python
list1 = [1, 3, 5, 7]
list2 = [2, 4, 6, 8]

merged = list1 + list2
merged.sort()
print(merged)  # [1, 2, 3, 4, 5, 6, 7, 8]
```

### প্রব্লেম ৪: লিস্ট রিভার্স করুন (বিভিন্ন উপায়)
```python
numbers = [1, 2, 3, 4, 5]

# Method 1
reversed1 = numbers[::-1]

# Method 2
reversed2 = list(reversed(numbers))

# Method 3
reversed3 = numbers.copy()
reversed3.reverse()

print(reversed1)  # [5, 4, 3, 2, 1]
print(reversed2)  # [5, 4, 3, 2, 1]
print(reversed3)  # [5, 4, 3, 2, 1]
```

### প্রব্লেম ৫: জোড় এবং বিজোড় আলাদা করুন
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = [num for num in numbers if num % 2 == 0]
odds = [num for num in numbers if num % 2 != 0]

print("জোড়:", evens)    # [2, 4, 6, 8, 10]
print("বিজোড়:", odds)   # [1, 3, 5, 7, 9]
```

## গুরুত্বপূর্ণ পয়েন্টস
- লিস্ট mutable, টাপল immutable
- লিস্ট square brackets [], টাপল parentheses ()
- Negative indexing শেষ থেকে শুরু হয়
- Slicing এ শেষ ইনডেক্স include হয় না
- List comprehension কোড ছোট করে
- টাপল দ্রুত এবং কম মেমরি ব্যবহার করে
- স্থির ডেটার জন্য টাপল, পরিবর্তনশীল ডেটার জন্য লিস্ট
