# Java

- To check if you have Java installed on a Windows PC `java -version`

## Output

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

## Comment

- Single-line comments start with two forward slashes `//`

## Variables

- `String` - stores text, such as "Hello". String values are surrounded by double quotes.
- `int`, `byte`, `short`, `long` - stores integers (whole numbers), without decimals, such as 123 or -123.
- `float`, `double` - stores floating point numbers, with decimals, such as 19.99 or -19.99.
- `char` - stores single characters, such as 'a' or 'B'. Char values are surrounded by single quotes.
- `boolean` - stores values with two states: true or false.

```java
String name = "John";
System.out.println("Hello " + name);
```

- A String in Java is actually a non-primitive data type, because it refers to an object. The String object has methods that are used to perform certain operations on strings.
- Primitive types are predefined (already defined) in Java. Non-primitive types are created by the programmer and is not defined by Java (except for String).
- A primitive type has always a value, while non-primitive types can be null.
- A primitive type starts with a lowercase letter, while non-primitive types starts with an uppercase letter.
- The size of a primitive type depends on the data type, while non-primitive types have all the same size.

## Type Casting

- Widening Casting (automatically) - converting a smaller type to a larger type size
  - byte -> short -> char -> int -> long -> float -> double

- Narrowing Casting (manually) - converting a larger type to a smaller size type
  - double -> float -> long -> int -> char -> short -> byte

```java
int myInt = 9;
double myDouble = myInt; // Automatic casting: int to double

double myDouble = 9.78d;
int myInt = (int) myDouble; // Manual casting: double to int
```

## Operators

- Arithmetic operators: `+`, `-`, `*`, `/`, `%`, `++`, `--`.
- Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `>>=`, `<<=`.
- Comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`.
- Logical operators: `&&`, `||`, `!`.
- Bitwise operators

## Strings

```java
String txt = "Hello World";
txt.length();
txt.toUpperCase();
txt.toLowerCase();
txt.indexOf("locate");

String firstName = "John ";
String lastName = "Doe";
firstName.concat(lastName); // = firstName + " " + lastName

String x = "10";
int y = 20;
String z = x + y;  // z will be 1020 (a String)
```

### Special Characters

`\'` -> `'`
`\"` -> `"`
`\\` -> `\`
`\n` -> New Line
`\r` -> Carriage Return
`\t` -> Tab
`\b` -> Backspace
`\f` -> Form Feed

## Math

```java
Math.max(5, 10);
Math.min(5, 10);
Math.sqrt(64);
```

## If ... Else

```java
if (condition) {
  // block of code to be executed if the condition is true
}

if (condition) {
  // block of code to be executed if the condition is true
} else {
  // block of code to be executed if the condition is false
}

if (condition1) {
  // block of code to be executed if condition1 is true
} else if (condition2) {
  // block of code to be executed if the condition1 is false and condition2 is true
} else {
  // block of code to be executed if the condition1 is false and condition2 is false
}

variable = (condition) ? expressionTrue :  expressionFalse;
```

## Switch

```java
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

## While

```java
while (condition) {
  // code block to be executed
}
```

## For Loop

```java
for (int i = 0; i < 5; i++) {
  System.out.println(i);
}
```

### For Each Loop

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String i : cars) {
  System.out.println(i);
}
```

## Break / Continue

```java
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    break;
  }
  System.out.println(i);
}
```

```java
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    continue;
  }
  System.out.println(i);
}
```

## Arrays

```java
String[] cars;

String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

int[] myNum = {10, 20, 30, 40};

System.out.println(cars[0]);
cars[0] = "Opel";

