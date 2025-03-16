---
layout: single 
title: "Map, Filter, and Reduce in Python" 
classes: wide
last_modified_at:
---

## Map
The `map` function executes some operation on each item in an iterable series.
The general syntax for the `map` function is;

`map(<function>, <series>)
`
```python
def double(number: int) -> int:
    return number * 2

res = map(double, [1, 2])

print(res)
# output: <map object at 0x00000166222BAC50>
for number in res:
    print(number)
# output:
# 2
# 4
```

or you can use lambda function:
`
```python
res = map(lambda x: x * 2, [1, 2])
```

## Filter
The `filter` is similar to the `map` function, but, it filters them with a criterion function. If the criterion function returns `True`, the item is selected.

```python
even = filter(lambda x: x % 2 == 0, [1, 2, 3, 4])

for number in even:
    print(number)
# output:
# 2
# 4
```

## Reduce
The `reduce` function reduce the items in series into a single value.
It is necessary to import `reduce` function from  the `functools` module.
The general syntax for the `reduce` function is;

`reduce(<function>, <series>, <initial_value>)

```python
from functools import reduce
  
numbers = [1, 2, 3, 5]
total = reduce(lambda reduced_sum, x: reduced_sum + x, numbers, 0)

print(total)
# output: 11
```

The `reduce` function takes three arguments:
- function
- series of items
- initial value

### Function
The first argument, function, represents the operation we want to perform on each item.

```python
lambda reduced_sum, x: reduced_sum + x
```
in which, the `reduced_sum` is a current reduced value and  the `x` is a item whose turn it is to be processed. In each turn, the lambda function return the sum of current reduced value and item.

This lambda function is equivalent to the normal function below;

```python
def sum_helper(reduced_sum, item):
  return reduced_sum + item
  
numbers = [1, 2, 3, 5]
total = reduce(sum_helper, numbers, 0)

print(total)
# output: 11

```

### Initial value
The third argument, initial value, is optional.
If the initial value is left out, `reduce` takes the first item in the list as the initial value and starts reducing from the second item onwards.
