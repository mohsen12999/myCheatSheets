# Erlang

## Sequential Programming

### The Erlang Shell

```sh
# for run shell
erl
# Eshell V5.9.1 (abort with ^G)
# 1>
```

* for exit use `halt()`

```erl
halt().
```

### Modules and Functions

* write program file

```erl
%% tut.erl
-module(tut).
-export([double/1]).

double(X) ->
    2 * X.
```

* compile and run

```erl
%% compile tut.erl
c(tut)
%% {ok,tut}

tut:double(10).
# 20
```

```erl
-module(tut1).
-export([fac/1, mult/2]).

fac(1) ->
    1;
fac(N) ->
   N*fac(N-1).

mult(X, Y) ->
    X * Y.
```

* semicolon ";" that indicates that there is more of the function fac> to come

### Atoms

* Atoms start with a small letter

```erl
-module(tut2).
-export([convert/2]).

convert(M, inch) ->
    M / 2.54;
convert(N, centimeter) ->
    N * 2.54.
```

```erl
%% use
tut2:convert(3, inch).
%% 1.1811023622047243

tut2:convert(7, centimeter).
%% 17.78
```

### Tuples

```erl
-module(tut3).
-export([convert_length/1]).

convert_length({centimeter, X}) ->
    {inch, X / 2.54};
convert_length({inch, Y}) ->
    {centimeter, Y * 2.54}.
```

```erl
tut3:convert_length({inch, 5}).
%% {centimeter,12.7}
tut3:convert_length(tut3:convert_length({inch, 5})).
%% {inch,5.0}
```

* also valid Tuple: `{moscow, {c, -10}}`, `{cape_town, {f, 70}}`, `{paris, {f, 28}}`

### Lists

```erl
TupleList = [{moscow, {c, -10}}, {cape_town, {f, 70}}, {stockholm, {c, -4}},
{paris, {f, 28}}, {london, {f, 36}}]

[First |TheRest] = [1,2,3,4,5].
First.
%% 1
TheRest.
%% [2,3,4,5]
```

```erl
[E1, E2 | R] = [1,2,3,4,5,6,7].
E1.
%% 1
E2.
%% 2
R.
%% [3,4,5,6,7]
```

```erl
[A, B | C] = [1, 2].
A.
%% 1
B.
%% 2
C.
%% []
```

```erl
%% find the length of a list
-module(tut4).
-export([list_length/1]).

list_length([]) ->
    0;
list_length([First | Rest]) ->
    1 + list_length(Rest).
```

* Erlang does not have a string data type. Instead, strings can be represented by lists of Unicode characters.

```erl
[97,98,99].
%% "abc"
```

### Maps

* `#{ key => value }`

```erl
%% calculate alpha blending using maps to reference color and alpha channels
-module(color).
-export([blend/2, new/4]).
-define(is_channel(V),
  is_float(V) andalso V >= 0.0 andalso V =< 1.0).

new(R, G, B, A)
    when ?is_channel(R), ?is_channel(G), ?is_channel(B),
  ?is_channel(A) ->
    #{red => R, green => G, blue => B, alpha => A}.

blend(Src, Dst) -> blend(Src, Dst, alpha(Src, Dst)).

blend(Src, Dst, Alpha) when Alpha > 0.0 ->
    Dst#{red := red(Src, Dst) / Alpha,
  green := green(Src, Dst) / Alpha,
  blue := blue(Src, Dst) / Alpha, alpha := Alpha};
blend(_, Dst, _) ->
    Dst#{red := 0.0, green := 0.0, blue := 0.0,
  alpha := 0.0}.

alpha(#{alpha := SA}, #{alpha := DA}) ->
    SA + DA * (1.0 - SA).

red(#{red := SV, alpha := SA},
    #{red := DV, alpha := DA}) ->
    SV * SA + DV * DA * (1.0 - SA).

green(#{green := SV, alpha := SA},
      #{green := DV, alpha := DA}) ->
    SV * SA + DV * DA * (1.0 - SA).

blue(#{blue := SV, alpha := SA},
     #{blue := DV, alpha := DA}) ->
    SV * SA + DV * DA * (1.0 - SA).
```

* `is_channel` is defined to help with the guard tests -> `Preprocessor`

```erl
C1 = color:new(0.3,0.4,0.5,1.0).
%% #{alpha => 1.0,blue => 0.5,green => 0.4,red => 0.3}
C2 = color:new(1.0,0.8,0.1,0.3).
%% #{alpha => 0.3,blue => 0.1,green => 0.8,red => 1.0}
color:blend(C1,C2).
%% #{alpha => 1.0,blue => 0.5,green => 0.4,red => 0.3}
color:blend(C2,C1).
%% #{alpha => 1.0,blue => 0.38,green => 0.52,red => 0.51}
```

### Standard Modules and Manual Pages

