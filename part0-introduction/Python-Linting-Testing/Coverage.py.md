### `Coverage.py` is a separate tool (often integrated into pytest via the pytest-cov plugin) that measures code execution.
#### 1. How Coverage.py Tracks Code Execution
pytest doesn't inherently look at your source code to see if you missed something; it only runs the tests you wrote. Coverage.py is the supervisor that watches pytest work.
It uses Python's built-in system tracing hooks (sys.settrace). When pytest starts running a test function, Coverage.py monitors every single line of your application code that gets compiled and executed in response.

The Breakdown:
* Statement Coverage: It looks at your source code, counts the total number of executable lines, and checks off each line that gets run during the test suite.
* Branch Coverage: If you have an if/else statement, it checks if your tests triggered both the True and False paths.

#### 2. An Example of How It Finds "Blind Spots"
eg `calculator.py`
```py
def divide(a, b):
    if b == 0:
        return "Cannot divide by zero!"  # Line A
    return a / b                         # Line B
```  
And you write this test in `test_calculator.py`
```
def test_normal_division():
    assert divide(10, 2) == 5
```
When you run `pytest --cov=src`, here is what happens:  
1. pytest runs `test_normal_division()`.
2. The code hits if b == 0 (False) and then executes Line B (return a / b).
3. The test passes! pytest gives a green light (Exit Code 0).
4. However, Coverage.py flags a warning: Line A was never executed. It will report that your code only has 66% test coverage.

#### 3. Deciding the "Go-Ahead" Based on Coverage
In a professional development workflow, teams don't just require tests to pass; they also require a minimum percentage of the code to be test
You can configure pytest to automatically fail the entire build if your coverage drops below a certain threshold (e.g., 90%)
```bash
pytest --cov=src --cov-fail-under=90
```
eg : Even if all your existing tests pass flawlessly, if you write a new feature and forget to write tests for it, Coverage.py will drop the score below 90%. It will force pytest to exit with a failure code (Exit Code 1), blocking the code from being deployed until you write the missing tests.
