#Python Style Guide

This is a basic style guide that I started writing after reviewing lots of Python code. This is how I personally write Python code and I feel that this may help others write more readable code. This is distributed under a BSD license so please feel free to use and modify. Since I have worked with a large amount of Django code, I may provide some examples that are specific to Django. You may take these examples are 'port' them to any application you are using

This guide is for Python 2.7. Some code listed may be incompatible with older or newer versions of Python

#Basic Types
## Strings
### .format
When creating strings always use `.format`. When you have one or two identifiers you may use numbers as place holders e.g `{0}`. However when you have may identifiers and the using numbers can be ambiguous it is important to use names identifiers  e.g `{name}`.
**DO**

```
print "Hello {name}, {greeting}".format(name="Levi", greeting="Welcome Home")
```

**DON'T**

```
print "Hello %s, %s" % ("Levi", "Welcome Home")
```
### String Concatenation
String concatenation should be done as if it were string construction
**DO**

```
mystr1 = "Hello"
mystr2 = "World"

greeting = "{0}{1}".format(mystr1, mystr2)

```

**DON'T**

```
mystr1 = "Hello"
mystr2 = "World"

greeting = mystr1 + mystr2

```
### .find, .rfind, .startswith, .endswith, .replace

Python provides some great helper methods with strings. Many people coming from other languages are temped to use regex's using Python's `re` model. I have nothing against regex's but these methods are faster and more straight forward.
##Collections
###Lists
List should be used as modifiable arrays. You should make use of `[].append()` and `[].extend()` when using lists. Use of addition when adding to a list is ambiguous and should be avoided. Additionally They should **NOT** be used in a case where the *collection* of data does not need to be modified e.g `valid_name = ['first_name', 'last_name',]` . This case should be a tuple.
#### List Use cases
**DO**
```
from django.contrib.auth.models import User
mylist = []
for user in Users.objects.filter(is_active=True):
    if user.first_name.startswith('A'):
          mylist.append(user)

...
mylist.remove(user)
```
**DON'T**
```
from django.contrib.auth.models import User
from django.views.generic import TemplateView

class AllUsers(TemplateView):
    template_name = 'application/all_users.html'

    def get_context_data(self, **kwargs):
        return {
            'all_users': list(Users.objects.all()),
            }
```
Use a **tuple** in this case.
**Correct**
```
from django.contrib.auth.models import User
from django.views.generic import TemplateView

class AllUsers(TemplateView):
    template_name = 'application/all_users.html'

    def get_context_data(self, **kwargs):
        return {
            'all_users': tuple(Users.objects.all()),
            }
```

### Tuple use cases
Tuples are immutable and should be used as such within your application. If you ever find yourself using `+=` with a tuple **you should be using a list**. 


##List/Set/Dictionary Comprehensions

###When to use list comprehensions
When you are creating a list of item list comprehensions are great!

List comprehensions are here to replace some types for loops but not every for loop. E.g

**DO**

`mylist = [letter for letter in 'Hello World' if letter is not 'l']`

**DON'T**
```
mylist = []
for letter in 'Hello World':
    if letter is 'l':
        continue
    mylist.append(letter)
```

## Loops
### For loops
You may be temped to write a bunch of list comprehensions instead of for loops. You must understand that list comprehensions replace certain types of  for loops but not all.
**DO**
`y = [x for x in 'Hello World' if x is not 'h']`
**DON'T**
`[mylist.sort() for mylist in list_of_lists]`