System.out.println(cars.length);
```

### Multi-Dimensional

```java
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
```

## Methods

- A method is a block of code which only runs when it is called.

```java
public class Main {
  static void myMethod() {
    // code to be executed
  }
}
```

- `myMethod()` is the name of the method
- `static` means that the method belongs to the Main class and not an object of the Main class. You will learn more about objects and how to access methods through objects later in this tutorial.
- `void` means that this method does not have a return value.

### Method Overloading

```java
int myMethod(int x)
float myMethod(float x)
double myMethod(double x, double y)
```

## Modifiers

### Access Modifiers

- for `class`:
  - `public`: The class is accessible by any other class
  - default: The class is only accessible by classes in the same package.
- For `attributes`, `methods` and `constructors`:
  - `public`: The code is accessible for all classes.
  - `private`: The code is only accessible within the declared class.
  - default: The code is only accessible in the same package. This is used when you don't specify a modifier.
  - `protected`: The code is accessible in the same package and subclasses.

### Non-Access Modifiers

- for `class`:
  - `final`: The class cannot be inherited by other classes.
  - `abstract`: The class cannot be used to create objects.
- For `attributes` and `methods`:
  - `final`: Attributes and methods cannot be overridden/modified.
  - `static`: Attributes and methods belongs to the class, rather than an object.
  - `abstract`: Can only be used in an abstract class, and can only be used on methods. The method does not have a body, for example abstract void run();. The body is provided by the subclass (inherited from).
  - `transient`: Attributes and methods are skipped when serializing the object containing them.
  - `synchronized`: Methods can only be accessed by one thread at a time.
  - `volatile`: The value of an attribute is not cached thread-locally, and is always read from the "main memory".

## Encapsulation

- The meaning of Encapsulation, is to make sure that "sensitive" data is hidden from users.

```java
public class Person {
  private String name; // private = restricted access

  // Getter
  public String getName() {
    return name;
  }

  // Setter
  public void setName(String newName) {
    this.name = newName;
  }
}
```

## Packages

### Built-in Packages

```java
import java.util.Scanner;   // Import a single class
import java.util.*;  // Import the whole package
```

```java
import java.util.Scanner;

class MyClass {
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);
    System.out.println("Enter username");

    String userName = myObj.nextLine();
    System.out.println("Username is: " + userName);
  }
}
```

### Import a Package

```java
package mypack;
class MyPackageClass {
  public static void main(String[] args) {
    System.out.println("This is my package!");
  }
}
```

- compile file: `javac MyPackageClass.java`
- compile the package: `javac -d . MyPackageClass.java`. This forces the compiler to create the "mypack" package. The `-d` keyword specifies the destination.
- run package: `java mypack.MyPackageClass` -> `This is my package!`.

## Inheritance

- `subclass` (child) - the class that inherits from another class
- `superclass` (parent) - the class being inherited from

```java
class Vehicle {
  protected String brand = "Ford";        // Vehicle attribute
  public void honk() {                    // Vehicle method
    System.out.println("Tuut, tuut!");
  }
}

class Car extends Vehicle {
  private String modelName = "Mustang";    // Car attribute
  public static void main(String[] args) {

    // Create a myCar object
    Car myCar = new Car();

    // Call the honk() method (from the Vehicle class) on the myCar object
    myCar.honk();

    // Display the value of the brand attribute (from the Vehicle class) and the value of the modelName from the Car class
    System.out.println(myCar.brand + " " + myCar.modelName);
  }
}
```

## Polymorphism

- Polymorphism means "many forms".

```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}
```

## Inner Classes

```java
class OuterClass {
  int x = 10;

  class InnerClass {
    int y = 5;
  }
}

public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);
  }
}

// Outputs 15 (5 + 10)
```

## Abstraction

- Data abstraction is the process of hiding certain details and showing only essential information to the user.
- `Abstract class`: is a restricted class that cannot be used to create objects (to access it, it must be inherited from another class).
- `Abstract method`: can only be used in an abstract class, and it does not have a body. The body is provided by the subclass (inherited from).

```java
// Abstract class
abstract class Animal {
  // Abstract method (does not have a body)
  public abstract void animalSound();
  // Regular method
  public void sleep() {
    System.out.println("Zzz");
  }
}

// Subclass (inherit from Animal)
class Pig extends Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig(); // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

## Interfaces

- An interface is a completely "abstract class" that is used to group related methods with empty bodies.
- Interface methods are by default `abstract` and `public`
- Interface attributes are by default `public`, `static` and `final`
- An interface cannot contain a constructor (as it cannot be used to create objects)

