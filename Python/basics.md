# **Naming Convention**
## **1. Single Leading Underscore**
- used to define **internal** attributes, these attributes are not meant to be accessed from the outside of the class, these attributes mostly needed internally for intermediate computations

## **2. Single Trailing Underscore**
- used on variables that is actually a reserved key word in Python
```python
class_ = "A
def_ = "Halo"
```

## **3. Single Underscores**
- to define temporary or unused variables
```python
for _ in range(100):
    do_some_work()
```
- we only want to access certain elements from tuples
```python
cpu,_,_,memory,_ = extract_laptop_specs(laptop)
# we only extract the 1st and 4th element from the tuple returned
```
- the result of the last evaluation in python interactive interpreter is store in "_"

## **4. Double Leading and Trailing Underscores**
- used to define speical universal methods called **dunder methods**
- dunder methods are reserved methods that we can still overwrite, they have special behaviour and are called differently
```python
1. __init__
2. __call__
```

## **5. Double Leading Underscores**
- typically used for name mangling, a process by which the interpreter changes the attribute name to avoid name collission in subclasses