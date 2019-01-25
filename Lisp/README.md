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
* Atoms can be numbers like 10, 3.14, or symbols like t (the truth constant), +, my-variable. There’s also a special kind of symbol called keywords, which are colon-prefixed symbols like :thing or :keyword. Keywords evaluate to themselves: you can think of them sort of like enums.
* LISP programs run either on an interpreter or as compiled code.

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

## Functions

### Named Functions

define function:

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
    many 2)
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

## Refrences

* [lisp-lang.org](https://lisp-lang.org/)
* [jonathanfischer.net](http://www.jonathanfischer.net/modern-common-lisp-on-linux/)
* [tutorialspoint](https://www.tutorialspoint.com/lisp/lisp_program_structure.htm)