# **Models**
- each `model` is a python class that subclasses `django.db.model.Models`
- each attribute of the model represents a database field
- the following example `model` defines a Person, which has `first_name` and `last_name`:
```python
from django.db imports models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)

# 'first_name' and 'last_name' are fields of the model
# each fiekd is specified as a class attribute, and each attribute maps to a database column
```
- the above `Person` model would create a database table like this:
```sql
CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varhcar(30) NOT NULL
)
```

# **Using Models**
- once we defined our models, we need to tell `Django` that we're going to use those models
- edit the setting files by changing the `INSTALLED_APPS` setting to add the name of the module that contains our `model.py`

# **Fields**
```python
from django.db import models

class Musician(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    instrument = models.CharField(max_length=100)

class Album(models.Model):
    artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    release_date = models.DateField()
    num_stars = models.IntegerField()
```

# **Model Inheritance**
- model inheritance is possible in `Django`, we need to decide whether we want the parent models to be models in their own right (having their own database tables), or if the parents are just holders of common information that will only be visible through the child models
- 3 types of inheritance in `Django`:
1. `Abstract Base Class`: we only want to use the parent class to hold information that we dont want to have to type out for each child model, this class isnt going to be ever used in isolation
2. `Multi-Table Inheritance`: if we subclass an existing model (perhaps something from another application entirely) and want each model to have its own database table
3. `Proxy Models` if we only want to modify the python-level behaviour of a model, without changing the models field in any way

## **1. Abstract Class**
- useful when we want to put some common information into a number of other modules
```python
from django.db import models

class CommonInfo(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()

    class Meta:
        abstract = True

class Student(CommonInfo):
    home_group = models.CharField(max_length=5)
```
- `CommonInfo` model cannot be used as a normal Django model, it doesnt generate a database table or have a manager, and cannot be instantiated or saved directly
- `Student` model will have 3 fileds: `name`, `age`, and `home_group`

## **2. Multi-table Inheritance**
- each model in the hierarchy is a model by itself
- each model corresponds to its own database and can be queried and created individually (a new database table is created for each subclass of a model)
```python
from django.db import models

class Place(models.Model):
    name = models.CharField(max_length=50)
    address = models.CharField(max_length=80)

class Restaurant(Place):
    serves_hot_dogs = models.BooleanField(default=False)
    serves_pizza = models.BooleanField(default=False)
```
## **3. Proxy Models**
- creating a 'proxy' for the original model, we can CRUD instances of the proxy model and all the data will be saved as if we were using the original model
```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)

class MyPerson(Person):
    class Meta:
        proxy = True

    def do_something(self):
        # ...
        pass
```
- `MyPerson` class operates on the same database table as it's parent `Person` class
- any new instances of `Person` will also be accessible through `MyPerson`, and vice-versa