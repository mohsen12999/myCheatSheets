# Python

* use Anaconda for having package of python library and editor like jupiter and spider. add to path when install anaconda.

see python version

```sh
python --version
```

run python program

```sh
python helloworld.py
```

python command line, `exit()` for exit;

```sh
python
python3
```

```py
__author__='mohsen'
```

## Print

```py
print("Hello world!")
print() #blank line
print("Hello"+"world!")
print("double qoute can use ' in it")
print('single qoute can use " in it')
# comment
"""This is a
multiline docstring."""
name = "ali"
print("hello "+name)
print("\t\n\"")
var severalLineString = """several
                            line
                            string"""
```

## Variable

```py
greeting ="bruce"
_name2 = "ali"
age = 23
# print(_name2 + age) -> make error, can not convert int to string
print(_name2 + str(age))
```

```py
a = 12
b = 3
print(a + b)
print(a - b)
print(a * b)
print(a / b)  # return float
print(a // b) # return int
print(a % b)
```

```py
parrot = "Norwegian Blue"
print(parrot)
print(parrot[0]) # first charachter
print(parrot[-1]) # last charachter
print(parrot[0:6]) # 6 first charachter
print(parrot[:6]) # 6 first charachter 0-5
print(parrot[6:]) # from 6 to end
print(parrot[-4:-2])
print(parrot[0:6:2]) # 0-5 with step of 2

numbers = "1, 2, 3, 4, 5, 6, 7, 8, 9"
print(numbers[0::3]) # start to end with step of 3 -> only number
```

```py
print("Hello"*5) # print Hello 5 time
today = "friday"
print("day" in today) # return True
print("parrot" in "bird") # return False
```

```py
age = 24
print("My age is " + str(age) + " years")
print("My age is {0} years".format(age))
print("My name is {0} age is {1} years & avg is {2}".format("mohsen",age,14.2))
print("My age is %d years" % age) # old way
print("My age is %d %s, %d %s" % (age, "years",6,"months")) # %d for digit and %s for string
# %4d => minimum 4 space for number equal to {0:4} and {0:<4} => number in left hand side
print("Pi is approximately %12f" %(22/7)) # 12 space for number =>{0:12}
print("Pi is approximately %12.50f" %(22/7)) # 50 decimal point =>{0:12.50}
# we can use {} and python use variable outomatically. we can alseo use {:4} and more
```

## Number

```py
x = 1    # int
x1 = 35656222554887711
x2 = -3255522

y = 2.8  # float
y1 = 35e3
y2 = 12E4
y3 = -87.7e100

z = 1j   # complex
z1 = 3+5j
z2 = -5j

print(type(x))
print(type(y))
print(type(z))
```

## casting

```py
x1 = int(2.8) # x1 will be 2
x2 = int("3") # x2 will be 3

y1 = float("3") # y1 will be 3.0

s1 = str("s1") # s1 will be 's1'
s2 = str(2)    # s2 will be '2'
s3 = str(3.0)  # s3 will be '3.0'
```

## String

```py
a = "Hello, World!"
print(a[1]) # e
print(b[2:5])
print(a.strip()) # like trim, returns "Hello, World!"
print(len(a))
print(a.lower())
print(a.upper())
print(a.replace("H", "J"))
print(a.split(",")) # returns ['Hello', ' World!']

print("Enter your name:")
x = input()
print("Hello, " + x)
```

## Operators

* Arithmetic: `+`, `-`, `*`, `/`, `//`, `**`, `%`
* Augumented Assignment: `+=`, `-=`, `*=`, `/=`, `//=`, `**=`, `%=`
* Comparison Operators: `==`, `!=`, `>`, `<`, `>=`, `<=`
* Logical Operators: `and`, `or`, `not`
* Identity Operators: `is`, `is not`
  * `is` Returns true if both variables are the same object
* Membership Operators: `in`, `not in`
  * `in` Returns True if a sequence with the specified value is present in the object
* Bitwise Operators: `&`, `|`, `^`(XOR), `~`(NOT),`<<`, `>>`

