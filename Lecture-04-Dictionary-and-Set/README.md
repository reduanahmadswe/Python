# Lecture 4: Dictionary & Set in Python

## ডিকশনারি (Dictionary)

ডিকশনারি হলো key-value pair এর একটি collection। এটি **mutable** এবং **unordered** (Python 3.7+ এ insertion order maintain করে)।

### ডিকশনারি তৈরি করা
```python
# খালি ডিকশনারি
empty_dict = {}
empty_dict2 = dict()

# Basic dictionary
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}

# বিভিন্ন টাইপের value
person = {
    "name": "করিম",
    "age": 25,
    "marks": [85, 90, 78],
    "is_student": True,
    "address": {
        "city": "চট্টগ্রাম",
        "area": "পাহাড়তলী"
    }
}

print(student)
print(len(student))  # 3 (key-value পেয়ারের সংখ্যা)
```

### ডিকশনারি এক্সেস করা (Accessing Dictionary)
```python
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}

# Square bracket দিয়ে
print(student["name"])  # রহিম
print(student["age"])   # 20

# get() method (নিরাপদ)
print(student.get("city"))        # ঢাকা
print(student.get("phone"))       # None (key না থাকলে)
print(student.get("phone", "N/A")) # N/A (default value)

# Error দেবে যদি key না থাকে
# print(student["phone"])  # KeyError!
```

### ডিকশনারি মডিফাই করা
```python
student = {
    "name": "রহিম",
    "age": 20
}

# নতুন key-value যোগ
student["city"] = "ঢাকা"
student["marks"] = 85

# মান পরিবর্তন
student["age"] = 21

# মুছে ফেলা
del student["marks"]

print(student)
```

### ডিকশনারি মেথডস (Dictionary Methods)

#### ১. keys(), values(), items()
```python
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}

# সব keys
keys = student.keys()
print(keys)  # dict_keys(['name', 'age', 'city'])
print(list(keys))  # ['name', 'age', 'city']

# সব values
values = student.values()
print(values)  # dict_values(['রহিম', 20, 'ঢাকা'])
print(list(values))  # ['রহিম', 20, 'ঢাকা']

# সব key-value pairs
items = student.items()
print(items)  # dict_items([('name', 'রহিম'), ('age', 20), ('city', 'ঢাকা')])
print(list(items))  # [('name', 'রহিম'), ('age', 20), ('city', 'ঢাকা')]
```

#### ২. update()
```python
student = {
    "name": "রহিম",
    "age": 20
}

# নতুন key-value যোগ বা existing update
student.update({"city": "ঢাকা", "marks": 85})
print(student)
# {'name': 'রহিম', 'age': 20, 'city': 'ঢাকা', 'marks': 85}

# আরেকটা ডিকশনারি দিয়ে update
extra = {"phone": "01712345678", "email": "rahim@mail.com"}
student.update(extra)
print(student)
```

#### ৩. pop() এবং popitem()
```python
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}

# pop() - নির্দিষ্ট key মুছবে এবং value রিটার্ন করবে
age = student.pop("age")
print(age)      # 20
print(student)  # {'name': 'রহিম', 'city': 'ঢাকা'}

# popitem() - শেষ item মুছবে (Python 3.7+)
last_item = student.popitem()
print(last_item)  # ('city', 'ঢাকা')
print(student)    # {'name': 'রহিম'}
```

#### ৪. clear() এবং copy()
```python
student = {
    "name": "রহিম",
    "age": 20
}

# copy() - ডিকশনারি কপি
student_copy = student.copy()
print(student_copy)

# clear() - সব মুছে দেবে
student.clear()
print(student)  # {}
```

