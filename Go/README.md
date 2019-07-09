# Go

## Set up Go

### Install Go

download from [Golang](www.golang.org)

```sh
go version
# go version go1.12.6 windows/amd64
```

### First Program

```go
// #Main.go
package main

import "fmt"

func main() {
    fmt.Println("Hello, فارسی")
}
```

### Run Or Build

```sh
go run Main.go
# run in virtual server
```

```sh
go build Main.go
# make exe file
```

### Go Tour

```sh
go get golang.org/x/tour
tour
```

### Go env

```sh
go env
```

* `GOROOT` -> go file location
* `GOPATH` -> your code location or workspace

* [your work space]
  * bin
  * pkg
  * src
    * github.com
      * [your github accound name]
        * [application name]

### install package

```sh
go install [package name]
```

## Variable

```go
var i int
i = 42
fmt.Println(i)

var j int = 47 //define & assign
var j2 float32 = 47 //define & assign
k :=45 //define & assign as int
k2 :=45. //define & assign as float64

fmt.printf("%v , %T" ,k,k) // print with format => T:show type

var (
  var age int = 23
  var name string = "Mohsen"
)
```

* Cant use : syntax in package level
* Camel case (Lower case first letter) variable in package level can use inside package
* Pascal case (Upper case first letter) variable in package level can see from outside package
* Capitalize acronyms(HTTP, URL)

### Convert Variable

```go
var i int = 32
var f float = 42.1

i = int(f)

i=42
var s string
s = string(i) // back character with code=42 -> "*"
// import strconv
s = strconv.Itoa(i) // -> "42"
```

### Data Type

```go
var b bool = true
b = false
c := 1==1
// bool (default) Zero value is false

n := 43 // int has vary size min 32bit
// int8 -128 - 127
// int16 -32,768 - 32,767
// int32 +/- 2E9
// int64 +/- 2E18

// byte/uint8 0 - 256
// uint16 0 - 65,538
// uint32 0 - 4e9
// int Zero value is 0

n := 43. // float64 +/- 2.23E-308 - +/-1.8E308
var n1 float32 // +/- 1.18E-38 - +/-3.4E38
n1 = 3.14e3
// float Zero value is 0

var n complex64 = 1 + 2i
m := 2i
fmt.Printf("%v , %T", n, n) // 1, complex64
fmt.Printf("%v , %T", real(n), real(n)) // 1, float32
fmt.Printf("%v , %T", imag(n), imag(n)) // 2, float32

var n complex128 = 1 + 2i
fmt.Printf("%v , %T", n, n) // 1, complex128
fmt.Printf("%v , %T", real(n), real(n)) // 1, float64
fmt.Printf("%v , %T", imag(n), imag(n)) // 2, float64
// complex Zero value is 0+0i

var s := "this is string"
fmt.Printf("%v , %T", s, s) // this is string , string
fmt.Printf("%v , %T", s[2], s[2]) // 105 , uint8

var s2 := "other string"
fmt.Printf("%v , %T", s+s2, s+s2)

b := []byte(s)
fmt.Printf("%v , %T", b, b) // [116 ... ] , []init8
// string -> utf8

r := 'a' // Rune
fmt.Printf("%v , %T", a, a) // 97, int32
// Rune -> utf32
```

* operator `+ - * / %` can only use on same type
* operator `& | ^ &^` -> and or xor xnor
* operator `>> <<`

```go
a := 8
fmt.Println(a << 3) // 2^3 * 2^3 = 64
fmt.Println(a >> 3) // 2^3 / 2^3 = 1
```

## Constant