```java
// Interface
interface Animal {
  public void animalSound(); // interface method (does not have a body)
  public void sleep(); // interface method (does not have a body)
}

// Pig "implements" the Animal interface
class Pig implements Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
  public void sleep() {
    // The body of sleep() is provided here
    System.out.println("Zzz");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig();  // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

## Enums

- An enum is a special "class" that represents a group of constants.

```java
enum Level {
  LOW,
  MEDIUM,
  HIGH
}
```

```java
Level myVar = Level.MEDIUM; 
System.out.println(myVar); // MEDIUM
```

## Dates

- `LocalDate`: Represents a date (year, month, day (yyyy-MM-dd))
- `LocalTime`: Represents a time (hour, minute, second and nanoseconds (HH-mm-ss-ns))
- `LocalDateTime`: Represents both a date and a time (yyyy-MM-dd-HH-mm-ss-ns)
- `DateTimeFormatter`: Formatter for displaying and parsing date-time objects

## ArrayList

- The ArrayList class is a resizable array.
- The ArrayList class has a regular array inside it. When an element is added, it is placed into the array. If the array is not big enough, a new, larger array is created to replace the old one and the old one is removed.

```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    System.out.println(cars);
  }
}
```

## LinkedList

- The LinkedList stores its items in "containers." The list has a link to the first container and each container has a link to the next container in the list. To add an element to the list, the element is placed into a new container and that container is linked to one of the other containers in the list.
- Use an `ArrayList` for storing and accessing data, and `LinkedList` to manipulate data.

```java
// Import the LinkedList class
import java.util.LinkedList;

public class Main {
  public static void main(String[] args) {
    LinkedList<String> cars = new LinkedList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    System.out.println(cars);
  }
}
```

- addFirst(): Adds an item to the beginning of the list.
- addLast(): Add an item to the end of the list.
- removeFirst(): Remove an item from the beginning of the list.
- removeLast(): Remove an item from the end of the list.
- getFirst(): Get the item at the beginning of the list.
- getLast(): Get the item at the end of the list.

## HashMap

- A HashMap however, store items in "key/value" pairs

```java
import java.util.HashMap;

public class Main {
  public static void main(String[] args) {
    // Create a HashMap object called capitalCities
    HashMap<String, String> capitalCities = new HashMap<String, String>();

    // Add keys and values (Country, City)
    capitalCities.put("England", "London");
    capitalCities.put("Germany", "Berlin");
    capitalCities.put("Norway", "Oslo");
    capitalCities.put("USA", "Washington DC");
    System.out.println(capitalCities);
  }
}
```

```java
capitalCities.get("England");

capitalCities.remove("England");

capitalCities.clear(); // To remove all items
```

## HashSet

- A HashSet is a collection of items where every item is unique.

```java
// Import the HashSet class
import java.util.HashSet;

public class Main {
  public static void main(String[] args) {
    HashSet<String> cars = new HashSet<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("BMW");
    cars.add("Mazda");
    System.out.println(cars);
  }
}
```

```java
cars.contains("Mazda"); // Check If an Item Exists

cars.remove("Volvo");

