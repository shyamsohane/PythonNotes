# Python Tutorial for C# Developers

This guide is written for developers who already know **C#** and want to transition smoothly into **Python**.  
It highlights Python concepts side by side with their C# equivalents.

---

## 1. Getting Started

### Hello World
**C#:**
```csharp
Console.WriteLine("Hello, World!");
```

**Python:**
```python
print("Hello, World!")
```

---

## 2. Variables and Types

- Python is **dynamically typed** (no type declarations).

**C#:**
```csharp
int x = 10;
string name = "Alice";
bool flag = true;
```

**Python:**
```python
x = 10
name = "Alice"
flag = True
```

---

## 3. Conditionals

**C#:**
```csharp
if (x > 5) {
    Console.WriteLine("Greater");
} else {
    Console.WriteLine("Smaller or Equal");
}
```

**Python:**
```python
if x > 5:
    print("Greater")
else:
    print("Smaller or Equal")
```

---

## 4. Loops

**C#:**
```csharp
for (int i = 0; i < 5; i++) {
    Console.WriteLine(i);
}
```

**Python:**
```python
for i in range(5):
    print(i)
```

---

## 5. Functions

**C#:**
```csharp
int Add(int a, int b) {
    return a + b;
}
```

**Python:**
```python
def add(a, b):
    return a + b
```

---

## 6. Classes and Objects

**C#:**
```csharp
public class Person {
    public string Name { get; set; }
    public Person(string name) {
        Name = name;
    }
    public void Greet() {
        Console.WriteLine($"Hello {Name}");
    }
}
```

**Python:**
```python
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hello {self.name}")

p = Person("Alice")
p.greet()
```

---

## 7. Collections

### Lists (like `List<T>` in C#)
```python
nums = [1, 2, 3]
nums.append(4)
print(nums)
```

### Dictionaries (like `Dictionary<TKey, TValue>` in C#)
```python
person = {"name": "Alice", "age": 30}
print(person["name"])
```

---

## 8. Exceptions

**C#:**
```csharp
try {
    int x = 10 / 0;
} catch (DivideByZeroException ex) {
    Console.WriteLine(ex.Message);
}
```

**Python:**
```python
try:
    x = 10 / 0
except ZeroDivisionError as ex:
    print(ex)
```

---

## 9. Async Programming

**C#:**
```csharp
public async Task<int> GetDataAsync() {
    await Task.Delay(1000);
    return 42;
}
```

**Python:**
```python
import asyncio

async def get_data():
    await asyncio.sleep(1)
    return 42
```

---

## 10. Useful Differences

- **Indentation is syntax** in Python (no `{}` braces).
- Python has no `;` line terminator.
- Everything is an **object** in Python (even functions).
- Uses **duck typing** instead of strong typing.

---

## 11. Next Steps

- Explore **virtual environments**: `python -m venv venv`
- Package management with **pip**: `pip install requests`
- Try frameworks:  
  - Web → Flask / FastAPI  
  - Data → Pandas / NumPy  
  - Testing → pytest

---

## Quick Comparison Cheat Sheet

| Concept              | C#                      | Python                   |
|----------------------|--------------------------|--------------------------|
| Variable Declaration | `int x = 5;`            | `x = 5`                  |
| String Interpolation | `$"{name}"`             | `f"{name}"`              |
| Null                 | `null`                  | `None`                   |
| Boolean              | `true/false`            | `True/False`             |
| List                 | `List<int> list`        | `[1, 2, 3]`              |
| Dictionary           | `Dictionary<string,int>`| `{"a": 1, "b": 2}`       |
| Function             | `int Add(int a,int b)`  | `def add(a,b)`           |

---

Happy Coding in Python 🚀


---

## 12. `self` in Python vs `this` in C#

One of the most common questions C# developers have when moving to Python is:  
**"Why do I need to write `self` in every method?"**

### C#
In C#, the current object is referenced automatically with `this`:
```csharp
public class Person {
    public string Name { get; set; }
    public void Greet() {
        Console.WriteLine($"Hello {this.Name}");
    }
}
```

### Python
In Python, you must explicitly declare `self` as the first parameter of instance methods:
```python
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hello {self.name}")
```

### Why the difference?
- In C#, the compiler automatically inserts `this` for instance members.  
- In Python, methods are just functions inside a class. The first argument is **the instance itself**, by convention called `self`.

