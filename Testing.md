### pytest

#### capsys
The capsys, capsysbinary, capfd, and capfdbinary fixtures allow access to stdout/stderr output created during test execution. Here is an example test function that performs some output related checks:

  - https://docs.pytest.org/en/stable/capture.html
  
```python

import mod

def test_main(capsys):
  mod.main(['arg'])
  
  out, err = capsys.readouterr()