* in os shell use `erl -man` -> `erl -man io`
* use site [commercial Erlang](www.erlang.se) or [open source](www.erlang.org).

### Writing Output to a Terminal

```erl
io:format("hello world~n", []).
%% hello world

io:format("this outputs one Erlang term: ~w~n", [hello]).
%% this outputs one Erlang term: hello

io:format("this outputs two Erlang terms: ~w~w~n", [hello, world]).
%% this outputs two Erlang terms: helloworld

io:format("this outputs two Erlang terms: ~w ~w~n", [hello, world]).
%% this outputs two Erlang terms: hello world
```

* format/2 -> get to list
* `~w` -> word, `~n` -> new line

```erl
-module(tut5).

-export([format_temps/1]).

%% Only this function is exported
format_temps([]) -> % No output for an empty list
    ok;
format_temps([City | Rest]) ->
    print_temp(convert_to_celsius(City)),
    format_temps(Rest).

convert_to_celsius({Name,
  {c, Temp}}) -> % No conversion needed
    {Name, {c, Temp}};
convert_to_celsius({Name,
  {f, Temp}}) -> % Do the conversion
    {Name, {c, (Temp - 32) * 5 / 9}}.

print_temp({Name, {c, Temp}}) ->
    io:format("~-15w ~w c~n", [Name, Temp]).

```

```erl
tut5:format_temps([{moscow, {c, -10}}, {cape_town, {f, 70}},
{stockholm, {c, -4}}, {paris, {f, 28}}, {london, {f, 36}}]).

%% moscow -10 c
%% cape_town 21.11111111111111 c
%% stockholm -4 c
%% paris -2.2222222222222223 c
%% london 2.2222222222222223 c
```

### Matching, Guards, and Scope of Variables

```erl
-module(tut6).
-export([list_max/1]).

list_max([Head | Rest]) -> list_max(Rest, Head).

list_max([], Res) -> Res;
list_max([Head | Rest], Result_so_far)
    when Head > Result_so_far ->
    list_max(Rest, Head);
list_max([Head | Rest], Result_so_far) ->
    list_max(Rest, Result_so_far).
```

* two functions have the same name -> different arg count and type

```erl
M = 5.
%% 5
M = 6.
%% ** exception error: no match of right hand side value 6
M = M + 1.
%% ** exception error: no match of right hand side value 6
N = M + 1.
%% 6
```

```erl
%% The | operator can be used to get the head of a list
[M1|T1] = [paris, london, rome].

%% The | operator can also be used to add a head to a list:
L1 = [madrid | T1].
```

```erl
-module(tut8).
-export([reverse/1]).

reverse(List) -> reverse(List, []).

reverse([Head | Rest], Reversed_List) ->
    reverse(Rest, [Head | Reversed_List]);
reverse([], Reversed_List) -> Reversed_List.
```