```py
# long string
input = "ddfdfdfdfdffgdg g fgdfg df" \
        "dfdfdffd  djdfd"
input = ("ddfdfdfdfdffgdg g fgdfg df"
         "dfdfdffd  djdfd")
```

## if statement

* `==`, `!=`, `>`, `<`, `>=`, `<=`

```py
name = input("Please enter your name: ")
age = int(input("Hoew old are you, {}?".format(name)))

if age >= 18:
    print("You are old enough to vote.") # must have indent (space in start of line)
else:
    print("Please come back in {0} years.".format(18-age))

print("please enter number between 1 to 10: ")
guess = int(input())
if guess < 5:
    print("please enter higher")
elif guess > 5:
    print("please enter lower")
else:
    print("you got it!")

age = int(input("How old are you?"))
if 16 <= age <= 65: # equal to if age >= 16 and age <=65:
    print("have a good day at work")

if (age<16) or (age>65):
    print("enjoy your free time")

if a > b and c > a:
  print("Both conditions are True")
  
x = "False"
if x:
    print("x is True or have none zero value") # its run
else
    print("x is False or zero or None or empty string or empty list or empty tuple or empty mapping , ...")

print(not False) # return True
print(not True) # return False
# if not(age<18)
```

### Short Hand

```py
if a > b: print("a is greater than b")

print("A") if a > b else print("B")

print("A") if a > b else print("=") if a == b else print("B")
```

## for loop

```py
number = "9,317,545,354,748,898"
for i in range(0, len(number)): # 0 to length-1
    print(number[i])

for i in range(0, len(number)):
    if number[i] in '0123456789':
        print(number[i],) # with , in end of print its not going to new line => print(number[i],end='') ,can be end='\n' or end='\t' or anything

cleanNumber=''
for i in range(0, len(number)):
    if number[i] in '0123456789':
        cleanNumber = cleanNumber + number[i]
newNumber =  int(cleanNumber)
print(newNumber)

cleanNumber=''
for char in number:
    if char in '0123456789':
        cleanNumber = cleanNumber + number[i]

for state in ["good","not good","bad"]:
    print(state)

for i in range(0,100,5): # 0 to 100 with step 5
    print(i)

for i in range(1,13):
    for j in range(1,13):
        print("{1} times {0} is {2}".format(i,j,i*j))
    print("=======================")
```

```py
shopping_list = ["milk", "pasta", "eggs", "spam", "bread", "rice" ]
for item in shopping_list:
    if item == "spam":
        continue # back to top of the loop
    print("Buy "+item)

meal = ["egg", "beacon","spam","sausages"]
for item in meal:
    if item == "span":
        nasty_food_item = item
        break # break the loop
else:
    print("I'll have a plate of that, then, please") # if dont break in loop go here
if nasty_food_item: # if we have'nt go to if we have error here
    print("Can't I have anything without spam in it")
```

## While Loop

```py
i = 0
while i<10:
    print("i is now {}".format(i))
    i += 1

while True:
    print("infinit loop")

available_exits = ["east", "north east", "south" ]
chosen_exit=""
while chosen_exit not in available_exits:
    chosen_exit = input("please choose a direction: ")
print("arent you glad you get out of there!")

while chosen_exit not in available_exits:
    chosen_exit = input("please choose a direction: ")
    if chosen_exit == "quit":
        print("Game over")
        break
else:
    print("arent you glad you get out of there!")
```

```py
import random

highest = 10
answer = randeom.randint(1, highest)

print("please guess a number between 1 and {}".format(highest))
guess = 0 # initial number and outside of valid range
while guess != answer:
    guess = int(input())
    if guess < answer:
        print("please guess higher")
    elif guess > answer:
        print("please guess lowe")
    else:
        print("well done, you guess it")
```

```py
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)
```

## Range

```py
range(100) #range(0,100)
my_list = list(range(10)) # [0,...,9]
even = list(range(0,10,2))
odd = list(range(1,10,2))
print(range(0, 5, 2)==range(0,6,2)) # True
r=range(0,100)
for i in r[::-2]: #range(99,0,-2)
    print(i) # 99 97 95 ...

string = "nohtyp"
print(string[::-1]) # reverse string
```

