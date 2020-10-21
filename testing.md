## pytest

https://docs.pytest.org/en/stable/

```bash
conda install pytest
```

#### capsys
The **capsys**, **capsysbinary**, **capfd**, and **capfdbinary** fixtures allow access to stdout/stderr output created during test execution. Here is an example test function that performs some output related checks:

  - https://docs.pytest.org/en/stable/capture.html
  
```python

import mod

def test_main(capsys):
  mod.main(['arg'])
  
  out, err = capsys.readouterr()
```

We can exit the main while raising an exception:
```python
def main():
  ...
  
if __name__ == "__main__":
  raise SystemExit(main())
 
```

$? in bash exit code of previous command
```bash
  bash -c 'exit 2'; echo $?
```
### Type annotations
```python
from typing import Optional
from typing import Sequence

def main(argv: Optional[Sequence[str]] = None) -> int:
  parser = argparse.ArgumentParser()
  parser.add_argument('person')
  args = parser.parser_args(argv)
  
  if args.person == '':
    print("Person's name must not be emplty", file=sys.stderr)
    return 1
```

  
#### mypy
Mypy is an optional static type checker for Python that aims to combine the benefits of dynamic (or "duck") typing and static typing. Mypy combines the expressive power and convenience of Python with a powerful type system and compile-time type checking.

```bash
conda install mypy
mypy main.py
```
It can check if files is missing a return statement.

#### Testing in Visual Studio Code
https://code.visualstudio.com/docs/python/testing
The Python extension supports testing with Python's built-in unittest framework as well as pytest. Nose is also supported, although the framework itself is in maintenance mode.

After enabling a test framework, use the Python: Discover Tests command to scan the project for tests according to the discovery patterns of the currently selected test framework. Once discovered, Visual Studio Code provides a variety of means to run tests and debug tests. VS Code displays test output in the Python Test Log panel, including errors caused when a test framework is not installed. With pytest, failed tests also appear in the Problems panel.
