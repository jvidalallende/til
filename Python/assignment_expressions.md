# Assignment expressions (a.k.a. the Walrus operator)

As part of [PEP 572][00], which was part of Python 3.8, the language introduced
a way to perform an assignment and return the value being assigned at the same time,
by using the [Walrus][01] operator `:=`.

Among other things, this allows more concise code in some situations. Here are some
examples taken from [PEP 572][00]:

```python
# Capture a "witness" from `any()`
if any((comment := line).startswith('#') for line in lines):
    print("First comment:", comment)
else:
    print("There are no comments")
```

```python
# Compute partial sums in a list comprehension
total = 0
partial_sums = [total := total + v for v in values]
print("Total:", total)
```

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://peps.python.org/pep-0572/
[01]: https://en.wikipedia.org/wiki/Walrus