## Binary

[decimal computer](http://www.bbc.com/news/technology-20155028)

```py
for i in range(17)
    print("{0:>2} in binary is {0:>08b}.format(i)")
```

## Hexadecimal & Octal

```py
for i in range(17)
    print("{0:>2} in binary is {0:>02x}.format(i)")

hex=0x20 #hexadecimal number
oct=0o26 #Octal number
bin=b010100101 #binary
```

## List

* A list is a collection which is ordered and changeable.

```py
ipAddress = "127.0.0.1"
ipAddress.count(".")
len(ipAddress)
```

```py
parrot_list = ["non pinin", "no more", "a stiff"]
parrot_list.append("A Norwegian Blue")

even = [2, 4, 6, 8]
add = [1,3,5,7,9]
numbers = even + odd
numbers.sort() # have no output
print(numbers)
sorted_numbers = sorted(number)
if sorted_numbers == numbers: # must have same member and same order
    print("the lists are equal")

numbers.sort(reverse=True)
print(sorted_numbers == numbers) # False
print(sorted_numbers in numbers) # True
```

```py
list_1 = []
list_2 = list()
if list_1 == list_2: # both are empty list
    print("the lists are equal")
print(list("Hello")) # ["H", "e", "l", "l", "o"]

even = [2,4,6,8]
another = list(even)
print(even in another) # False
print(even == another) # True
```

```py
even = [2, 4, 6, 8]
add = [1,3,5,7,9]
numbers = [even,odd]
for number_set in numbers:
    print(number_set)
    for value in number_set:
        print(value)
```

```py
menu=[]
menu.append(["egg","spam","beacon"])
menu.append(["egg","sausage","beacon"])
menu.append(["egg","spam"])
menu.append(["egg","spam","sausage","beacon"])
for meal in menu:
    if not "spam" in meal:
        print(meal)
```

```py
thislist = ["apple", "banana", "cherry"]
thislist.insert(1, "orange")
thislist.remove("banana")
thislist.pop() # The pop() method removes the specified index, (or the last item if index is not specified)
del thislist[0]
thislist.clear()
thislist = list(("apple", "banana", "cherry")) # Using the list() constructor to make a List
```

## Tuple

* A tuple is a collection which is ordered and unchangeable.

```py
t = "a", "b", "c" # its tuple
t2 = ("a", "b", "c")
mettalica = "Ride the Lightening", "Mettalica", 1984
print(mettalica)
print(mettalica[0])
# mettalica[0] = "Master of Puppets" # can not change
mettalica = mettalica[0], "Master of Puppets",mettalica[2]
```

```py
a=12
b=13
a,b=b,a # swap

mettalica = "Ride the Lightening", "Mettalica", 1984
title, artist, year = mettalica # unpack tuples

imelda = "More Mayhem", "Imelda May", 2011, {(1,"pulling the Rug"),(2,"Psycho"),(3,"Meyhem")}
title, artist, year, tracks = imelda

imelda2 = "More Mayhem", "Imelda May", 2011, {[(1,"pulling the Rug"),(2,"Psycho"),(3,"Meyhem")]} # make list
imelda2[3].append((6,"Eternity")) # add to list in tuple
```

```py
thistuple = ("apple", "banana", "cherry")
print(len(thistuple))
del thistuple
thistuple = tuple(("apple", "banana", "cherry")) # Using the tuple() method to make a tuple
```

## Dictionary

* A dictionary is a collection which is unordered, changeable and indexed.

```py
fruit={"apple":"red sweet fruit", "orange":"citrus fruit"}
print(fruit)
print(fruit["apple"])
print(fruit.get("apple"))
print(fruit.get("apple","we dont have apple"))
fruit["pear"]="an odd shape fruit" #insert new member
fruit["apple"]="red or yellow sweet fruit" #update member
fruit.clear() #remove all

if "grape" in fruit: #search in key
    print("we have grape")
for snack in fruit:
    print(snack + " is "+ fruit[snack])

key_list=fruit.keys()
for snack in sorted(fruit.keys()): #list sort by key
    print(snack + " is "+ fruit[snack])

values=fruit.values()

f_tuple=tuple(fruit.items())

st=", ".join(fruit.keys()) #make string of keys

veg={"spinach":"green one"}
veg.update(fruit) #add fruit to end of veg

fruit=fruit.copy()
```

## Sets

* A set is a collection which is unordered and unindexed

```py
farm_animals={"sheep","cow","hen"} #first way
wild_animals=set(["lion","wolf","hare","tiger"])#second way
farm_animal.add("horse")
a={} #empty dictionary
a2=set() #empty set
farm_animals.union(wild_animals) # add only new member
farm_animals.intersection(wild_animals) # get only mamber both have
farm_animals.diffrent(wild_animals)
farm_animals.diffrent_update(wild_animals) # equqal to farm_animal-wild_animal

farm_animal.discard("cow")
farm_animal.remove("hen")
farm_animal.discard("not_member") # no error

if "not_member" in farm_animal:
    farm_animal.discard("not_member") #for no error

try:
    farm_animal.discard("not_member")
except KeyError:
    print("its not a member")

if even.issubset(number)::
    print("subset")
if number.issuperset(even):
    print("superset")

even = frozenset(range(0,100,2)) # cant add or remove member
# even.add(3) have error
```

## Function

```py
def my_function():
  print("Hello from a function")

my_function()
```

### Parameters

```py
def my_function(fname):
  print(fname + " Refsnes")

my_function("Emil")
```

### Default Parameter Value

```py
def my_function(country = "Norway"):
  print("I am from " + country)

my_function("Sweden")
my_function()
```

### Return Values

```py
def my_function(x):
  return 5 * x

print(my_function(3))
```

### Recursion

```py
def tri_recursion(k):
  if(k>0):
    result = k+tri_recursion(k-1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6)
```

## Lambda

* lambda arguments : expression

```py
x = lambda a : a + 10
print(x(5))

x = lambda a, b : a * b
print(x(5, 6))
```

```py
def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)
print(mydoubler(11))

mytripler = myfunc(3)
print(mytripler(11))
```

## Class

```py
class MyClass:
  x = 5

p1 = MyClass()
print(p1.x)
```

```py
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)

print(p1.name)
print(p1.age)
```

```py
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self):
    print("Hello my name is " + self.name)

p1 = Person("John", 36)
p1.myfunc()
```

## Iterators

```py
string = "1234567890"
my_iterator = itr(string)
print(my_iterator) #<str_itrator ...
print(next(my_iterator)) # 1
print(next(my_iterator)) # 2

for char in string: # python convert string to itr(string)
    print(char)
```

```py
my_list = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"]
my_iterator = itr(my_list)
for i in range(0, len(my_list)):
    next_item = next(my_iterator)
    print(next_item)
```

### Create an Iterator

```py
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myclass = MyNumbers()
myiter = iter(myclass)

print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
```

### StopIteration

```py
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    if self.a <= 20:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

myclass = MyNumbers()
myiter = iter(myclass)

for x in myiter:
  print(x)
```

## Modules

* A file containing a set of functions you want to include in your application.

### Create a Module

```py
# mymodule.py
def greeting(name):
  print("Hello, " + name)
person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
}

# use in app
import mymodule
mymodule.greeting("Jonathan")
a = mymodule.person1["age"]
```

### Re-naming a Module

```py
import mymodule as mx

a = mx.person1["age"]
print(a)
```

### Import From Module

```py
# mymodule
def greeting(name):
  print("Hello, " + name)

person1 = {
  "name": "John",
  "age": 36,
  "country": "Norway"
}

# use
from mymodule import person1

print (person1["age"])
```

### dir

* list all the function names (or variable names) in a module.

```py
import platform

x = dir(platform)
print(x)
```

## Datetime

```py
import datetime

x = datetime.datetime.now()
print(x) # 2019-02-09 12:06:04.546695
print(x.year) # 2016
print(x.strftime("%A")) # Saturday
print(x.strftime("%B")) # February
print(x.strftime("%c")) # Sat Feb  9 12:11:43 2019
print(x.strftime("%x")) # 02/09/19
print(x.strftime("%X")) # 12:11:43

x2 = datetime.datetime(2020, 5, 17)
```

## JSON

```py
import json

# some JSON:
x =  '{ "name":"John", "age":30, "city":"New York"}'

# parse x:
y = json.loads(x)

# the result is a Python dictionary:
print(y["age"])
```

```py
import json

# a Python object (dict):
x = {
  "name": "John",
  "age": 30,
  "city": "New York"
}

# convert into JSON:
y = json.dumps(x)

# the result is a JSON string:
print(y)
```

```py
import json

print(json.dumps({"name": "John", "age": 30}))
print(json.dumps(["apple", "bananas"]))
print(json.dumps(("apple", "bananas")))
print(json.dumps("hello"))
print(json.dumps(42))
print(json.dumps(31.76))
print(json.dumps(True))
print(json.dumps(False))
print(json.dumps(None))
```

```py
import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}

print(json.dumps(x))
```

```py
json.dumps(x, indent=4)
json.dumps(x, indent=4, separators=(". ", " = "))
json.dumps(x, indent=4, sort_keys=True)
```

## Regex

* `findall` Returns a list containing all matches
* `search` Returns a Match object if there is a match anywhere in the string
* `split` Returns a list where the string has been split at each match
* `sub` Replaces one or many matches with a string

```py
import re

txt = "The rain in Spain"
x = re.search("^The.*Spain$", txt)
```

* `[]`  A set of characters  "[a-m]"
* `\`  Signals a special sequence (can also be used to escape special characters) "\d"
* `.` Any character (except newline character) "he..o"
* `^` Starts with "^hello"
* `$` Ends with "world$"
* `*` Zero or more occurrences "aix*"
* `+` One or more occurrences "aix+"
* `{}` Excactly the specified number of occurrences "al{2}"
* `|` Either or "falls|stays"
* `()` Capture and group

* `\A` Returns a match if the specified characters are at the beginning of the string "\AThe"
* `\b` Returns a match where the specified characters are at the beginning or at the end of a word r"\bain"    r"ain\b"
* `\B` Returns a match where the specified characters are present, but NOT at the beginning (or at the end) of a word r"\Bain"    r"ain\B"
* `\d` Returns a match where the string contains digits (numbers from 0-9) "\d"
* `\D` Returns a match where the string DOES NOT contain digits "\D"
* `\s` Returns a match where the string contains a white space character "\s"
* `\S` Returns a match where the string DOES NOT contain a white space character "\S"
* `\w` Returns a match where the string contains any word characters (characters from a to Z, digits from 0-9, and the underscore _ character) "\w"
* `\W` Returns a match where the string DOES NOT contain any word characters "\W"
* `\Z` Returns a match if the specified characters are at the end of the string "Spain\Z"

* `[arn]` Returns a match where one of the specified characters (a, r, or n) are present
* `[a-n]` Returns a match for any lower case character, alphabetically between a and n
* `[^arn]` Returns a match for any character EXCEPT a, r, and n
* `[0123]` Returns a match where any of the specified digits (0, 1, 2, or 3) are present
* `[0-9]` Returns a match for any digit between 0 and 9
* `[0-5][0-9]` Returns a match for any two-digit numbers from 00 and 59
* `[a-zA-Z]` Returns a match for any character alphabetically between a and z, lower case OR upper case
* `[+]` In sets, +, *, ., |, (), $,{} has no special meaning, so [+] means: return a match for any + character in the string

### findall

```py
import re

str = "The rain in Spain"
x = re.findall("ai", str)
print(x) #['ai', 'ai']
```

### search

```py
import re

str = "The rain in Spain"
x = re.search("\s", str)

print("The first white-space character is located in position:", x.start())
# The first white-space character is located in position: 3
```

### split

```py
import re

str = "The rain in Spain"
x = re.split("\s", str)
print(x) # ['The', 'rain', 'in', 'Spain']
```

```py
import re

str = "The rain in Spain"
x = re.split("\s", str, 1) # maxsplit
print(x) # ['The', 'rain in Spain']
```

### sub

```py
import re

str = "The rain in Spain"
x = re.sub("\s", "9", str)
print(x) # The9rain9in9Spain
```

```py
import re

str = "The rain in Spain"
x = re.sub("\s", "9", str, 2)
print(x) # The9rain9in Spain
```

### Match Object

* an object containing information about the search and the result
  * `.span()` returns a tuple containing the start-, and end positions of the match.
  * `.string` returns the string passed into the function
  * `.group()` returns the part of the string where there was a match

```py
import re

str = "The rain in Spain"
x = re.search(r"\bS\w+", str)
print(x.span()) # (12, 17)
print(x.string) # The rain in Spain
print(x.group()) # Spain
```

## PIP

* PIP is a package manager for Python packages, or modules if you like.

```sh
pip install camelcase
pip unistall camelcase
pip list # list all the packages installed on your system
```

## Try Except

* The `try` block lets you test a block of code for errors.
* The `except` block lets you handle the error.
* The `finally` block lets you execute code, regardless of the result of the try- and except blocks.

```py
try:
  print(x)
except:
  print("An exception occurred") # may x not defined
```

```py
try:
  print(x)
except NameError:
  print("Variable x is not defined")
except:
  print("Something else went wrong")
```

```py
try:
  print("Hello")
except:
  print("Something went wrong")
else:
  print("Nothing went wrong")
```

```py
try:
  print(x)
except:
  print("Something went wrong")
finally:
  print("The 'try except' is finished")
```

```py
try:
  f = open("demofile.txt")
  f.write("Lorum Ipsum")
except:
  print("Something went wrong when writing to the file")
finally:
  f.close()
```

## File

* `r` - Read - Default value. Opens a file for reading, error if the file does not exist
* `a` - Append - Opens a file for appending, creates the file if it does not exist
* `w` - Write - Opens a file for writing, creates the file if it does not exist
* `x` - Create - Creates the specified file, returns an error if the file exists

* `t` - Text - Default value. Text mode
* `b` - Binary - Binary mode (e.g. images)

```py
f = open("demofile.txt") # open a file for reading equel to
f = open("demofile.txt", "rt")
```

```py
f = open("demofile.txt", "r")
print(f.read()) # returns the whole text
print(f.read(5)) # how many character you want
print(f.readline()) # read the first lines:
```

```py
f = open("demofile.txt", "r")
for x in f: # Loop through the file line by line
  print(x)
```

```py
f = open("demofile.txt", "w") # w" method will overwrite the entire file.
f.write("Woops! I have deleted the content!")
```

```py
f = open("myfile.txt", "x") # Create a file called "myfile.txt"
```

### Delete a File

```py
import os
os.remove("demofile.txt")
```

### Check if File exist

```py
import os
if os.path.exists("demofile.txt"):
  os.remove("demofile.txt")
else:
  print("The file does not exist")
```

### Delete Folder

```py
import os
os.rmdir("myfolder")
```

## MySQL

* download and install [MySql](https://www.mysql.com/downloads/.)
* use `MySQL Connector` to connent to mysql database

```sh
# Download and install "MySQL Connector"
python -m pip install mysql-connector
```

```py
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  passwd="yourpassword"
)

