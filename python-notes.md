## Python Notes

* Strings are immutable just like in Java, to change a character you can convert it to a list by doing `list(s)` and then after the changes are done just use `join()` to create a new modified string.

* `set()` takes an iterable (tuple, string, etc) and then adds its elements to the set. 

-----

* **`any(iterable)`** is a built-in Python function that returns `True` if **any element** in the iterable is truthy. Otherwise, it returns `False`.

```python
  any([False, True, False])  # → True
```

You can combine it with generator expressions:

```python
any(c in "hello" for c in "aeiou")  # → True
```

This checks if any vowel is present in the word without building an intermediate list.
A generator expression (e.g., (c in word for c in vowels)) returns a generator object, which:

- Is an iterable (__iter__() is implemented)

- Is also an iterator (__next__() is implemented)

- Evaluates lazily — doesn't create a list in memory

In Python, an iterable is any object that implements __iter__(), including:

- Strings (str)
- Lists (list)
- Tuples (tuple)
- Dictionaries (dict)

Generators are instances of the built-in generator type and conform to both Iterable and Iterator via Python’s collections.abc.

-----

* `lambda`

A `lambda` is an **anonymous function**, a function without a name.

### Example
```python
f = lambda x: x * 2
```

Equivalent to:

```python
def f(x):
    return x * 2
```

----

* `global`

Used inside a function to tell Python you want to modify a module-level variable.

Example:

```py
x = 10

def change():
    global x
    x = 99
```


Without `global x`, Python would treat `x = 99` as a local variable.

----

* `*args`

Captures extra positional arguments into a tuple.

```py
def f(*args):
    print(args)

f(1, 2, 3)  # (1, 2, 3)
```

-----

 * `**kwargs`

Captures extra keyword arguments into a dictionary.

```py
def f(**kwargs):
    print(kwargs)

f(name="John", occupation="engineer")
```

----