* reverse([1|2,3], []) => reverse([2,3], [1|[]])
* reverse([2|3], [1]) => reverse([3], [2|[1])
* reverse([3|[]], [2,1]) => reverse([], [3|[2,1]])
* reverse([], [3,2,1]) => [3,2,1]

```erl
-module(tut7).

-export([format_temps/1]).

format_temps(List_of_cities) ->
    Converted_List = convert_list_to_c(List_of_cities),
    print_temp(Converted_List),
    {Max_city, Min_city} = find_max_and_min(Converted_List),
    print_max_and_min(Max_city, Min_city).

convert_list_to_c([{Name, {f, Temp}} | Rest]) ->
    Converted_City = {Name, {c, (Temp - 32) * 5 / 9}},
    [Converted_City | convert_list_to_c(Rest)];
convert_list_to_c([City | Rest]) ->
    [City | convert_list_to_c(Rest)];
convert_list_to_c([]) -> [].

print_temp([{Name, {c, Temp}} | Rest]) ->
    io:format("~-15w ~w c~n", [Name, Temp]),
    print_temp(Rest);
print_temp([]) -> ok.

find_max_and_min([City | Rest]) ->
    find_max_and_min(Rest, City, City).

find_max_and_min([{Name, {c, Temp}} | Rest],
     {Max_Name, {c, Max_Temp}}, {Min_Name, {c, Min_Temp}}) ->
    if Temp > Max_Temp ->
     Max_City = {Name, {c, Temp}}; % Change
       true ->
     Max_City = {Max_Name, {c, Max_Temp}} % Unchanged
    end,
    if Temp < Min_Temp ->
     Min_City = {Name, {c, Temp}}; % Change
       true ->
     Min_City = {Min_Name, {c, Min_Temp}} % Unchanged
    end,
    find_max_and_min(Rest, Max_City, Min_City);
find_max_and_min([], Max_City, Min_City) ->
    {Max_City, Min_City}.

print_max_and_min({Max_name, {c, Max_temp}},
      {Min_name, {c, Min_temp}}) ->
    io:format("Max temperature was ~w c in ~w~n",
        [Max_temp, Max_name]),
    io:format("Min temperature was ~w c in ~w~n",
        [Min_temp, Min_name]).
```

### If and Case

```erl
-module(tut9).
-export([test_if/2]).

test_if(A, B) ->
    if A == 5 -> io:format("A == 5~n", []), a_equals_5;
       B == 6 -> io:format("B == 6~n", []), b_equals_6;
       A == 2, B == 3 -> %That is A equals 2 and B equals 3
     io:format("A == 2, B == 3~n", []),
     a_equals_2_b_equals_3;
       A == 1; B == 7 -> %That is A equals 1 or B equals 7
     io:format("A == 1 ; B == 7~n", []),
     a_equals_1_or_b_equals_7
    end.
```

* `tut9:test_if(33, 33).` -> make error, no condition for that

```erl
-module(tut10).
-export([convert_length/1]).

convert_length(Length) ->
    case Length of
      {centimeter, X} -> {inch, X / 2.54};
      {inch, Y} -> {centimeter, Y * 2.54}
    end.
```

```erl
-module(tut11).

-export([month_length/2]).

month_length(Year, Month) ->
    %% All years divisible by 400 are leap
    %% Years divisible by 100 are not leap (except the 400 rule above)
    %% Years divisible by 4 are leap (except the 100 rule above)
    Leap = if trunc(Year / 400) * 400 == Year -> leap;
        trunc(Year / 100) * 100 == Year -> not_leap;
        trunc(Year / 4) * 4 == Year -> leap;
        true -> not_leap
     end,
    case Month of
      sep -> 30;
      apr -> 30;
      jun -> 30;
      nov -> 30;
      feb when Leap == leap -> 29;
      feb -> 28;
      jan -> 31;
      mar -> 31;
      may -> 31;
      jul -> 31;
      aug -> 31;
      oct -> 31;
      dec -> 31
    end.
```

```erl
tut11:month_length(1947, aug).
%% 31
```

### Built-In Functions (BIFs)

* trunc(5.01) -> 5
* 2004 rem 400 -> 4

```erl
trunc(Year / 400) * 400 == Year -> leap;
%% same as
Year rem 400 == 0 -> leap;
```

```erl
%% can be used in guards
trunc(5.6).
%% 5
round(5.6).
%% 6
length([a,b,c,d]).
%% 4
float(5).
%% 5.0
is_atom(hello).
%% true
is_atom("hello").
%% false
is_tuple({paris, {c, 30}}).
%% true
is_tuple([paris, {c, 30}]).
%% false

%% cannot be used in guards:
atom_to_list(hello).
%% "hello"
list_to_atom("goodbye").
%% goodbye
integer_to_list(22).
%% "22"
%% These three BIFs do conversions that would be difficult (or impossible) to do in Erlang.
```

### Higher-Order Functions (Funs)

```erl
Xf = fun(X) -> X * 2 end.
%% #Fun<erl_eval.5.123085357>
Xf(5).
%% 10
```

```erl
foreach(Fun, [First|Rest]) ->
    Fun(First),
    foreach(Fun, Rest);
foreach(Fun, []) ->
    ok.
map(Fun, [First|Rest]) ->
    [Fun(First)|map(Fun,Rest)];
map(Fun, []) ->
    [].

Add_3 = fun(X) -> X + 3 end.
lists:map(Add_3, [1,2,3]).
%% [4,5,6]
```

```erl
Print_City = fun({City, {X, Temp}}) -> io:format("~-15w ~w ~w~n", [City, X, Temp end.
lists:foreach(Print_City, [{moscow, {c, -10}}, {cape_town, {f, 70}}, {stockholm, {c, -4}}, {paris, {f, 28}}, {london, {f, 36}}]).
%% moscow c -10
%% cape_town f 70
%% stockholm c -4
%% paris f 28
%% london f 36
```

```erl
-module(tut13).

-export([convert_list_to_c/1]).

convert_to_c({Name, {f, Temp}}) ->
    {Name, {c, trunc((Temp - 32) * 5 / 9)}};
convert_to_c({Name, {c, Temp}}) -> {Name, {c, Temp}}.

convert_list_to_c(List) ->
    New_list = lists:map(fun convert_to_c/1, List),
    lists:sort(fun ({_, {c, Temp1}}, {_, {c, Temp2}}) ->
           Temp1 < Temp2
         end,
           New_list).
```

## Concurrent Programming

### Processes

* Erlang can handle concurrency and distributed programming.
* In Erlang, each thread of execution is called a `process`. p93

```erl

```

```erl

```

```erl

```

```erl

```

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

```erl
<<10,20>>.
%% <<10,20>>

<<"ABC">>.
%% <<"ABC">>

<<1:1,0:1>>.
%% <<2:2>>
```

## Refrence

* [Getting Started with Erlang User's Guide](http://erlang.org/doc/getting_started/users_guide.html)
