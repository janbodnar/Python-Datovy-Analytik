# Predpoklady

Predpoklady pre školenie *Python dátová analýza I - dátový analytik junior*.  

Je potrebné mať znalosti na úrovni mierne pokročilého programátora v jazyku Python.  

Je dobré už poznať nasledovné oblasti:

- poznať zoznamy, n-tice a slovníky
- dátové typy a operátory
- list comprehensions
- dynamická tvorba reťazcov pomocou fstrings
- moduly
- základy práce s funkciami
- lambda funkcie
- načítanie dát pomocou funkcie open 
- použitie data classes/namedtuples
- poznať základy práce s editormi VS Code alebo PyCharm
- vedieť inštalovať externé moduly pomocou nástroja pip

Preberané učivo Python I-III (všetky príklady a materiály) nájdete na linku: 
https://github.com/janbodnar/Python-Skolenie



## Ukážky príkladov preberaných Python I-III

Nasledujúce ukážky ukazujú typické príklady preberané na začiatočníckych kurzoch.  


### Načítanie slov zo súboru a ich filtrovanie

Súbor `thermopylae.txt`:

```
The Battle of Thermopylae was fought between an alliance of Greek city-states, 
led by King Leonidas of Sparta, and the Persian Empire of Xerxes I over the 
course of three days, during the second Persian invasion of Greece.
```

```python
import re

file_name = 'thermopylae.txt'

with open(file_name, 'r') as f:
    content = f.read()
    print(content)

    words = re.split(r'\W+', content)
    words.pop()
    print(words)

    words_2_3 = list(filter(lambda e: len(e) == 2 or len(e) == 3, words))
    print(words_2_3)
```



### filter funkcia

```python
vals = [1, 2, 3, -4, 0, -8, -9, -1, 9]

positives = list(filter(lambda e: e > 0, vals))
print(positives)

negatives = list(filter(lambda e: e < 0, vals))
print(negatives)
```

```python
words = ['sky', 'war', 'warm', 'water', 'cup', 'cloud', 'forest']

words_w = list(filter(lambda e: e.startswith('w'), words))
print(words_w)

words_w_c = list(filter(lambda e: e.startswith(('w', 'c')), words))
print(words_w_c)

words_3c = list(filter(lambda e: len(e) == 3, words))
print(words_3c)
```



### map funkcia

```python
def twice(e):
    return e * 2

def cube(e):
    return e * e * e

vals = [1, 2, 3, 4, 5]

vals2 = list(map(twice, vals))
print(vals2)

vals_cubed = list(map(cube, vals))
print(vals_cubed)
```

---

```python
def string_upper(e):
    return e.upper()


words = ['sky', 'blue', 'war', 'forest']
# words_uppered = list(map(string_upper, words))
words_uppered = list(map(lambda e: e.upper(), words))

print(words_uppered)
print(words)
```


### map a lambda

```python
vals = [1, 2, 3, 4, 5]

vals2 = list(map(lambda e: e * 2, vals))
print(vals2)

vals_cubed = list(map(lambda e: e * e * e, vals))
print(vals_cubed)
```


### Vypočítaj sumu z CSV dát v súbore

The `data.csv` file:  

```
1,2,3,4,5
6,7,8,9,10
```


```python
mysum = 0
file_name = 'data.csv'

with open(file_name, 'r') as f:
    lines = f.readlines()

    for line in lines:
        fields = line.rstrip().split(",")
        for field in fields:
            mysum += int(field)


print(mysum)
```


### Vypočítaj sumu z CSV dát v reťazci

```python
data = """
1,2,3,4,5
6,7,8,9,10
11,12,13,14,15
"""

mysum = 0

lines = data.splitlines()[1:]
# lines.pop(0)
print(lines)

for line in lines:
    fields = line.split(',')

    for field in fields:
        mysum += int(field)

print(mysum)
```


### Implicitné argumenty

```python
def power(x, y):
    r = 1

    for i in range(y):
        r = r * x

    return r


print(power(3, 2))
print(power(3, 3), end=' ')
print(power(5, 5), end=' ')
```

### Celsius to fahrenheit

```python
def cel_to_fahr(c):
    return c * 9/5 + 32

f1 = cel_to_fahr(100)
f2 = cel_to_fahr(0)
f3 = cel_to_fahr(30)

print(f1, f2, f3)
```


### splitlines funkcia

```python
data = """
sky
dark
warm
water
cup
ten
rock
"""

lines = data.splitlines()
lines.pop(0)
print(lines)
```


### Filtrovanie prázdnych slov

```python
data = """
sky
dark
warm

water
cup

ten

rock
"""

fields = data.split('\n')
print(fields)

words = []

for field in fields:
    if field != '':
        words.append(field)

print(words)
```



### input od užívateľa

```python
x = int(input('enter first integer value: '))
y = int(input('enter second integer value: '))

print(f'addition of {x} and {y} is {x + y}')
print(f'multiplication of {x} and {y} is {x * y}')
```


### Načítanie slov do zoznamu

Súbor `words.txt`

```
sky
work
blue
sky
cup
cloud
pen
storm
```

