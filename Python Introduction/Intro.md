# Module 1: Python Introduction (Interview-Level Depth)

Each topic covers three things: **what it is**, **how it works**, and **what problem it solves**, with code examples you can run yourself.

---

## 1. What is Programming? What is a Programming Language?

### What is programming?
A computer only understands **electrical signals (0s and 1s)**. It cannot think on its own. Programming means giving the computer **precise, step-by-step instructions** to perform a task.

**Example:** "If salary is above 50,000, deduct 10% tax."
A human understands this instantly. A computer needs exact logic:

```python
salary = 75000

if salary > 50000:
    tax = salary * 0.10
else:
    tax = 0

print("Tax:", tax)   # Tax: 7500.0
```

**Problem it solves:** Humans can't do repetitive, calculation-heavy, or massive-scale work by hand (millions of bank transactions, billions of search queries). Write a program once, and it runs millions of times without mistakes or fatigue.

**Real example:** Calculating tax for 1 employee by hand takes a minute. For 10 lakh employees, a program does it in seconds:

```python
salaries = [45000, 75000, 120000, 30000]

for s in salaries:
    tax = s * 0.10 if s > 50000 else 0
    print(f"Salary: {s}, Tax: {tax}")
```

### What is a programming language?
A programming language is a **medium of communication between humans and machines**. Machines only understand **machine code** (binary), which is nearly impossible for humans to read or write.

| Level | Example | What it looks like |
|---|---|---|
| Machine language | Binary | `10110000 01100001` |
| Assembly language | x86 ASM | `MOV AL, 61h` |
| High-level language | Python, Java, C | `print("Hello")` |

- **Low-level languages** are close to the hardware: very fast, but hard to write and specific to one type of CPU.
- **High-level languages** are close to human language: easy to read and write, but need a translator (compiler or interpreter) to convert them to machine code.

**Problem it solves:** High-level languages free the programmer from hardware details (memory addresses, CPU registers) so they can focus on **solving the actual business problem**.

---

## 2. What is Python? Who Created It? Where Is It Used?

### What is Python?
Python is a **high-level, interpreted, dynamically typed, general-purpose** programming language. Let's break that down:

**High-level:** Reads almost like English. Memory is managed automatically (garbage collection).

```python
# You never allocate or free memory manually
names = ["Amit", "Priya", "Rahul"]
print(len(names))   # 3
```

**Interpreted:** You don't compile it into a separate `.exe` before running. Just run it.

**Dynamically typed:** You don't declare a variable's type. Python figures it out at runtime, and a variable can even change type:

```python
x = 10          # x is an int
print(type(x))  # <class 'int'>

x = "hello"     # now x is a str
print(type(x))  # <class 'str'>
```

Compare with Java (statically typed):
```java
int x = 10;
x = "hello";   // Compile error! Type mismatch
```

**General-purpose:** Not limited to one domain. Used for web, AI, data, automation, and more.

**Multi-paradigm:** Supports multiple programming styles:

```python
# Procedural style
def area(r):
    return 3.14 * r * r

# Object-oriented style
class Circle:
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14 * self.r * self.r

# Functional style
radii = [1, 2, 3]
areas = list(map(lambda r: 3.14 * r * r, radii))

print(area(2), Circle(2).area(), areas)
```

### Who created Python?
- Created by **Guido van Rossum** at CWI (a research institute in the Netherlands)
- Work began in **December 1989** as a hobby project over the Christmas holidays
- First public release in **1991**
- The name comes from the British comedy show **"Monty Python's Flying Circus,"** not the snake
- Guido was known as the **"BDFL" (Benevolent Dictator For Life)** for many years. He stepped down in 2018, and Python is now governed by a **Steering Council**. New features go through the **PEP (Python Enhancement Proposal)** process. For example, PEP 8 is the official style guide.

### Why was Python created? (The problem)
At the time, programmers had two extremes:
- **C:** Powerful, but even small tasks needed lots of code, manual memory management, and was bug-prone
- **Shell scripts:** Easy, but weak for large programs

