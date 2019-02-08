# Lisp

* John McCarthy invented LISP in 1958.

## Environment

* Text Editor: vi, notpad, 
* `.lisp` file.
* The Lisp Executer: CLIPS

* linux & mac: sbcl,Quicklisp,Emacs and SLIME => run emacs, alt-x slime
* windows: lipstick

## Program Structure

* LISP expressions are called symbolic expressions or s-expressions.
* The s-expressions are composed of three valid objects, `atoms`, `lists` and `strings`.
  * `atom` is a number or string of contiguous characters. It includes numbers and special characters.
  * `list` is a sequence of atoms and/or other lists enclosed in parentheses.
  * `string` is a group of characters enclosed in double quotation marks.
* The basic numeric operations in LISP are +, -, *, and /
* LISP represents a function call f(x) as (f x), for example cos(45) is written as cos 45
* LISP expressions are case-insensitive, cos 45 or COS 45 are same.
* LISP tries to evaluate everything, including the arguments of a function. Only three types of elements are constants and always return their own value:
  * Numbers
  * The letter `t`, that stands for logical true.
  * The value `nil`, that stands for logical false, as well as an empty list.
* LISP programs run either on an interpreter or as compiled code.
* Atoms can be numbers like 10, 3.14, or symbols like t (the truth constant), +, my-variable. There’s also a special kind of symbol called keywords, which are colon-prefixed symbols like :thing or :keyword. Keywords evaluate to themselves: you can think of them sort of like enums.

## Hello World

```lisp
(write-line "Hello World")
(format t "Hello, world!")
```

## Comment

```lisp
;; Single line comments start with a semicolon, and can start at any point in the line
#|
  This is a multi-line comment.

  #|
    They can be nested!
  |#
|#
```

## Prefix Notation

* In prefix notation, operators are written before their operands.

```lisp
(/ (* a (+ b c) ) d)         ;; => a * ( b + c ) / d
(write(+ (* (/ 9 5) 60) 32)) ;; =>(60 * 9 / 5) + 32
```

## Data Types

* Scalar types − for example, number types, characters, symbols etc.
* Data structures − for example, lists, vectors, bit-vectors, and strings.

* `type-of` function returns the data type of a given object.

```lisp
(setq x 10)
(setq y 34.567)
(setq ch nil)
(setq n 123.78)
(setq bg 11.0e+4)
(setq r 124/2)

(print x)
(print y)
(print n)
(print ch)
(print bg)
(print r)

(print (type-of x))
```

## Decision Making

### cond

```lisp
(setq a 10)
(cond ((> a 20)
   (format t "~% a is greater than 20"))
   (t (format t "~% value of a is ~d " a)))
;; value of a is 10
```

### if

```lisp
(setq a 10)
(if (> a 20)
   (format t "~% a is less than 20"))
(format t "~% value of a is ~d " a)
;; value of a is 10

(setq a 10)
(if (> a 20)
   then (format t "~% a is less than 20"))
(format t "~% value of a is ~d " a)
;; a is less than 20
;; value of a is 10

(setq a 100)
(if (> a 20)
   (format t "~% a is greater than 20") 
   (format t "~% a is less than 20"))
(format t "~% value of a is ~d " a)
;; a is greater than 20
;; value of a is 100 
```

### when

```lisp
(setq a 100)
(when (> a 20)
   (format t "~% a is greater than 20"))
(format t "~% value of a is ~d " a)
;; a is greater than 20
;; value of a is 100 
```

### case

```lisp
(setq day 4)
(case day
(1 (format t "~% Monday"))
(2 (format t "~% Tuesday"))
(3 (format t "~% Wednesday"))
(4 (format t "~% Thursday"))
(5 (format t "~% Friday"))
(6 (format t "~% Saturday"))
(7 (format t "~% Sunday")))
;; Thursday
```

## Loops

### loop

```lisp
(setq a 10)
(loop 
   (setq a (+ a 1))
   (write a)
   (terpri)
   (when (> a 15) (return a))
)
;; 11
;; 12
;; 13
;; 14
;; 15
;; 16
```

### loop for

```lisp
(loop for x in '(tom dick harry)
   do (format t " ~s" x)
)
;; TOM DICK HARRY

(loop for a from 10 to 15
   do (print a)
)
;; 10 
;; 11 
;; 12 
;; 13 
;; 14 
;; 15 

(loop for x from 1 to 10
   if(evenp x)
   do (print x)
)
;; 2 
;; 4 
;; 6 
;; 8 
;; 10
```

### do

