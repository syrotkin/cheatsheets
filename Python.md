# Introspection

https://www.golinuxcloud.com/python-type-of-variable/

```python
type(foo)

print (Foo.__class__)
#
print(Foo.__bases__)
print(Foo.__dict__)
print(Foo.__doc__)
```

https://stackoverflow.com/questions/34439/finding-what-methods-a-python-object-has

```python
l = []
dir(l)
# we can see that insert is one of the methods
l.insert.__doc__
# returns the documentation string about the insert method
```
