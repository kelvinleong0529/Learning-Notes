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

## **Using Models**
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