
## Pytest
pytest is incredibly smart about finding and running your tests. It relies on a concept called Test Discovery, 
which follows standard naming conventions to automatically map out your codebase without you having to explicitly register each test.  

Here is exactly how pytest looks at your code, figures out what to test, and decides whether to give your build a "go-ahead."

#### 1. How pytest Automatically Finds Your Tests (Test Discovery)
When you type pytest in your terminal, it scans your current directory and subdirectories looking for specific patterns. If a file, class, or function doesn't match these naming conventions, pytest will simply ignore it.
###### The Naming Rules:
- `Files`: It looks for files named test_*.py or *_test.py.
- `Classes`: Inside those files, it looks for classes named Test (with a capital T, e.g., class TestBillingSystem:). These classes should not have an __init__ method.
- `Functions / Methods`: Inside those files or classes, it looks for functions or methods prefixed with test_* (e.g., def test_payment_success():).

```
my_project/
│
├── src/
│   └── calculator.py       <-- Your actual application code
└── tests/
    └── test_calculator.py  <-- pytest automatically finds this file
```

**test_calculator.py**
```
# pytest will automatically run this because it starts with "test_"
def test_addition():
    assert 1 + 1 == 2

# pytest will IGNORE this because it doesn't match the naming convention
def helper_function():
    return 42
```
#### 2. How pytest Knows What to Test (The Assert Statement)
pytest performs Abstract Syntax Tree (AST) rewriting,Before it executes your test files, it intercepts Python's normal compilation process and rewrites the assert statements.his is why when a test fails, pytest doesn't just say "Error"; it gives you a highly detailed breakdown of exactly what the variables were at the moment of failure.

#### 3. How it Decides to Give a "Go-Ahead" (Exit Codes)
When integrated into a workflow (like GitHub Actions), pytest tells the system whether everything is safe to proceed using standard Operating System Exit Codes.
- Exit Code 0 (Success):
- Exit Code 1 (Failure):
- Exit Code 2 (Interrupted): user stoped the test
- Exit Code 5 (No tests collected): It ran, but didn't find any files matching test_*.py
