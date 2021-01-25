# Global Keyword

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

Example:

```python
messages = ["Hello", "How are you?"]

def example1():
  print(messages)
  
def example2():
  messages[0] = "hi"
  
def example3():
  messages.append("Nice hat")
  
def example4():
	# global messages
  messages = ["Goodbye", "See you later"]
```

Without the global keyword, you can read and use global variables but you can't change their value. Example 2 & 3 are just USING the messages variable, basically calling a method/property of it. But example 4 is actually trying to re-assign it (i.e. change the value)