print(mydb)

mycursor = mydb.cursor()

mycursor.execute("CREATE DATABASE mydatabase") # create data base

mycursor.execute("SHOW DATABASES")

for x in mycursor:
  print(x) # Return a list of your system's databases
```

```py
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  passwd="yourpassword",
  database="mydatabase"
) # connect to database "mydatabase"

mycursor = mydb.cursor()

mycursor.execute("CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))")

mycursor.execute("CREATE TABLE customers (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), address VARCHAR(255))")

mycursor.execute("ALTER TABLE customers ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY")

mycursor.execute("SHOW TABLES")

for x in mycursor:
  print(x)

# Insert Into Table
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("John", "Highway 21")
mycursor.execute(sql, val)

mydb.commit()

# Insert Multiple Rows
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = [
  ('Peter', 'Lowstreet 4'),
  ('Amy', 'Apple st 652'),
  ('Hannah', 'Mountain 21'),
]

mycursor.executemany(sql, val)

mydb.commit()

# Get Inserted ID
print("1 record inserted, ID:", mycursor.lastrowid)

# Select From a Table
mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Selecting Columns
mycursor.execute("SELECT name, address FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# fetchone() method will return the first row of the result
mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchone()

print(myresult)

# Select With a Filter
sql = "SELECT * FROM customers WHERE address ='Park Lane 38'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Wildcard Characters %
sql = "SELECT * FROM customers WHERE address LIKE '%way%'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Prevent SQL Injection %s
sql = "SELECT * FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )

mycursor.execute(sql, adr)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Order By
sql = "SELECT * FROM customers ORDER BY name" # ORDER BY name DESC

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Delete Record
sql = "DELETE FROM customers WHERE address = 'Mountain 21'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")