```go
const myConst int = 2
// const myConst float64 = math.Sin(1.57) => make error need to replace at compile time

const a = iota // 0
const (
  b = iota // 0
  c // -> c=iota ->1
  d // -> c=iota ->2
)
const a2 = iota // 0
const (
  _ = iota // 0 -> dont care about this value
  e // -> c=iota ->1
  f // -> c=iota ->2
)
const (
  _ = iota + 6 // 6 -> dont care about this value
  g // -> c=iota ->7
  h // -> c=iota ->8
)
const (
  _ = iota
  KB = 1 << (10 * iota)
  MB
  GB
  TB
)
const (
  isAdmin = 1 << iota
  isHeadquarter
  canSeeFinance

  canSeeAfrica
  canSeeAsia
  canSeeEurope
)
// var roles byte = isAdmin | canSeeFinance | canSeeAsia
// fmt.Printf("isAdmin? %v", roles & isAdmin == isAdmin)
```

* like variable Pascal case for export and Camel case for use in package

## Arrays & Slices

```go
// Arrays -> fix size
var students [3]string
students[0]="Lisa"
fmt.Printf("students: %v", students)
fmt.Printf("student #1: %v", students[1])
fmt.Printf("number of students: %v", len(students))

grades := [...]int{97,23,45}
fmt.Printf("Grades: %v", grades)

var identityMatrix [3][3]int = [3][3]int { [3]int{1, 0, 0},  [3]int{0, 1, 0},  [3]int{0, 0, 1} }

a := [...]int{97,23,45}
b := &a // b point to same data
b[1] = 5 // a,b change
fmt.Printf("numbers: %v", a) // [97 5 45]

// Slices
a := []int{1, 2, 3}
fmt.Printf("numbers: %v", a)
fmt.Printf("Lenght: %v", len(a))
fmt.Printf("Capacity: %v", cap(a)) // -> lenght of underlying array

// Arrays or Slices
a := []int{1, 2, 3, 4, 5, 7, 8, 9, 10}
b := a[:]
c := a[3:]
d := a[:6]
e := a[3:6]
// do not clone its only a link to array or slice

a := make([]int, 3) //[0 0 0]
a := make([]int, 3, 100) //len 3, cap 100

a := []int{} //len 0, cap 0
a = append(a, 1) //len 1, cap 2
a = append(a, 2, 3, 4, 5) //len 5, cap 8

b := a[1:] // remove from start
b := a[:len(a)-1] // remove from end
b := append(a[:2],a[3:]...) // remove ele index #2 but change a
```

## Maps & Structs

```go
// Maps -> no order garanty
cityPopulation := map[string]int{
  "Ramsar": 75000,
  "Rasht":  1000000,
  "Tehran": 12000000
}
fmt.Printf(cityPopulation)

statePopulation := make(map[string]int) // define
statePopulation = map[string]int{
  "Mazandaran": 2000000,
  "Gilan":  1500000,
  "Tehran": 15000000
}
fmt.Printf(statePopulation["Tehran"]) // 15000000

statePopulation["Kermanshah"] = 1700000
delete(statePopulation, "Tehran")
fmt.Printf(statePopulation["Tehran"]) // 0 -> not found
pop , ok := statePopulation["Tehran"]
fmt.Printf(pop , ok) // 0 , false
_ , ok := statePopulation["Gilan"] // no need first ele
fmt.Printf(ok) // true -> have that key

fmt.Printf(len(statePopulation))
```

```go
// Struct
type Doctor struct {
  number int
  actorName string
  companion []string
}

aDoctor := Doctor {
  number: 3,
  actorName: "Jon Pertwee",
  companion: []string {
    "Liz Shaw", "Jo Grant"
  }
}
fmt.Printf(aDoctor)
fmt.Printf(aDoctor.actorName)
fmt.Printf(aDoctor.companion[1])

aDoctor2 := Doctor {
  3,
  "Jon Pertwee",
  []string {
    "Liz Shaw", "Jo Grant"
  }
} // when complete all field

// Ananymous Struct -> short live struct
aDoctor := struct{name string}{name:"John Pertwee"}
fmt.Printf(aDoctor) // John Pertwee

aDoctor := struct{name string}{name:"John Pertwee"}
anotherDoctor := aDoctor
anotherDoctor.name = "Tom Baker"
fmt.Printf(aDoctor) // {John Pertwee}
fmt.Printf(anotherDoctor) // {Tom Baker}

type Animal struct {
  Name  string
  Origin  string
}
type Bird struct {
  Animal
  SpeedKPH  float32
  CanFly  bool
}
b := Bird{}
b.Name = "Emu" // inherit from animal
b.CanFly = false
fmt.Println(b.Name)
b := Bird{
  Animal: Animal{Name:"",Origin=""},
  SpeedKPH: 48,
  CanFly: false
}

// Struct tag -> use reflect package to see tag, need other package for validation
import (
  "fmt"
  "reflect"
)
type Animal struct {
  Name  string `required max:"100"`
  Origin  string
}
t := reflect.TypeOf(Animal{})
field, _ := t.FieldByName("Name")
fmt.Println(field.Tag)
```

