# Erlang

## Data Types

### Terms

A piece of data of any data type

### Number

* integers / floats
* $char / base#value
  * $char: ASCII value or unicode code-point of the character
  * base#value: Integer with the base base, that must be an integer in the range 2..36.

```erl
42.     ->42
$A.     ->65
$\n.    ->10
2#101.  ->5
16#1f.  ->31
2.3.    ->2.3
2.3e3.  ->2.3e3
2.3e-3. ->0.0023
```

### Atom

* is a literal, a constant with name.
* An atom is to be enclosed in single quotes (') if it does not begin with a lower-case letter or if it contains other characters than alphanumeric characters, underscore (_), or @.

```erl
hello
phone_number
'Monday'
'phone number'
```

### Bit Strings and Binaries

* A bit string is used to store an area of untyped memory.
* Bit strings that consist of a number of bits that are evenly divisible by eight, are called binaries