# Delete a Table
sql = "DROP TABLE customers" # "DROP TABLE IF EXISTS customers"

mycursor.execute(sql)

# Update Table
sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")

# Limit
mycursor.execute("SELECT * FROM customers LIMIT 5") # LIMIT 5 OFFSET 2

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

# Join
sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  INNER JOIN products ON users.fav = products.id"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

## MongoDB

* MongoDB stores data in JSON-like documents, which makes the database very flexible and scalable.
* download a free [MongoDB](https://www.mongodb.com/)
* use `PyMongo` to connent to Mongo database

```sh
# Download and install "PyMongo"
python -m pip install pymongo
```

```py
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

mydb = myclient["mydatabase"] # In MongoDB, a database is not created until it gets content!

# list of your system's databases
print(myclient.list_database_names())

# Creating a Collection
mycol = mydb["customers"] # a collection is not created until it gets content!

print(mydb.list_collection_names())

# Insert Into Collection
mydict = { "name": "John", "address": "Highway 37" }

x = mycol.insert_one(mydict)

print(x.inserted_id)

# Insert Multiple Documents
mylist = [
  { "name": "Amy", "address": "Apple st 652"},
  { "name": "Hannah", "address": "Mountain 21"},
  { "name": "Michael", "address": "Valley 345"},
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)

# Insert Multiple Documents, with Specified IDs
mylist = [
  { "_id": 1, "name": "John", "address": "Highway 37"},
  { "_id": 2, "name": "Peter", "address": "Lowstreet 27"},
  { "_id": 3, "name": "Amy", "address": "Apple st 652"},
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)

# Find
x = mycol.find_one() # returns the first occurrence in the selection.
print(x)

# find all
for x in mycol.find():
  print(x)

# Only Some Fields, 1 include , 0 exclude
for x in mycol.find({},{ "_id": 0, "name": 1, "address": 1 }):
  print(x)

# Filter the Result
myquery = { "address": "Park Lane 38" }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)

# Advanced Query
myquery = { "address": { "$gt": "S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)

# Filter With Regular Expressions
myquery = { "address": { "$regex": "^S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)

# sort
mydoc = mycol.find().sort("name") # sort("name", 1)=>ascending & sort("name", -1)=>descending

for x in mydoc:
  print(x)

# delete
myquery = { "address": "Mountain 21" }

mycol.delete_one(myquery)

# Delete Many Documents
myquery = { "address": {"$regex": "^S"} }

x = mycol.delete_many(myquery)

print(x.deleted_count, " documents deleted.")

# Delete All Documents in a Collection
x = mycol.delete_many({})

print(x.deleted_count, " documents deleted.")

# Delete Collection
mycol.drop()

# Update Collection
myquery = { "address": "Valley 345" }
newvalues = { "$set": { "address": "Canyon 123" } }

mycol.update_one(myquery, newvalues)

#print "customers" after the update:
for x in mycol.find():
  print(x)

# Update Many
myquery = { "address": { "$regex": "^S" } }
newvalues = { "$set": { "name": "Minnie" } }

x = mycol.update_many(myquery, newvalues)

print(x.modified_count, "documents updated.")

# Limit
myresult = mycol.find().limit(5)

#print the result:
for x in myresult:
  print(x)
```

## How to Remove Duplicates From a Python List

```py
mylist = list(dict.fromkeys(mylist))
```