Guido wanted a language **as powerful as C but as easy as a shell script**. Python's core philosophy is **"readability counts."** Try this in Python:

```python
import this
```
It prints "The Zen of Python," including lines like *"Beautiful is better than ugly"* and *"Simple is better than complex."*

**Same task in Java vs Python:**

```java
// Java: read a file and print each line
import java.io.*;
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("data.txt"));
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

```python
# Python: same task
with open("data.txt") as f:
    for line in f:
        print(line, end="")
```

### Where is Python used?

| Field | What it does | Popular libraries / tools |
|---|---|---|
| **AI / Machine Learning** | Training models, LLMs, computer vision | PyTorch, TensorFlow, scikit-learn, Hugging Face |
| **Data Science / Analytics** | Cleaning data, analysis, visualization | Pandas, NumPy, Matplotlib, Jupyter |
| **Web Development (backend)** | APIs, server-side of websites | Django, Flask, FastAPI |
| **Automation / Scripting** | Automating repetitive tasks | os, shutil, openpyxl, Selenium |
| **DevOps / Cloud** | Infrastructure scripts, deployment | Ansible, boto3 (AWS) |
| **Web Scraping** | Extracting data from websites | BeautifulSoup, Scrapy |
| **Testing** | Automated tests | pytest |
| **Cybersecurity** | Security tools, network analysis | Scapy |

**Examples of each:**

*Web (a working API in a few lines with FastAPI):*
```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/hello/{name}")
def hello(name: str):
    return {"message": f"Hello, {name}"}
# Run: uvicorn main:app --reload → visit /hello/Rahul
```

*Data analysis (Pandas):*
```python
import pandas as pd

df = pd.DataFrame({
    "city": ["Mumbai", "Delhi", "Mumbai", "Pune"],
    "sales": [500, 300, 700, 200]
})
print(df.groupby("city")["sales"].sum())
# Delhi     300
# Mumbai   1200
# Pune      200
```

*Automation (rename 1000 files in one go):*
```python
import os

for i, filename in enumerate(os.listdir("photos")):
    os.rename(f"photos/{filename}", f"photos/trip_{i}.jpg")
```

*Machine Learning (scikit-learn):*
```python
from sklearn.linear_model import LinearRegression

X = [[1], [2], [3], [4]]   # years of experience
y = [30, 40, 50, 60]       # salary in thousands

model = LinearRegression().fit(X, y)
print(model.predict([[5]]))   # [70.]
```

**Real companies:** Instagram's backend is built on Django; Netflix and Spotify use Python for data pipelines and recommendations; almost the entire AI industry runs on Python.

### Why is Python the king of AI if it's slow?
Python itself is slow, but libraries like NumPy and PyTorch are written internally in **C, C++, and CUDA**. Python acts as an easy "control layer" on top. This is why it's called a **"glue language."**

**Example: pure Python vs NumPy speed:**
```python
import time
import numpy as np

data = list(range(10_000_000))

start = time.time()
total = sum(x * 2 for x in data)        # pure Python loop
print("Python:", time.time() - start)

arr = np.array(data)
start = time.time()
total = (arr * 2).sum()                 # NumPy, runs in C
print("NumPy:", time.time() - start)
```
NumPy is typically **tens of times faster** because the loop runs in compiled C code, not in Python.

### Python's weaknesses (mention these in interviews; it shows maturity)
- **Raw speed** is lower than C, C++, Java, or Go
- **GIL (Global Interpreter Lock):** In CPython, only one thread executes Python bytecode at a time, so threads can't run CPU-heavy work in parallel (a GIL-free build is being introduced experimentally in newer versions)
- **Not common for mobile apps or browser frontends**
- **Runtime type errors:** Because of dynamic typing, some bugs only show up when the code runs:

```python
def add(a, b):
    return a + b

