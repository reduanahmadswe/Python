# Lecture 7: File Input/Output in Python

## ফাইল কি? (What is a File?)

ফাইল হলো ডেটা সংরক্ষণের একটি স্থান যা হার্ড ডিস্কে permanent ভাবে থাকে। Python দিয়ে text files এবং binary files নিয়ে কাজ করা যায়।

### ফাইল টাইপস:
- **Text files**: .txt, .csv, .json, .html ইত্যাদি
- **Binary files**: .jpg, .png, .pdf, .exe ইত্যাদি

## File Operations (ফাইল অপারেশন)

### ১. File খোলা (Opening a File)
```python
# Syntax
file = open("filename.txt", "mode")
```

### File Modes (ফাইল মোড):

| Mode | বর্ণনা | ফাইল না থাকলে |
|------|--------|---------------|
| 'r' | Read (পড়া) - ডিফল্ট | Error দেবে |
| 'w' | Write (লেখা) - overwrite করবে | তৈরি করবে |
| 'a' | Append (শেষে যোগ) | তৈরি করবে |
| 'x' | Create (নতুন তৈরি) | Error দেবে যদি থাকে |
| 'r+' | Read + Write | Error দেবে |
| 'w+' | Write + Read | তৈরি করবে |
| 'a+' | Append + Read | তৈরি করবে |

```python
# Read mode
file = open("data.txt", "r")

# Write mode
file = open("output.txt", "w")

# Append mode
file = open("log.txt", "a")
```

## Reading Files (ফাইল পড়া)

### read() - পুরো ফাইল পড়া
```python
# Method 1: Manual close
file = open("sample.txt", "r")
content = file.read()
print(content)
file.close()

# Method 2: with statement (সবচেয়ে ভালো)
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)
# Automatically close হবে
```

### read(n) - নির্দিষ্ট characters পড়া
```python
with open("sample.txt", "r") as file:
    # প্রথম 10 characters
    content = file.read(10)
    print(content)
    
    # পরের 5 characters
    more = file.read(5)
    print(more)
```

### readline() - একটা লাইন পড়া
```python
with open("sample.txt", "r") as file:
    line1 = file.readline()
    print("Line 1:", line1)
    
    line2 = file.readline()
    print("Line 2:", line2)
```

### readlines() - সব লাইন list হিসেবে
```python
with open("sample.txt", "r") as file:
    lines = file.readlines()
    print(lines)
    
    # প্রতিটা লাইন iterate করা
    for line in lines:
        print(line.strip())  # strip() newline remove করে
```

### Loop দিয়ে পড়া (Memory Efficient)
```python
with open("sample.txt", "r") as file:
    for line in file:
        print(line.strip())
```

## Writing Files (ফাইলে লেখা)

### write() - লেখা
```python
# Write mode - পুরানো content মুছে যাবে
with open("output.txt", "w") as file:
    file.write("হ্যালো, Python!\n")
    file.write("এটি দ্বিতীয় লাইন।\n")

# Multiple lines
lines = ["প্রথম লাইন\n", "দ্বিতীয় লাইন\n", "তৃতীয় লাইন\n"]
with open("output.txt", "w") as file:
    file.writelines(lines)
```

### append() - শেষে যোগ করা
```python
# Append mode - নতুন content শেষে যোগ হবে
with open("log.txt", "a") as file:
    file.write("নতুন লাইন\n")
    file.write("আরেকটি লাইন\n")
```

### Example: User Input থেকে লেখা
```python
with open("notes.txt", "w") as file:
    while True:
        line = input("লিখুন (বা 'quit'): ")
        if line.lower() == 'quit':
            break
        file.write(line + "\n")
```

## File Positions (ফাইল পজিশন)

### tell() - বর্তমান position
```python
with open("sample.txt", "r") as file:
    print(file.tell())  # 0 (শুরুতে)
    
    file.read(10)
    print(file.tell())  # 10
```

### seek() - নির্দিষ্ট position এ যাওয়া
```python
with open("sample.txt", "r") as file:
    # শুরু থেকে 5 character এগিয়ে
    file.seek(5)
    content = file.read()
    print(content)
    
    # আবার শুরুতে যাওয়া
    file.seek(0)
    first_line = file.readline()
    print(first_line)
```

## File এবং Directory Operations

### os module
```python
import os

# Check if file exists
if os.path.exists("data.txt"):
    print("ফাইল আছে")
else:
    print("ফাইল নেই")

# Get file size
size = os.path.getsize("data.txt")
print(f"Size: {size} bytes")

# Rename file
os.rename("old.txt", "new.txt")

# Delete file
if os.path.exists("temp.txt"):
    os.remove("temp.txt")
    print("ফাইল মুছে গেছে")

# Get current directory
print(os.getcwd())

# Create directory
if not os.path.exists("my_folder"):
    os.mkdir("my_folder")

# Remove directory
os.rmdir("my_folder")

# List files in directory
files = os.listdir(".")
for file in files:
    print(file)
```