```python
words = []

file_name = 'words.txt'

with open(file_name, 'r') as f:
    lines = f.readlines()

    for line in lines:
        cleaned_word = line.strip()
        words.append(cleaned_word)


words.sort()
print(words)
```






### Filtering by type

```python
words = []
data = ('sky', 1, 2, True, 'forest', 3.4, 6.7, False, 'water')

for e in data:
    if type(e) == str:
        words.append(e)


print(words)
```


## Floats

```python
# 100 m is 0.1 km

distance = 0.1

# 9.87 s is 9.87/60*60 h

time = 9.87 / 3600

speed = distance / time

print(f"The average speed of a sprinter is {round(speed, 2)} km/h")
print(f"The average speed of a sprinter is {speed} km/h")
```


### Vykonanie operacie x krat

```python
msg = 'hello there!'

i = 1

while i <= 10:
    print(msg)
    i += 1

print('-----------------------')

for i in range(10):
    print(msg)
```


### Podmienečné vypisovanie slov

`words.txt`:

```
war
sky
cup
cloud
nice
water
warm
```

```python
file_name = 'words.txt'

with open(file_name, 'r') as f:

    lines = f.readlines()
    print(lines)

    for line in lines:

        if line.startswith(('w', 'c')):
            print(line.rstrip())
```


### Opakovanie

```python
# vypis hlasku pomocou fstringu
name = 'John Doe'
age = 34
occupation = 'gardener'

msg = f'{name} is {age} years old and he is a {occupation}'
print(msg)


# vypis sumu
# vypis prvy, posledny prvok
vals = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(vals[0])
print(vals[-1])

print(sum(vals))

mysum = 0

for val in vals:
    mysum = mysum + val

print(mysum)


# vypocitaj sumu
data = "1,2,3,4,5,6,7,8,9,10"

mysum2 = 0
fields = data.split(',')

for field in fields:
    mysum2 += int(field)

print(mysum2)
```


### Show Python version and read text file

`words.txt`:

```
war
sky
cup
cloud
nice
water
warm
```

```python

import sys

print(sys.version)
print(sys.executable)


file_name = 'words.txt'

with open(file_name, 'r') as f:

    for line in f:
        print(line.strip())
```


### List comprehensions

```python
vals = [-4, 2, 0, -1, 12, -3]

positive = [e for e in vals if e > 0]
print(positive)

negative = [e for e in vals if e < 0]
print(negative)

words = ['sky', 'ten', 'word', 'tomorrow', 'war', 'pen', 'fly']
words_3 = [word for word in words if len(word) == 3]
print(words_3)
```

```python
words = ['sky', 'ten', 'word', 'tomorrow', 'war', 'pen', 'fly', 'float']
# words_w_f = [word for word in words if word.startswith('w') or word.startswith('f')]
words_w_f = [word for word in words if word.startswith(('w', 'f'))]
print(words_w_f)
```

```python
a = ['a', 2, 1.2, 'c', 12, 3, 'd', 23.4]

b = [e for e in a if type(e) == int]
c = [e for e in a if type(e) == str]
d = [e for e in a if type(e) == float]

print(b)
print(c)
print(d)

float_values = []

for val in a:
    if type(val) == float:
        float_values.append((val))

print(float_values)
```


### Read CSV data into namedtuples

```python
from collections import namedtuple
import csv

User = namedtuple('User', 'first_name last_name occupation')

file_name = 'users.csv'
users = []

with open(file_name, 'r') as f:

    reader = csv.reader(f)

    for fields in reader:
        # user = User(fields[0], fields[1], fields[2])
        user = User(*fields)
        users.append(user)


print(users)
```

### Simple namedtuples

```python
from collections import namedtuple

User = namedtuple('User', 'first_name last_name occupation')

u1 = User('John', 'Doe', 'gardener')
# print(u1)

print(f'{u1.first_name} {u1.last_name} is a {u1.occupation}')

u2 = User('Roger', 'Roe', 'driver')
# print(u2)
print(f'{u2.first_name} {u2.last_name} is a {u2.occupation}')
```


```python
def cube(x):
    return x * x * x

c = 5

print(f'The cube of {c} is {cube(c)}')
```

### Úlohy

```python
# vypis hlasku pomocou fstringu
name = 'John Doe'
age = 34
occupation = 'gardener'

# vypis prvy, posledny, sumu
vals = [1, 2, -3, -5, 0, 3, 4, 9]

# vypocitaj sumu z cisiel
data = '1,2,3,4,5,6,7,8,9,10'
```


### Riešenie

```python
# vypis hlasku pomocou fstringu
name = 'John Doe'
age = 34
occupation = 'gardener'

msg = f'{name} is {age} years old, he is a {occupation}'
print(msg)

# vypis prvy, posledny, sumu, min, max, velkost
vals = [1, 2, -3, -5, 0, 3, 4, 9]
print(min(vals))
print(max(vals))
print(sum(vals))
print(vals[0])
print(vals[-1])
print(len(vals))


# vypocitaj sumu z cisiel
data = '1,2,3,4,5,6,7,8,9,10'

fields = data.split(',')
print(fields)
mysum = 0

for field in fields:
    mysum += int(field)

print(mysum)
```