print(add(2, 3))       # 5
print(add("2", 3))     # TypeError at runtime, not before
```
Large projects solve this with **type hints** plus a checker like **mypy**:
```python
def add(a: int, b: int) -> int:
    return a + b
# mypy will flag add("2", 3) BEFORE you run the code
```

---

## 3. Compiler vs Interpreter

Both do the same job: **translate high-level code into something the machine can execute.** The difference is *when* and *how*.

### Compiler
Reads the **entire program at once**, translates it completely, and produces an **executable file**. That file then runs directly.

**Analogy:** Translating an entire English book into Hindi and printing it. Readers no longer need a translator.

**Example (C):**
```c
// hello.c
#include <stdio.h>
int main() {
    printf("Hello\n");
    return 0;
}
```
```bash
gcc hello.c -o hello    # Step 1: compile → creates 'hello' executable
./hello                 # Step 2: run the executable
```

### Interpreter
Reads and executes code **statement by statement** at runtime.

**Analogy:** A live translator translating a speaker sentence by sentence.

**Example (Python):**
```bash
python hello.py         # one step: just run it
```

### Key behavioral difference: when errors appear

```python
# error_demo.py
print("Line 1 runs")
print("Line 2 runs")
print(10 / 0)            # runtime error here
print("Line 4 never runs")
```
Output:
```
Line 1 runs
Line 2 runs
ZeroDivisionError: division by zero
```
Lines 1 and 2 executed before the error. In C, a type error would stop compilation entirely and **nothing** would run.

| Point | Compiler | Interpreter |
|---|---|---|
| Translation | Whole program at once | Statement by statement, at runtime |
| Output | Separate executable (.exe) | No separate executable |
| Execution speed | Faster | Slower |
| When errors appear | All compile errors at once, before running | Stops at the line with the error |
| Debugging | Harder | Easier (instant feedback) |
| Portability | Recompile for each OS/CPU | Runs anywhere the interpreter is installed |
| Examples | C, C++, Go, Rust | Python, JavaScript, Ruby |

### Why is Python interpreted?
1. **Fast development:** Write and run instantly. Ideal for experimentation, data analysis, and AI research.
2. **Dynamic typing:** Types are only known at runtime, so many decisions can't be made ahead of time.
3. **Portability:** The same `.py` file runs on Windows, macOS, and Linux.
4. **Interactive use:** Tools like the REPL and Jupyter are only possible because of this.

### ⚠️ Interview trap: "Is Python purely interpreted?"
**No.** The correct answer:

> "Python is first **compiled into bytecode**, and that bytecode is then **interpreted by the Python Virtual Machine (PVM)**. It's called an interpreted language because there is no separate compile step you run manually and it doesn't compile to machine code, but there is an internal compilation step to bytecode that happens automatically."

**Proof that compilation happens first:**
```python
# syntax_demo.py
print("Will this line run?")
print("Missing bracket"
```
Output:
```
SyntaxError: '(' was never closed
```
Even the **first line didn't run**. If Python were purely line-by-line, line 1 would have printed. The whole file was parsed and compiled first, and compilation failed.

Saying this in an interview immediately shows you understand what happens under the hood.

---

## 4. How Python Code Runs: Source Code → Bytecode → PVM

When you run `python app.py`, this happens internally:

```
 app.py  (source code, human-readable text)
        │
        ▼
 ┌──────────────────────────────────┐
 │  COMPILER (inside CPython)        │
 │  1. Tokenizing  → split into tokens│
 │  2. Parsing     → build AST        │
 │  3. Code gen    → bytecode         │
 └──────────────────────────────────┘
        │
        ▼
 Bytecode  (.pyc files in __pycache__)
        │
        ▼
 ┌──────────────────────────────────┐
 │  PVM (Python Virtual Machine)     │
 │  A loop that executes bytecode    │
 │  instructions one by one          │
 └──────────────────────────────────┘
        │
        ▼
 Actual work on the machine / OS (output)
```

### Step 1: Source code
Your `.py` file, plain text.

### Step 2: Compilation to bytecode

**2a. Tokenizing:** The code is broken into tokens. You can see this yourself:
```python
import tokenize, io

code = "x = 5 + 3"
for tok in tokenize.generate_tokens(io.StringIO(code).readline):
    print(tokenize.tok_name[tok.type], repr(tok.string))
```
Output (simplified):
```
NAME 'x'
OP '='
NUMBER '5'
OP '+'
NUMBER '3'
```

**2b. Parsing into an AST (Abstract Syntax Tree):** The parser checks grammar and builds a tree. **SyntaxErrors are caught here.**
```python
import ast
print(ast.dump(ast.parse("x = 5 + 3"), indent=2))
```
Output (simplified):
```
Module(
  body=[
    Assign(
      targets=[Name(id='x')],
      value=BinOp(left=Constant(value=5), op=Add(), right=Constant(value=3)))])
```

**2c. Bytecode generation:** The AST is turned into **bytecode**, low-level platform-independent instructions.

### Step 3: PVM execution
The PVM is software (in CPython, written in C) that reads each bytecode instruction and executes it. **Runtime errors** like `ZeroDivisionError` and `NameError` happen at this stage.

### See the bytecode yourself
```python
import dis

def add(a, b):
    return a + b

dis.dis(add)
```
Output (exact names vary slightly by Python version):
```
LOAD_FAST     a
LOAD_FAST     b
BINARY_OP     + 
RETURN_VALUE
```
These are the instructions the PVM executes. It works like a stack machine: push `a`, push `b`, add the top two, return the result.

**Fun fact (constant folding):** The compiler optimizes some things in advance:
```python
import dis
dis.dis("x = 60 * 60 * 24")
```
You'll see `LOAD_CONST 86400` because the compiler already calculated `60*60*24` before running.

### `.pyc` files and `__pycache__`

**Example project:**
```
project/
├── main.py
└── utils.py
```
```python
# utils.py
def greet(name):
    return f"Hello, {name}"
```
```python
# main.py
import utils
print(utils.greet("Priya"))
```
After running `python main.py`:
```
project/
├── main.py
├── utils.py
└── __pycache__/
    └── utils.cpython-3XX.pyc    ← bytecode cached here
```

- When you **import** a module, Python saves its bytecode in `__pycache__`.
- Next time, if `utils.py` hasn't changed, Python skips compilation and loads the `.pyc` directly. **Problem solved: faster startup.**
- The main script you run directly (`main.py`) usually doesn't get a `.pyc`; only imported modules do.
- `.pyc` files are tied to the Python version (that's why the filename includes it).

### Why the bytecode design? (Problem solved)
- **Portability:** Bytecode is platform-independent. Only the PVM differs per OS; your code stays the same.
- **Speed:** Executing bytecode is faster than re-parsing raw text every time.
- **Separation of concerns:** Syntax checking happens once; execution is separate.

### Python implementations (bonus; impressive in interviews)
"Python" is a language specification. Different programs implement it:

| Implementation | Written in | Key feature |
|---|---|---|
| **CPython** | C | The official, default one (from python.org) |
| **PyPy** | Python (RPython) | **JIT compiler**; often much faster for long-running code |
| **Jython** | Java | Runs on the JVM, can use Java libraries |
| **IronPython** | C# | Runs on .NET |
| **MicroPython** | C | For microcontrollers and IoT devices |

Check which one you're using:
```python
import platform
print(platform.python_implementation())   # CPython
```

**JIT (Just-In-Time) compilation:** Code that runs repeatedly (hot loops) is compiled into machine code at runtime, so it runs much faster. Java's JVM does this too. Newer CPython versions are adding an experimental JIT as well.

---

## 5. Python 2 vs Python 3

### Background
- **Python 2.0** released in 2000
- **Python 3.0** released in December 2008, **intentionally backward-incompatible**: Python 2 code won't necessarily run on Python 3 without changes
- **Python 2 reached end of life on January 1, 2020.** No more security fixes or updates. All new work uses Python 3.

### Why was Python 3 created? (The problem)
Python 2 had design flaws that couldn't be fixed without breaking compatibility. The biggest one: **confusion between text and bytes.** In Python 2, a normal string was a sequence of bytes, so handling Hindi, emojis, or any non-English text caused many bugs. As the internet went global, this became a major issue.

### Key differences with examples

**1. `print` became a function**
```python
# Python 2
print "Hello"

# Python 3
print("Hello")
print("A", "B", sep="-", end="!\n")   # A-B!  (functions take arguments)
```

**2. Division**
```python
# Python 2
print 7 / 2      # 3  (integer division, surprising!)

# Python 3
print(7 / 2)     # 3.5  (true division)
print(7 // 2)    # 3    (floor division)
print(-7 // 2)   # -4   (floors toward negative infinity, a classic interview question)
```

**3. Strings are Unicode by default**
```python
# Python 3
name = "नमस्ते"
print(len(name))           # counts characters properly
print(name.encode("utf-8"))  # converts to bytes: b'\xe0\xa4\xa8...'

data = b"hello"            # bytes are a separate type
print(type(data))          # <class 'bytes'>
# "hello" + b"hello"       # TypeError: can't mix str and bytes
```
In Python 2, mixing text and bytes silently "worked" until it crashed in production with non-English input.

**4. `input()`**
```python
# Python 2
name = raw_input("Name: ")   # returns a string
x = input("Number: ")        # EVALUATES what you type as code (security risk!)

# Python 3
age = input("Age: ")         # always returns a string
age = int(age)               # convert explicitly
```

**5. `range` is lazy**
```python
# Python 2: range(10**9) builds a list of a billion items → huge memory
# Python 3:
r = range(10**9)
print(r[500])     # 500, instant, almost no memory used
```

**6. Integers have no size limit**
```python
print(2 ** 200)   # a huge exact number; Python 3 has a single unlimited int type
```

**7. Exception syntax**
```python
# Python 2
except ValueError, e:

# Python 3
try:
    int("abc")
except ValueError as e:
    print("Error:", e)
```

**Summary table:**

| Feature | Python 2 | Python 3 |
|---|---|---|
| print | Statement: `print "hi"` | Function: `print("hi")` |
| `5 / 2` | `2` | `2.5` (use `//` for `2`) |
| Strings | Bytes by default; `u"..."` for Unicode | **Unicode** by default; bytes are `b"..."` |
| input | `raw_input()`; `input()` evaluated code | Only `input()`, always a string |
| range | Built a full list; `xrange()` was lazy | `range()` is lazy |
| Integers | `int` and `long` | Only `int`, unlimited size |
| Exceptions | `except E, e:` | `except E as e:` |
| Support | Ended 2020 | Active |

**Industry impact:** The migration took over 10 years because companies had millions of lines of Python 2 code. It's a famous software engineering case study in how costly a backward-incompatible change can be.

---

## 6. REPL / Python Shell vs `.py` File

### What is the REPL?
**R**ead → **E**valuate → **P**rint → **L**oop

1. **Read:** Reads the line you type
2. **Evaluate:** Executes it
3. **Print:** Shows the result
4. **Loop:** Waits for the next input

Type `python` (or `python3`) in a terminal:
```
>>> 2 + 3
5
>>> name = "Rahul"
>>> name.upper()
'RAHUL'
>>> [x * x for x in range(5)]
[0, 1, 4, 9, 16]
>>> help(len)          # built-in documentation
>>> dir(name)          # list all methods available on a string
>>> exit()
```

Notice: in the REPL, the value of an expression is **printed automatically.** In a `.py` file, you must use `print()`.

**Demonstration of this difference:**
```python
# test.py
2 + 3            # nothing is shown
"hello".upper()  # nothing is shown
print(2 + 3)     # 5
```

**Special REPL trick: `_` holds the last result**
```
>>> 10 * 5
50
>>> _ + 1
51
```

### `.py` file
Save code in a file and run it:
```python
# calculator.py
def add(a, b):
    return a + b

if __name__ == "__main__":
    print(add(10, 20))
```
```bash
python calculator.py    # 30
```

| Point | REPL | `.py` file |
|---|---|---|
| Purpose | Quick tests, experiments, learning | Real programs, projects |
| Code saved? | No (lost when session closes) | Yes, permanent |
| Auto-print | Yes | No, need `print()` |
| Multi-line logic | Awkward | Easy |
| Reuse / share / Git | No | Yes |

**Problems solved:**
- **REPL:** Want to know what `"a,b,c".split(",")` returns? Don't write a whole file. Type it and see instantly. Fast feedback means faster learning and debugging.
- **`.py` file:** Save, reuse, test, deploy, and share code with a team.

### Pro tips
**`python -i`** runs the file and then opens a REPL with all variables still available. Great for debugging:
```bash
python -i calculator.py
>>> add(5, 7)
12
```

**IPython** is an enhanced REPL with colors, auto-complete, and magic commands like `%timeit`:
```
In [1]: %timeit sum(range(1000))
```

### What does `if __name__ == "__main__":` do?
When a file is **run directly**, Python sets `__name__` to `"__main__"`. When it's **imported**, `__name__` is the module's name.

```python
# calculator.py
def add(a, b):
    return a + b

print("__name__ is:", __name__)

if __name__ == "__main__":
    print("Running tests:", add(2, 3))
```
```bash
python calculator.py
# __name__ is: __main__
# Running tests: 5
```
```python
# other.py
import calculator
# __name__ is: calculator
# (tests do NOT run)
```
**Problem solved:** You can put test or demo code in a module without it running every time someone imports it.

---

## 7. What is an IDE? (VS Code, PyCharm, Jupyter)

### IDE = Integrated Development Environment
A software that brings all coding tools **together in one place.** You *can* write Python in Notepad, but an IDE multiplies productivity.

### What an IDE gives you (and the problem each solves)

| Feature | What it does | Problem solved |
|---|---|---|
| Syntax highlighting | Colors keywords, strings, comments | Code is easier to read |
| Auto-complete (IntelliSense) | Suggests functions and methods as you type | Less typing, fewer typos |
| Linting | Flags errors and warnings while you type | Bugs caught before running |
| Debugger | Breakpoints, step line by line, inspect variables | No more scattering `print()` everywhere |
| Integrated terminal | Run code inside the IDE | No window switching |
| Git integration | Commit, push, view diffs | Easy version control |
| Refactoring | Rename a variable across the whole project safely | Safe changes in large codebases |
| Virtual environment support | Separate packages per project | No version conflicts |

**Example of what a linter catches before you run:**
```python
def calculate_total(prices):
    total = 0
    for p in prices:
        totl += p        # IDE underlines 'totl' in red: undefined name
    return total
```
Without an IDE, you'd only discover this typo when the code crashes.

**Example of debugging without vs with an IDE:**
```python
def find_average(nums):
    total = sum(nums)
    return total / len(nums)

print(find_average([]))   # ZeroDivisionError
```
- **Without a debugger:** add `print(total)`, `print(len(nums))`, re-run, repeat.
- **With a debugger:** click to set a breakpoint on line 3, run in debug mode, and hover over `nums` to see it's `[]`. You find the cause in seconds.

**Virtual environment example** (why IDEs support them):
```bash
python -m venv venv           # create isolated environment
source venv/bin/activate      # Mac/Linux  (Windows: venv\Scripts\activate)
pip install django==4.2       # installed only for this project
```
Project A can use Django 4.2 and Project B can use Django 5 without conflicts. VS Code and PyCharm detect and switch these automatically.

### The three popular options

**VS Code (Microsoft)**
- Technically a lightweight **code editor** that becomes an IDE through **extensions** (Python extension, Pylance)
- Free, fast, works for every language
- Very widely used in industry
- **Best for:** General development, web plus Python, beginners to professionals

**PyCharm (JetBrains)**
- A **full-featured, Python-specific IDE**
- Powerful refactoring, debugging, Django/Flask support, database tools built in
- Free Community edition; paid Professional edition
- Heavier (uses more RAM)
- **Best for:** Large Python projects, backend development

**Jupyter Notebook / JupyterLab**
- Not a traditional IDE; an **interactive notebook** that runs in the browser
- Code is written in **cells**; each cell runs separately, and output (tables, charts) appears right below it
- Combines code, output, and notes (Markdown) in one document
- **Best for:** Data science, machine learning, analysis, teaching

**Jupyter example:**
```python
# Cell 1
import pandas as pd
df = pd.read_csv("sales.csv")

# Cell 2  (run without reloading the file)
df.head()        # shows a formatted table right below

# Cell 3
df["sales"].plot(kind="bar")   # chart appears inline
```
Loading a large dataset once in Cell 1 and experimenting in other cells saves a lot of time. That's the problem Jupyter solves.

**Jupyter's weakness: hidden state.**
```python
# Cell 1
x = 10
# Cell 2
x = x * 2
print(x)
```
Run Cell 2 three times and you get 20, 40, 80. Someone else running the notebook top to bottom gets 20. Cells run out of order create confusing bugs. That's why Jupyter is not used for production code. Notebook files are also hard to review in Git.

**Google Colab** is a free cloud-hosted Jupyter with GPU access, popular for ML practice.

| | VS Code | PyCharm | Jupyter |
|---|---|---|---|
| Type | Editor + extensions | Full IDE | Notebook |
| Weight | Light | Heavy | Browser-based |
| Best use | Everything | Large Python projects | Data/ML exploration |
| Cost | Free | Free + Paid | Free |

**Real-world workflow:** A data scientist first experiments in Jupyter, then moves the final code into proper `.py` modules in VS Code or PyCharm, which get tested and deployed to production.

---

## 🎯 Interview Questions from This Module

1. **Is Python compiled or interpreted?**
   Both. Source code is compiled to bytecode, then the PVM interprets the bytecode. Proof: a SyntaxError on line 5 prevents line 1 from running.

2. **What is a `.pyc` file and when is it created?**
   Cached compiled bytecode, stored in `__pycache__` for imported modules, used to speed up startup.

3. **What is the PVM?**
   The runtime engine that executes bytecode instructions (a loop written in C in CPython).

4. **Why is Python slow?**
   Interpretation overhead, dynamic typing (type checks on every operation), and the GIL. Solutions: C-backed libraries like NumPy, PyPy, multiprocessing.

5. **What is the GIL?**
   A lock in CPython allowing only one thread to execute Python bytecode at a time. Threads are fine for I/O-bound work (network, files); use multiprocessing for CPU-bound work.

6. **CPython vs PyPy?**
   Official C-based implementation vs a JIT-based implementation that's often faster for long-running code.

7. **Biggest differences between Python 2 and 3?**
   Unicode strings by default, `print()` as a function, `/` performs true division.

8. **What does `-7 // 2` return and why?**
   `-4`, because `//` floors toward negative infinity, not toward zero.

9. **Dynamic vs static typing?**
   Types checked at runtime vs at compile time. Python supports optional type hints checked by tools like mypy.

10. **Why is Python dominant in AI despite being slow?**
    It's a glue language; heavy computation happens in C/C++/CUDA libraries underneath.

11. **Why use `if __name__ == "__main__":`?**
    So code inside it runs only when the file is executed directly, not when imported.

---

One honest note: a top-tier, high-paying role isn't won on Python basics alone. It comes from strong DSA, system design, deep expertise in a domain (AI/ML, large-scale backend, distributed systems), and real projects. But this "why and how" understanding is exactly the foundation that separates an average candidate from a strong one, because senior interviews test reasoning, not syntax.

