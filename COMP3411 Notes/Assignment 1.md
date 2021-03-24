# 1.1 List Processing

```python
def sumsq_even(list):
	if not list:
    return 0
  return (list[0] % 2) * list[0] ** 2 + sumsq_even(list[1:])
```

```
sumsq([]) :- 0.

sumsq([Head | Tail], Sum) :- 
```

