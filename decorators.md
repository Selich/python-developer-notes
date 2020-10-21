## Decorators

Lets build our own decorator:
```python
def dec(func):
  def dec_inner(*args, **kwargs):
    return func(*args, **kwargs)
  return func

@dec
def f(x):
  print(f'hello {x}')
  
f(1)
  
```
Function dec *decorates* function f.
