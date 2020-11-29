# Global

global keyword required for immutable times (tuples, strings etc)

foo.py:

```python
name = 'Ralph'

def edit_name(string):
  global name
  name = string
  
def get_name():
  return name
```

```python
import foo
print(foo.get_name())
foo.edit_name('Hayden')
print(foo.get_name())
```



