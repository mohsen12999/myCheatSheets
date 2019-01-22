# Lisp

* John McCarthy invented LISP in 1958.

## Environment

* Text Editor: vi, notpad.
* `.lisp` file.
* The Lisp Executer: CLIPS

## Program Structure

* LISP expressions are called symbolic expressions or s-expressions.
* The s-expressions are composed of three valid objects, `atoms`, `lists` and `strings`.
* Atoms can be numbers like 10, 3.14, or symbols like t (the truth constant), +, my-variable. There’s also a special kind of symbol called keywords, which are colon-prefixed symbols like :thing or :keyword. Keywords evaluate to themselves: you can think of them sort of like enums.
* LISP programs run either on an interpreter or as compiled code.

## Hello World

```lisp
(write-line "Hello World")
```

## Comment


## Prefix Notation

* In prefix notation, operators are written before their operands.

```lisp
(/ (* a (+ b c) ) d)         ;; => a * ( b + c ) / d
(write(+ (* (/ 9 5) 60) 32)) ;; =>(60 * 9 / 5) + 32
```


