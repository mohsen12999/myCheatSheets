# Python

* use Anaconda for having package of python library and editor like jupiter and spider. add to path when install anaconda.

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
print("day" in today) # return true
print("parrot" in "bird") # return false
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

x = "false"
if x:
    print("x is true or have none zero value") # its run
else
    print("x is false or zero or None or empty string or empty list or empty tuple or empty mapping , ...")

print(not false) # return true
print(not true) # return false
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