cars.clear(); // To remove all items
```

## Iterator

- An Iterator is an object that can be used to loop through collections.

```java
// Import the ArrayList class and the Iterator class
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {

    // Make a collection
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");

    // Get the iterator
    Iterator<String> it = cars.iterator();

    // Print the first item
    System.out.println(it.next());

    // Looping Through a Collection
    while(it.hasNext()) {
        System.out.println(it.next());
    }
  }
}
```

```java
// Removing Items from a Collection
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(12);
    numbers.add(8);
    numbers.add(2);
    numbers.add(23);
    Iterator<Integer> it = numbers.iterator();
    while(it.hasNext()) {
      Integer i = it.next();
      if(i < 10) {
        it.remove();
      }
    }
    System.out.println(numbers);
  }
}
```

## Wrapper Classes

- Wrapper classes provide a way to use primitive data types (int, boolean, etc..) as objects.

- byte -> Byte
- short -> Short
- int -> Integer
- long -> Long
- float -> Float
- double -> Double
- boolean -> Boolean
- char -> Character

```java
ArrayList<int> myNumbers = new ArrayList<int>(); // Invalid
ArrayList<Integer> myNumbers = new ArrayList<Integer>(); // Valid
```

### Creating Wrapper Objects

```java
public class Main {
  public static void main(String[] args) {
    Integer myInt = 5;
    Double myDouble = 5.99;
    Character myChar = 'A';
    System.out.println(myInt.intValue()); // same as System.out.println(myInt);
    System.out.println(myDouble.doubleValue());
    System.out.println(myChar.charValue());
  }
}
```

## Exceptions

```java
try {
  //  Block of code to try
}
catch(Exception e) {
  //  Block of code to handle errors
}
```

```java
public class Main {
  public static void main(String[] args) {
    try {
      int[] myNumbers = {1, 2, 3};
      System.out.println(myNumbers[10]);
    } catch (Exception e) {
      System.out.println("Something went wrong.");
    } finally {
      System.out.println("The 'try catch' is finished.");
    }
  }
}
```

## Regular Expressions

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Main {
  public static void main(String[] args) {
    Pattern pattern = Pattern.compile("w3schools", Pattern.CASE_INSENSITIVE);
    Matcher matcher = pattern.matcher("Visit W3Schools!");
    boolean matchFound = matcher.find();
    if(matchFound) {
      System.out.println("Match found");
    } else {
      System.out.println("Match not found");
    }
  }
}
// Outputs Match found
```

[abc] -> Find one character from the options between the brackets
[^abc] -> Find one character NOT between the brackets
[0-9] -> Find one character from the range 0 to 9

### Meta characters

- `|` -> Find a match for any one of the patterns separated by | as in: cat|dog|fish
- `.` -> Find just one instance of any character
- `^` -> Finds a match as the beginning of a string as in: ^Hello
- `$` -> Finds a match at the end of the string as in: World$
- `\d` -> Find a digit
- `\s` -> Find a whitespace character
- `\b` -> Find a match at the beginning of a word like this: \bWORD, or at the end of a word like this: WORD\b
- `\uxxxx` -> Find the Unicode character specified by the hexadecimal number xxxx

### Quantifiers

- `n+` -> Matches any string that contains at least one n
- `n*` -> Matches any string that contains zero or more occurrences of n
- `n?` -> Matches any string that contains zero or one occurrences of n
- `n{x}` -> Matches any string that contains a sequence of X n's
- `n{x,y}` -> Matches any string that contains a sequence of X to Y n's
- `n{x,}` -> Matches any string that contains a sequence of at least X n's

### Threads

- Threads allows a program to operate more efficiently by doing multiple things at the same time.

### Creating a Thread

- 2 way: `Thread` or `Runnable`

- It can be created by extending the Thread class and overriding its run() method:

```java
public class Main extends Thread {
  public static void main(String[] args) {
    Main thread = new Main();
    thread.start();
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

- Another way to create a thread is to implement the Runnable interface:

```java
public class Main implements Runnable {
  public static void main(String[] args) {
    Main obj = new Main();
    Thread thread = new Thread(obj);
    thread.start();
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

- The major difference is that when a class extends the Thread class, you cannot extend any other class, but by implementing the Runnable interface, it is possible to extend from another class as well, like: `class MyClass extends OtherClass implements Runnable`.

### Concurrency Problems

- Because threads run at the same time as other parts of the program, there is no way to know in which order the code will run. When the threads and main program are reading and writing the same variables, the values are unpredictable.
- To avoid concurrency problems, it is best to share as few attributes between threads as possible. If attributes need to be shared, one possible solution is to use the isAlive() method of the thread to check whether the thread has finished running before using any attributes that the thread can change.

```java
public class Main extends Thread {
  public static int amount = 0;

  public static void main(String[] args) {
    Main thread = new Main();
    thread.start();
    // Wait for the thread to finish
    while(thread.isAlive()) {
    System.out.println("Waiting...");
  }
  // Update amount and print its value
  System.out.println("Main: " + amount);
  amount++;
  System.out.println("Main: " + amount);
  }
  public void run() {
    amount++;
  }
}
```

## Lambda

```java
parameter -> expression

(parameter1, parameter2) -> expression

(parameter1, parameter2) -> { code block }
```

## Reference

- learn from lovely [W3Schools](https://www.w3schools.com/java/).