### Path operations
```python
import os

# Join paths
path = os.path.join("folder", "subfolder", "file.txt")
print(path)  # folder/subfolder/file.txt

# Get absolute path
abs_path = os.path.abspath("data.txt")
print(abs_path)

# Get directory name
dirname = os.path.dirname("/home/user/file.txt")
print(dirname)  # /home/user

# Get filename
basename = os.path.basename("/home/user/file.txt")
print(basename)  # file.txt

# Split extension
name, ext = os.path.splitext("document.pdf")
print(name, ext)  # document .pdf
```

## Working with CSV Files

### Writing CSV
```python
import csv

# Write to CSV
data = [
    ["নাম", "বয়স", "শহর"],
    ["রহিম", 25, "ঢাকা"],
    ["করিম", 30, "চট্টগ্রাম"],
    ["জামাল", 28, "সিলেট"]
]

with open("students.csv", "w", newline='', encoding='utf-8') as file:
    writer = csv.writer(file)
    writer.writerows(data)

# Alternative: Write row by row
with open("students.csv", "w", newline='', encoding='utf-8') as file:
    writer = csv.writer(file)
    writer.writerow(["নাম", "বয়স", "শহর"])
    writer.writerow(["রহিম", 25, "ঢাকা"])
    writer.writerow(["করিম", 30, "চট্টগ্রাম"])
```

### Reading CSV
```python
import csv

# Read CSV
with open("students.csv", "r", encoding='utf-8') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Skip header
with open("students.csv", "r", encoding='utf-8') as file:
    reader = csv.reader(file)
    next(reader)  # Skip first line
    for row in reader:
        print(f"নাম: {row[0]}, বয়স: {row[1]}, শহর: {row[2]}")
```

### CSV DictReader এবং DictWriter
```python
import csv

# Write using DictWriter
data = [
    {"name": "রহিম", "age": 25, "city": "ঢাকা"},
    {"name": "করিম", "age": 30, "city": "চট্টগ্রাম"},
]

with open("students.csv", "w", newline='', encoding='utf-8') as file:
    fieldnames = ["name", "age", "city"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    
    writer.writeheader()
    writer.writerows(data)

# Read using DictReader
with open("students.csv", "r", encoding='utf-8') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"নাম: {row['name']}, বয়স: {row['age']}, শহর: {row['city']}")
```

## Working with JSON Files

### Writing JSON
```python
import json

# Dictionary to JSON
data = {
    "name": "রহিম",
    "age": 25,
    "city": "ঢাকা",
    "marks": [85, 90, 78]
}

# Write to file
with open("data.json", "w", encoding='utf-8') as file:
    json.dump(data, file, ensure_ascii=False, indent=4)

# Convert to JSON string
json_string = json.dumps(data, ensure_ascii=False, indent=2)
print(json_string)
```

### Reading JSON
```python
import json

# Read from file
with open("data.json", "r", encoding='utf-8') as file:
    data = json.load(file)
    print(data)
    print(f"নাম: {data['name']}")
    print(f"বয়স: {data['age']}")

# Parse JSON string
json_string = '{"name": "করিম", "age": 30}'
data = json.loads(json_string)
print(data)
```

## Exception Handling with Files

### try-except
```python
# File not found handling
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
        print(content)
except FileNotFoundError:
    print("ফাইল পাওয়া যায়নি!")

# Multiple exceptions
try:
    with open("data.txt", "r") as file:
        number = int(file.read())
        result = 10 / number
except FileNotFoundError:
    print("ফাইল পাওয়া যায়নি!")
except ValueError:
    print("সংখ্যা নয়!")
except ZeroDivisionError:
    print("শূন্য দিয়ে ভাগ করা যায় না!")
except Exception as e:
    print(f"Error: {e}")
finally:
    print("Cleanup কাজ")
```

## প্র্যাক্টিস প্রব্লেম (Practice Problems)

### প্রব্লেম ১: Word Count
```python
def word_count(filename):
    try:
        with open(filename, "r", encoding='utf-8') as file:
            content = file.read()
            words = content.split()
            lines = content.split('\n')
            chars = len(content)
            
            print(f"শব্দ: {len(words)}")
            print(f"লাইন: {len(lines)}")
            print(f"ক্যারেক্টার: {chars}")
    except FileNotFoundError:
        print("ফাইল পাওয়া যায়নি!")

word_count("sample.txt")
```