## If & Switch

```go
if true {
  fmt.Println("true")
}

if pop , ok := statePopulation["Tehran"]; ok {
  fmt.Printf("Tehran Population: %v",pop)
}

if n < g {
  fmt.Println("n < g")
}
if n == g {
  fmt.Println("n == g")
}
if n >= g {
  fmt.Println("n >= g")
}

if g < 1 || g > 100 {
  fmt.Println("out of range")
}
if g >= 1 && g <= 100 {
  fmt.Println("in the range")
}

if g < 1 || g > 100 {
  fmt.Println("out of range")
} else {
  fmt.Println("in the range")
}

switch n {
  case 1:
    fmt.Println("one")
  case 2:
    fmt.Println("two")
  case 3,4,4:
    fmt.Println("other")
  default:
    fmt.Println("not one or two or other")
}

i := 10
switch {
  case i <= 10 :
    fmt.Println("less than 10")
  case i <= 20 :
    fmt.Println("less than 20")
  default:
    fmt.Println("greater  than 20")
}
// only do first case
// no need break to prevent fallthrough

// no tag switch
i := 10
switch {
  case i <= 10 :
    fmt.Println("less than 10")
    fallthrough
  case i <= 20 :
    fmt.Println("less than 20")
  default:
    fmt.Println("greater  than 20")
}
// only do first & second case

var i interface{} = 1
switch i.(type) {
  case int:
    fmt.Println("i is an int")
    break // break out early
    fmt.Println("not see this")
  case float64:
    fmt.Println("i is an int")
  case string:
    fmt.Println("i is an string")
  case [3]int:
    fmt.Println("i is an [3]int")
  default:
    fmt.Println("i is another type")
}
// i is an int
```

## Loop

```go
for i := 0; i < 5; i++ {
  fmt.Println(i)
}

for i,j := 0, 0; i < 5;i,j = i+1,j+2{
  fmt.Println(i,j)
}

i := 0
for i < 5 {
  fmt.Println(i)
  i++
}

i := 0
for {
  fmt.Println(i)
  i++
  if i == 5 {
    break
  }
}

for i := 0; i < 10; i++ {
  if i % 2 == 0 {
    continue
  }
  fmt.Println(i)
}
for i := 0; i < 3; i++ {
  for i := 0; i < 3; i++ {
    fmt.Println(i*j)
  }
}

for i := 0; i < 10; i++ {
  for i := 0; i < 310; i++ {
    fmt.Println(i*j)
    if i % 2 == 0 {
      // break -> only break inner loop
      break Loop // break and go to label
    }
  }
}
Loop: // label

// Slice
s := []int{1,2,3}
for k,v := range s {
  fmt.Println(k,v) // print key and value
}

// Map
cityPopulation := map[string]int{
  "Ramsar": 75000,
  "Rasht":  1000000,
  "Tehran": 12000000
}
for k,v := range cityPopulation {
  fmt.Println(k,v) // print key and value
}

// string
s := "Hello Go!"
for k,v := range s {
  fmt.Println(k,v,string(v)) // print key and value
}
```

3:41:31

## Refrences

* [Golang](www.golang.org)
* [Learn Go Programming - Golang Tutorial for Beginners](https://www.youtube.com/watch?v=YS4e4q9oBaU)