```lisp
(do ((x 0 (+ 2 x)) ;; (variable1    value1   updated-value1)
   (y 20 ( - y 2)))
   ((= x y)(- x y))
   (format t "~% x = ~d  y = ~d" x y)
)
;; x = 0  y = 20
;; x = 2  y = 18
;; x = 4  y = 16
;; x = 6  y = 14
;; x = 8  y = 12
```

### dotimes

```lisp
(dotimes (n 11)
   (print n) (prin1 (* n n))
)
;; 0 0
;; 1 1
;; 2 4
;; 3 9
;; 4 16
;; 5 25
;; 6 36
;; 7 49
;; 8 64
;; 9 81
;; 10 100
```

### dolist

```lisp
(dolist (n '(1 2 3 4 5 6 7 8 9))
   (format t "~% Number: ~d Square: ~d" n (* n n))
)
;; Number: 1 Square: 1
;; Number: 2 Square: 4
;; Number: 3 Square: 9
;; Number: 4 Square: 16
;; Number: 5 Square: 25
;; Number: 6 Square: 36
;; Number: 7 Square: 49
;; Number: 8 Square: 64
;; Number: 9 Square: 81
```

## Functions

### Named Functions

define function: `(defun name (parameter-list) "Optional documentation string." body)`

```lisp
(defun fib (n)
  "Return the nth Fibonacci number."
  (if (< n 2)
      n
      (+ (fib (- n 1))
         (fib (- n 2)))))
```

use function:

```lisp
(fib 30)
```

### Anonymous Functions

#### Application

Functions can be called indirectly using funcall:

```lisp
(funcall #'fib 30)
```

Or with apply:

```lisp
(apply #'fib (list 30))
```

#### Multiple Return Values

```lisp
(defun many (n)
  (values n (* n 2) (* n 3)))
```

```lisp
(multiple-value-list (many 2)) ;; (2 4 6)
(nth-value 1 (many 2)) ;; 4
```

We can also use multiple-value-bind to assign each return value to a variable:

```lisp
(multiple-value-bind (first second third)
    (many 2)
  (list first second third)) ;; (2 4 6)
```

## Variables

### Local Variables

```lisp
(let ((str "Hello, world!"))
  (string-upcase str))       ;; => "HELLO, WORLD!"
```

```lisp
(let ((x 1)
      (y 5))
  (+ x y))   ;; => 6
```

* To define variables whose initial values depend on previous variables in the same form, use let*:

```lisp
(let* ((x 1)
       (y (+ x 1)))
  y)                ;; => 2

```

```lisp
(setq x 100)
(setq y 200)
(format t "x = ~2d y = ~2d" x y)
;; x = 100 y = 200

(let ((x 'a) (y 'b)(z 'c))
(format t "x = ~a y = ~a z = ~a" x y z))
;; x = A y = B z = C

(prog ((x '(a b c))(y '(1 2 3))(z '(p q 10)))
(format t "x = ~a y = ~a z = ~a" x y z))
;; x = (A B C) y = (1 2 3) z = (P Q 10)
```

### Dynamic Variables

* Dynamic variables are sort of like global variables, but more useful: they are dynamically scoped. You define them either with `defvar` or `defparameter`, the differences being:
    * `defparameter` requires an initial value, `defvar` does not.
    * `defparameter` variables are changed when code is reloaded with a new initial value, `defvar` variables are not.

```lisp
(defparameter *string* "I'm global")

(defun print-variable ()
  (print *string*))

(print-variable) ;; Prints "I'm global"

(let ((*string* "I have dynamic extent")) ;; Binds *string* to a new value
  (print-variable)) ;; Prints "I have dynamic extent"
;; The old value is restored

(print-variable) ;; Prints "I'm global"
```

* when you redefine the value of a dynamic variable using let, the variable is bound to the new value inside the body of the let, and the old value is ‘restored’ afterwards.

### Constants

```lisp
(defconstant PI 3.141592)
(defun area-circle(rad)
   (terpri)
   (format t "Radius: ~5f" rad)
   (format t "~%Area: ~10f" (* PI rad rad)))
(area-circle 10)
```

## Operators

### Arithmetic Operations

```lisp
(+A B) ;; A+B
(- A B) ;; A-B
(* A B) ;; A*B
(/ B A) ;; A/B
(mod B A ) ;; A%B
(incf A 3) ;; A+=3
(decf A 4) ;; A-=4
```

### Comparison Operations

```lisp
(= A B)
(/= A B)
(> A B)
(< A B)
(>= A B)
(<= A B)
(max A B)
(min A B) 
```

### Logical Operations