### প্রব্লেম ২: Copy File
```python
def copy_file(source, destination):
    try:
        with open(source, "r", encoding='utf-8') as src:
            content = src.read()
        
        with open(destination, "w", encoding='utf-8') as dst:
            dst.write(content)
        
        print("ফাইল কপি সফল!")
    except FileNotFoundError:
        print("Source ফাইল পাওয়া যায়নি!")
    except Exception as e:
        print(f"Error: {e}")

copy_file("original.txt", "backup.txt")
```

### প্রব্লেম ৩: Search in File
```python
def search_in_file(filename, search_text):
    try:
        with open(filename, "r", encoding='utf-8') as file:
            line_number = 0
            found = False
            
            for line in file:
                line_number += 1
                if search_text in line:
                    print(f"Line {line_number}: {line.strip()}")
                    found = True
            
            if not found:
                print("পাওয়া যায়নি!")
    except FileNotFoundError:
        print("ফাইল পাওয়া যায়নি!")

search_in_file("data.txt", "Python")
```

### প্রব্লেম ৪: Student Management System
```python
import json

class StudentManager:
    def __init__(self, filename="students.json"):
        self.filename = filename
        self.students = self.load_students()
    
    def load_students(self):
        try:
            with open(self.filename, "r", encoding='utf-8') as file:
                return json.load(file)
        except FileNotFoundError:
            return []
    
    def save_students(self):
        with open(self.filename, "w", encoding='utf-8') as file:
            json.dump(self.students, file, ensure_ascii=False, indent=4)
    
    def add_student(self, name, age, marks):
        student = {
            "name": name,
            "age": age,
            "marks": marks
        }
        self.students.append(student)
        self.save_students()
        print("ছাত্র যোগ হয়েছে!")
    
    def display_students(self):
        if not self.students:
            print("কোন ছাত্র নেই!")
            return
        
        for i, student in enumerate(self.students, 1):
            print(f"{i}. নাম: {student['name']}, বয়স: {student['age']}, নম্বর: {student['marks']}")

# Usage
manager = StudentManager()
manager.add_student("রহিম", 20, 85)
manager.add_student("করিম", 22, 92)
manager.display_students()
```

### প্রব্লেম ৫: Log File Generator
```python
from datetime import datetime

def write_log(message, log_file="app.log"):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] {message}\n"
    
    with open(log_file, "a", encoding='utf-8') as file:
        file.write(log_entry)

# Usage
write_log("Application started")
write_log("User logged in")
write_log("Error: File not found")
write_log("Application closed")
```

### প্রব্লেম ৬: CSV to Dictionary
```python
import csv

def csv_to_dict(filename):
    result = []
    
    with open(filename, "r", encoding='utf-8') as file:
        reader = csv.DictReader(file)
        for row in reader:
            result.append(dict(row))
    
    return result

# Usage
students = csv_to_dict("students.csv")
for student in students:
    print(student)
```

### প্রব্লেম ৭: Merge Multiple Text Files
```python
def merge_files(file_list, output_file):
    with open(output_file, "w", encoding='utf-8') as outfile:
        for filename in file_list:
            try:
                with open(filename, "r", encoding='utf-8') as infile:
                    outfile.write(f"\n--- {filename} ---\n")
                    outfile.write(infile.read())
                    outfile.write("\n")
            except FileNotFoundError:
                print(f"{filename} পাওয়া যায়নি!")

# Usage
files = ["file1.txt", "file2.txt", "file3.txt"]
merge_files(files, "combined.txt")
```

## Best Practices (ভালো অভ্যাস)

1. **সবসময় with statement ব্যবহার করুন**
```python
# ভালো
with open("file.txt", "r") as file:
    content = file.read()

# খারাপ
file = open("file.txt", "r")
content = file.read()
file.close()  # ভুলে যেতে পারেন
```

2. **Exception handling করুন**
```python
try:
    with open("file.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("ফাইল পাওয়া যায়নি!")
```

3. **Encoding specify করুন**
```python
with open("file.txt", "r", encoding='utf-8') as file:
    content = file.read()
```

4. **Large files এর জন্য line by line পড়ুন**
```python
# Memory efficient
with open("large_file.txt", "r") as file:
    for line in file:
        process(line)
```

## গুরুত্বপূর্ণ পয়েন্টস
- `with` statement automatic close করে
- 'r' mode file না থাকলে error দেয়
- 'w' mode পুরানো content মুছে দেয়
- 'a' mode শেষে যোগ করে
- `readline()` একটা লাইন, `readlines()` সব লাইন
- CSV এবং JSON নিয়ে কাজ করতে module import করতে হয়
- Exception handling করা গুরুত্বপূর্ণ
- UTF-8 encoding বাংলা লেখার জন্য প্রয়োজন
- Large files এর জন্য memory efficient method ব্যবহার করুন
