# 🐍 Python Cheat Sheet (GenAI + ML Focus)

[⬅ Back to README](../../README.md)

---

# ⚡ Basics

---

## Variables & Types

```python
x = 10
name = "AI"
is_valid = True
```

---

## Lists

```python
arr = [1, 2, 3]

arr.append(4)
arr.pop()

# List comprehension
squares = [x*x for x in arr]
```

---

## Dictionaries

```python
data = {"name": "Sandeep", "age": 30}

data["name"]
data.get("age")

for k, v in data.items():
    print(k, v)
```

---

## Sets

```python
s = {1, 2, 3}
s.add(4)
```

---

# 🔁 Control Flow

---

## If-Else

```python
if x > 10:
    print("High")
elif x == 10:
    print("Equal")
else:
    print("Low")
```

---

## Loops

```python
for i in range(5):
    print(i)

while x > 0:
    x -= 1
```

---

# ⚙️ Functions

```python
def add(a, b):
    return a + b

# Lambda
square = lambda x: x*x
```

---

# 🧠 OOP (Important)

---

## Class

```python
class Model:
    def __init__(self, name):
        self.name = name

    def predict(self, x):
        return x * 2

m = Model("test")
m.predict(5)
```

---

## Inheritance

```python
class Base:
    def greet(self):
        print("Hello")

class Child(Base):
    pass
```

---

# 📦 File Handling

```python
with open("file.txt", "r") as f:
    data = f.read()
```

---

# 📊 Data Handling (VERY IMPORTANT)

---

## NumPy

```python
import numpy as np

arr = np.array([1, 2, 3])
arr.mean()
```

---

## Pandas

```python
import pandas as pd

df = pd.read_csv("data.csv")

df.head()
df["column"].mean()
```

---

# 🔥 Error Handling

```python
try:
    x = int("abc")
except Exception as e:
    print(e)
```

---

# ⚡ Async Programming (VERY IMPORTANT)

---

## Async Example

```python
import asyncio

async def task():
    return "done"

async def main():
    result = await task()
    print(result)

asyncio.run(main())
```

---

## Parallel Calls

```python
async def fetch():
    return "data"

results = await asyncio.gather(fetch(), fetch())
```

---

# 🌐 API Calls

```python
import requests

response = requests.get("https://api.com")
data = response.json()
```

---

# 🧠 JSON Handling

```python
import json

data = json.loads('{"a":1}')
json_str = json.dumps(data)
```

---

# 🧵 Generators (IMPORTANT)

```python
def gen():
    for i in range(3):
        yield i

for x in gen():
    print(x)
```

---

# ⚡ Decorators

```python
def log(func):
    def wrapper(*args, **kwargs):
        print("Calling function")
        return func(*args, **kwargs)
    return wrapper

@log
def hello():
    print("Hello")
```

---

# 🧠 Useful Built-ins

```python
len(arr)
sum(arr)
max(arr)
min(arr)
```

---

# 📚 ML / GenAI Utilities

---

## Token Counting (example)

```python
len(text.split())
```

---

## Simple Caching

```python
cache = {}

def get_data(x):
    if x in cache:
        return cache[x]

    result = x * 2
    cache[x] = result
    return result
```

---

## Timing Code

```python
import time

start = time.time()

# code

print(time.time() - start)
```

---

# 🚨 Must-Know for Interviews

- List vs Tuple  
- Deep copy vs shallow copy  
- Mutable vs Immutable  
- GIL (Global Interpreter Lock)  
- Async vs threading  

---

# 💡 Key Insight

> Python is not just syntax — mastering async, data handling, and structure is critical for building scalable GenAI systems.