```lisp
(and A B)
(or A B)
(not A) 
```

### Bitwise Operations

```lisp
(logand a b) ;; AND
(logior a b) ;; INCLUSIVE OR
(logxor a b) ;; EXCLUSIVE OR
(lognor a b) ;; NOT
(logeqv a b) ;; EQUIVALENCE or exclusive nor
```


## List

### Basic

```lisp
(list 1 2 3) ;;(1 2 3)
```

* can use `first`, `second` ... `tenth` or `nth` function

```lisp
(first (list 1 2 3)) ;; 1
```

* change member

```lisp
(defparameter my-list (list 1 2 3)) ;; MY-LIST
(setf (second my-list) 7) ;; 7
my-list ;; (1 7 3)
```

```lisp
(defparameter my-list (list 1 2 3)) ;; MY-LIST
(setf (nth 1 my-list) 65) ;; 65
my-list ;; (1 65 3)
```

### Map

```lisp
(mapcar #'evenp (list 1 2 3 4 5 6)) ;; (NIL T NIL T NIL T)
;; equel to
(list (evenp 1) (evenp 2) (evenp 3) (evenp 4) (evenp 5) (evenp 6))  ;; (NIL T NIL T NIL T)
```

```lisp
(mapcar #'string-upcase (list "Hello" "world!")) ;; ("HELLO" "WORLD!")
```

### Reduce

```lisp
(reduce #'+ (list 1 2 3)) ;; 6
(reduce #'(lambda (a b)
                     (* a b))
                 (list 10 20 30)) ;; 6000
```

### Sorting

```lisp
(sort (list 9 2 4 7 3 0 8) #'<) ;; (0 2 3 4 7 8 9)
```

### Destructuring

```lisp
(defun destructure (list)
  (destructuring-bind (first second &rest others)
    list
    (format t "First: ~A~%" first)
    (format t "Second: ~A~%" second)
    (format t "Rest: ~A~%" others)))

(destructure (list 1 2 3 4 5 6))
;; First: 1
;; Second: 2
;; Rest: (3 4 5 6)
;; NIL
```

## File I/O

* write in file

```lisp
(with-open-file (stream (merge-pathnames #p"data.txt"
                                         (user-homedir-pathname))
                        :direction :output    ;; Write to disk
                        :if-exists :supersede ;; Overwrite the file
                        :if-does-not-exist :create)
  (dotimes (i 100)
    ;; Write random numbers to the file
    (format stream "~3,3f~%" (random 100))))
```

* read file

```lisp
(uiop:read-file-string (merge-pathnames #p"data.txt"
                        (user-homedir-pathame)))
```

## Macro

* Common Lisp has no while loop, can use this macro instead of while

```lisp
(defmacro while (condition &body body)
  `(loop while ,condition do (progn ,@body)))
;; use
(while (some-condition)
  (do-something)
  (do-something-else))
```

## Object Orientation

### Generic Functions and Methods

```lisp
;; define generic function
(defgeneric description (object)
  (:documentation "Return a description of an object."))

;; efine methods of that function
(defmethod description ((object integer))
  (format nil "The integer ~D" object))

(defmethod description ((object float))
  (format nil "The float ~3,3f" object))

;; use
(description 10) ;; "The integer 10"
(description 3.14) ;; "The float 3.140"
```

## Classes

```lisp
(defclass vehicle ()
  ((speed :accessor vehicle-speed
          :initarg :speed
          :type real
	      :documentation "The vehicle's current speed."))
  (:documentation "The base class of vehicles."))

```

```lisp
(defclass bicycle (vehicle)
  ((mass :reader bicycle-mass
         :initarg :mass
         :type real
         :documentation "The bike's mass."))
  (:documentation "A bicycle."))

(defclass canoe (vehicle)
  ((rowers :reader canoe-rowers
           :initarg :rowers
           :initform 0
           :type (integer 0)
           :documentation "The number of rowers."))
  (:documentation "A canoe."))

;; use
(defparameter canoe (make-instance 'canoe :speed 10 :rowers 6)) ;; CANOE
(class-of canoe) ;; 
#<STANDARD-CLASS COMMON-LISP-USER::CANOE>
(canoe-rowers canoe) ;; 6
(vehicle-speed canoe) ;; 10
(describe 'canoe) ;; ......
```

## Refrences

* [lisp-lang.org](https://lisp-lang.org/)
* [jonathanfischer.net](http://www.jonathanfischer.net/modern-common-lisp-on-linux/)
* [tutorialspoint](https://www.tutorialspoint.com/lisp/lisp_program_structure.htm)