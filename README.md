#Python Style Guide

This is a basic style guide that I started writing after reviewing lots of Python code. This is how I personally write Python code and I feel that this may help others write more readable code. This is distributed under a BSD license so please feel free to use and modify.

This guide is for Python 2.7. Some code listed may be incompatible with older or newer versions of Python

#Basic Types
## Strings
When creating strings always use `.format`. When you have one or two identifiers you may use numbers as place holders e.g `{0}`. However when you have may identifiers and the using numbers can be ambiguous it is important to use names identifiers  e.g `{name}`.
**DO**

```
print "Hello {name}, {greeting}".format(name="Levi", greeting="Welcome Home")
```

**DON'T**

```
print "Hello %s, %s" % ("Levi", "Welcome Home")
```

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
return render_to_response('my_template.html', {'users': list(User.objects.all()),}, context_instance=RequestContext(request))
```
Use a **tuple** in this case.
**Correct**
```
return render_to_response('my_template.html', {'users': tuple(User.objects.all()),}, context_instance=RequestContext(request))
```

### Tuple use cases


##List/Set/Dictionary Comprehensions

####When to use list comprehensions
When you are creating a list of item list comprehensions are great!

`y = [x for x in 'Hello World' if x is not 'h']`

####When NOT to use list comprehensions
`[mylist.sort() for mylist in list_of_lists]`

List comprehensions are here to replace some types for loops but not every for loop. E.g

They replace the following loop
```
mylist = []
for letter in 'Hello World':
    if letter is 'l':
        continue
    mylist.append(letter)
```

**With**

`mylist = [letter for letter in 'Hello World' if letter is not 'l']`