So:
```python
p.greet()
```
is really shorthand for:
```python
Person.greet(p)
```

This design makes it clear that methods are just functions with the instance passed in.

---
# Parallel Programming in Python (for C# Developers)

This guide explains how to perform **parallel and concurrent programming in Python**, comparing it to familiar **C# concepts** like `Task`, `async/await`, and `Parallel.ForEach`.

---

## 1. Concurrency vs Parallelism

- **Concurrency** → Multiple tasks make progress at the same time (e.g., `async/await` in C#).
- **Parallelism** → Multiple tasks actually run simultaneously on multiple CPU cores.

Python offers both through libraries:
- `threading` → concurrency (I/O-bound tasks).
- `multiprocessing` → parallelism (CPU-bound tasks).
- `asyncio` → async/await style (like C# async).

---

## 2. Threading (for I/O-bound tasks)

**C#:**
```csharp
var t1 = new Thread(() => DownloadFile("a.txt"));
var t2 = new Thread(() => DownloadFile("b.txt"));
t1.Start();
t2.Start();
```

**Python:**
```python
import threading

def download_file(name):
    print(f"Downloading {name}")

t1 = threading.Thread(target=download_file, args=("a.txt",))
t2 = threading.Thread(target=download_file, args=("b.txt",))

t1.start()
t2.start()
```

⚠️ Due to the **Global Interpreter Lock (GIL)**, Python threads do not run CPU tasks truly in parallel.  
They are best for I/O tasks (file, network).

---

## 3. Multiprocessing (for CPU-bound tasks)

**C#:**
```csharp
Parallel.For(0, 5, i => {
    Console.WriteLine(i);
});
```

**Python:**
```python
from multiprocessing import Process

def worker(n):
    print(f"Processing {n}")

processes = []
for i in range(5):
    p = Process(target=worker, args=(i,))
    processes.append(p)
    p.start()

for p in processes:
    p.join()
```

Here each process has its own Python interpreter, bypassing the GIL → true parallelism.

---

## 4. AsyncIO (async/await style)

**C#:**
```csharp
public async Task RunAsync() {
    await Task.Delay(1000);
    Console.WriteLine("Done");
}
```

**Python:**
```python
import asyncio

async def run_async():
    await asyncio.sleep(1)
    print("Done")

asyncio.run(run_async())
```

AsyncIO is **single-threaded** but handles thousands of tasks concurrently (great for network servers, APIs).

---

## 5. ThreadPoolExecutor (high-level parallelism)

Python’s `concurrent.futures` provides an easy way (similar to `Task.Run` in C#).

**C#:**
```csharp
var tasks = Enumerable.Range(0, 5)
    .Select(i => Task.Run(() => DoWork(i)));
await Task.WhenAll(tasks);
```

**Python:**
```python
from concurrent.futures import ThreadPoolExecutor

def work(n):
    print(f"Working {n}")

with ThreadPoolExecutor() as executor:
    futures = [executor.submit(work, i) for i in range(5)]
    for f in futures:
        f.result()
```

---

## 6. Multiprocessing Pool

For distributing tasks across processes easily:

```python
from multiprocessing import Pool

def square(n):
    return n * n

with Pool(4) as pool:
    results = pool.map(square, [1, 2, 3, 4])
    print(results)
```

Output:
```
[1, 4, 9, 16]
```

---

## 7. Summary: Which to Use?

| Scenario               | C# Equivalent           | Python Approach              |
|-------------------------|-------------------------|------------------------------|
| I/O-bound (web, files) | `Task`, `async/await`   | `threading` / `asyncio`      |
| CPU-bound (math, AI)   | `Parallel.For`, TPL     | `multiprocessing`, `Pool`    |
| Mixed workloads        | Combine Tasks & Threads | Mix `asyncio` + multiprocessing |

---

## 8. Next Steps

- Explore libraries:  
  - `joblib` (for data science parallelism)  
  - `ray` (distributed computing)  
  - `dask` (big data parallelism)  
- Benchmark before choosing threading vs multiprocessing.

---

⚡ Key takeaway:  
- Use **`asyncio`/`threading`** for I/O tasks.  
- Use **`multiprocessing`** for CPU-heavy work.  