#### ৫. setdefault() এবং fromkeys()
```python
student = {
    "name": "রহিম"
}

# setdefault() - key থাকলে value দেবে, না থাকলে যোগ করবে
age = student.setdefault("age", 20)
print(age)      # 20
print(student)  # {'name': 'রহিম', 'age': 20}

# fromkeys() - keys থেকে ডিকশনারি তৈরি
keys = ["name", "age", "city"]
new_dict = dict.fromkeys(keys, "Unknown")
print(new_dict)
# {'name': 'Unknown', 'age': 'Unknown', 'city': 'Unknown'}
```

### ডিকশনারি লুপিং (Looping Through Dictionary)
```python
student = {
    "name": "রহিম",
    "age": 20,
    "city": "ঢাকা"
}

# শুধু keys
for key in student:
    print(key)

# keys এবং values
for key in student:
    print(f"{key}: {student[key]}")

# items() ব্যবহার করে (সবচেয়ে ভালো)
for key, value in student.items():
    print(f"{key}: {value}")

# শুধু values
for value in student.values():
    print(value)
```

### Nested Dictionary (ভিতরে ডিকশনারি)
```python
students = {
    "student1": {
        "name": "রহিম",
        "age": 20,
        "marks": 85
    },
    "student2": {
        "name": "করিম",
        "age": 22,
        "marks": 90
    }
}

# Access nested values
print(students["student1"]["name"])  # রহিম
print(students["student2"]["marks"]) # 90

# Loop through nested dictionary
for student_id, info in students.items():
    print(f"\n{student_id}:")
    for key, value in info.items():
        print(f"  {key}: {value}")
```

### Dictionary Comprehension
```python
# Basic dictionary comprehension
squares = {x: x*x for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With condition
evens = {x: x*x for x in range(1, 11) if x % 2 == 0}
print(evens)  # {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# From two lists
keys = ["name", "age", "city"]
values = ["রহিম", 20, "ঢাকা"]
person = {k: v for k, v in zip(keys, values)}
print(person)  # {'name': 'রহিম', 'age': 20, 'city': 'ঢাকা'}
```

## সেট (Set)

সেট হলো unique elements এর একটি collection। এটি **mutable** কিন্তু **unordered** এবং **unindexed**। ডুপ্লিকেট থাকে না।

### সেট তৈরি করা
```python
# খালি সেট (dict() নয়!)
empty_set = set()

# Basic set
numbers = {1, 2, 3, 4, 5}
fruits = {"আম", "কলা", "আপেল"}

# List থেকে set (duplicates remove)
numbers_list = [1, 2, 2, 3, 3, 3, 4, 5]
numbers_set = set(numbers_list)
print(numbers_set)  # {1, 2, 3, 4, 5}

# String থেকে set
letters = set("hello")
print(letters)  # {'h', 'e', 'l', 'o'}
```

### সেট মেথডস (Set Methods)

#### ১. Adding Elements
```python
fruits = {"আম", "কলা"}

# add() - একটা element যোগ
fruits.add("আপেল")
print(fruits)  # {'আম', 'কলা', 'আপেল'}

# update() - একাধিক যোগ
fruits.update(["আঙুর", "লিচু"])
print(fruits)  # {'আম', 'কলা', 'আপেল', 'আঙুর', 'লিচু'}
```

#### ২. Removing Elements
```python
numbers = {1, 2, 3, 4, 5}

# remove() - element মুছবে (না থাকলে error)
numbers.remove(3)
print(numbers)  # {1, 2, 4, 5}

# discard() - element মুছবে (না থাকলে error দেবে না)
numbers.discard(10)  # কোন error নেই
print(numbers)

# pop() - random element মুছবে
removed = numbers.pop()
print(f"Removed: {removed}")
print(numbers)

# clear() - সব মুছে দেবে
numbers.clear()
print(numbers)  # set()
```

#### ৩. Set Operations (গাণিতিক অপারেশন)
```python
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}

# Union (মিলন) - দুইটার সব element
print(A | B)  # {1, 2, 3, 4, 5, 6, 7, 8}
print(A.union(B))

# Intersection (ছেদ) - common elements
print(A & B)  # {4, 5}
print(A.intersection(B))

# Difference (বিয়োগ) - A তে আছে কিন্তু B তে নেই
print(A - B)  # {1, 2, 3}
print(A.difference(B))

# Symmetric Difference - common বাদে বাকি
print(A ^ B)  # {1, 2, 3, 6, 7, 8}
print(A.symmetric_difference(B))
```

