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
print(a.strip()) # returns "Hello, World!"
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

x = "False"
if x:
    print("x is True or have none zero value") # its run
else
    print("x is False or zero or None or empty string or empty list or empty tuple or empty mapping , ...")

print(not False) # return True
print(not True) # return False
# if not(age<18)
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

## Text File 061

```py
jabber=open("text.txt")
for line in jabber:
    print("line")
jabber.close()
```