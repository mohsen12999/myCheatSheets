# Haskell

* `ghci` is an interactive mode of Huskell compiler.
* for loading Huskell file like `myfunctions.hs` in `ghci`: `:l myfunctions` and for reloading file `:l myfunctions` or `:r`.

## References

* [Learning Haskell Book](http://learnyouahaskell.com/)
* [Haskell for Imperative Programmers by Philipp Hagenlocher](https://www.youtube.com/watch?v=Vgu82wiiZ90&list=PLe7Ei6viL6jGp1Rfu0dil1JH1SHk9bgDV)
* [Introductory Haskell course of the University of Pennsylvania (CIS194)](https://www.seas.upenn.edu/~cis1940/spring13/lectures.html)

## install

* Use [`GHCup`](https://www.haskell.org/ghcup/) to install GHC, cabal-install, Stack and haskell-language-server.

## Basic

* Functional programming
  * Pure (Mathematical) Functions.
  * Immutable data.
  * No/Less side-effects.
  * Declarative.

## Function

* simple function: `succ 8` = 8+1, `min 9 10`, `max 100 101`.

Definition: `name arg1 arg2 ... argn = <expr>`.

Application: `name arg1 arg2 ... argn`.

```hs
in_range min max x =
    x >= min && x <= max

in_range 0 5 3
    => True

in_range 4 5 3
    => False
```

## Type

Basic: `name :: <type>`

```hs
x :: Integer
x = 1

y :: Bool
y = True

z :: Float
z = 3.14159
```

Functions Type

```hs
in_range :: Integer -> Integer -> Integer -> Bool
in_range min max x = x >= min && x <= max

in_range 0.5 1.5 1
    Type error

in_range 0 5 3
    Correct
```

Operator Type

```sh
ghci> :t (+)
    (+) :: Num a => a -> a -> a
```

```hs
add a b = a+b

add 10 20

10 `add` 20
```

## Let

```hs
in_range min max x =
    let in_lower_bound = min <= x
        in_upper_bound = max >= x
    in
        in_lower_bound && in_upper_bound
```

## Where

```hs
in_range min max x = ilb && iub
    where
        ilb = min <= x
        iub = max >= x
```

## If statements

```hs
doubleSmallNumber x = 
    if x > 100  
        then x  
        else x*2 
```

## Recursion

`name <args> = ... name <args'>`

```hs
fac n =
    if n <= 1 then
        1
    else
        n * fac (n-1)
```

## Guards

```hs
fac n
    | n <= 1    = 1
    | otherwise = n * fac (n-1)
```

## Pattern Matching

```hs
is_zero 0 = True
is_zero _ = False
```

## Accumulators

```hs
fac n = aux n 1
    where
        aux n acc
            | n <= 1    = acc
            | otherwise = aux (n-1) (n*acc)
```