#### ৪. Subset এবং Superset
```python
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

# issubset() - A, B এর subset কিনা
print(A.issubset(B))  # True
print(A <= B)         # True

# issuperset() - B, A এর superset কিনা
print(B.issuperset(A))  # True
print(B >= A)           # True

# isdisjoint() - কোন common element নেই কিনা
C = {6, 7, 8}
print(A.isdisjoint(C))  # True
```

### Frozen Set (অপরিবর্তনীয় সেট)
```python
# Immutable set
frozen = frozenset([1, 2, 3, 4, 5])
print(frozen)

# নিচের operations কাজ করবে না
# frozen.add(6)     # Error!
# frozen.remove(1)  # Error!

# কিন্তু read operations কাজ করবে
print(len(frozen))
print(3 in frozen)
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: শব্দের ফ্রিকোয়েন্সি গণনা
```python
text = "python is awesome and python is easy"
words = text.split()

# Dictionary দিয়ে count
word_count = {}
for word in words:
    word_count[word] = word_count.get(word, 0) + 1

print(word_count)
# {'python': 2, 'is': 2, 'awesome': 1, 'and': 1, 'easy': 1}
```

### প্রব্লেম ২: দুইটা dictionary মার্জ করুন
```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

# Method 1: update()
merged = dict1.copy()
merged.update(dict2)
print(merged)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Method 2: ** operator (Python 3.5+)
merged = {**dict1, **dict2}
print(merged)

# Method 3: | operator (Python 3.9+)
merged = dict1 | dict2
print(merged)
```

### প্রব্লেম ৩: ডুপ্লিকেট খুঁজুন
```python
numbers = [1, 2, 3, 2, 4, 5, 3, 6]

# Set দিয়ে duplicates খুঁজুন
unique = set()
duplicates = set()

for num in numbers:
    if num in unique:
        duplicates.add(num)
    else:
        unique.add(num)

print("Duplicates:", duplicates)  # {2, 3}
```

### প্রব্লেম ৪: Student Grades Management
```python
students = {
    "রহিম": {"math": 85, "english": 90, "science": 78},
    "করিম": {"math": 92, "english": 88, "science": 95},
    "জামাল": {"math": 78, "english": 85, "science": 80}
}

# প্রতিটা ছাত্রের গড় নম্বর
for name, marks in students.items():
    total = sum(marks.values())
    average = total / len(marks)
    print(f"{name}: {average:.2f}")
```

### প্রব্লেম ৫: Common এবং Unique Elements
```python
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]

set1 = set(list1)
set2 = set(list2)

# Common elements
common = set1 & set2
print("Common:", common)  # {4, 5}

# Unique to list1
unique_to_1 = set1 - set2
print("Unique to list1:", unique_to_1)  # {1, 2, 3}

# Unique to list2
unique_to_2 = set2 - set1
print("Unique to list2:", unique_to_2)  # {6, 7, 8}

# All unique elements
all_unique = set1 ^ set2
print("All unique:", all_unique)  # {1, 2, 3, 6, 7, 8}
```

## গুরুত্বপূর্ণ পয়েন্টস

### Dictionary
- Key-value pair এ কাজ করে
- Keys অবশ্যই unique এবং immutable হতে হবে
- Values যেকোনো টাইপের হতে পারে
- get() method ব্যবহার করা নিরাপদ
- Dictionary comprehension কোড ছোট করে

### Set
- শুধুমাত্র unique elements
- Unordered এবং unindexed
- গাণিতিক অপারেশনের জন্য খুব useful
- Duplicates remove করতে দ্রুত
- Frozen set immutable
