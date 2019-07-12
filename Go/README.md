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
// Maps -> no order Guarantee
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
  fmt.Println(k,v,string(v)) // print key, code and char
}
```

## Defer, Panic & Recover

```go
defer fmt.Println("defer")
// run after the end of function before return value

defer fmt.Println("defer 1")
defer fmt.Println("defer 2")
// defer execute from last one to start LIFO (last in, first out)

a := "start"
defer fmt.Println(a)
a = "end"
// start -> get arg when send to defer
```

```go
package main

import (
  "fmt"
  "io/ioutil"
  "log"
  "net/http"
)

func main() {
  res, err := http.Get("http://www.google.com/robots.txt")
  if err != nil {
    log.Fatal(err)
  }
  defer res.Body.Close() // close befor open but run at the end
  robots, err := ioutil.ReadAll(res.Body)
  
  if err != nil {
    log.Fatal(err)
  }
  fmt.Printf("%s", robots)
}
```

```go
// panic -> can't countinue
a,b := 1, 0
ans := a / b

// Make panic
panic("someting bad happend")
```

```go
package main

import "net/http"

func main() {
  http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request){
    w.Write([]byte("Hello Go!"))
  })
  err := http.ListenAndServe(":8080", nil)
  if err != nil {
    panic(err.Error())
  }
}
```

* `panic` happen after open `defer`

```go
package main

import "fmt"
import "log"

func main() {
  fmt.Println("start")
  defer func() { // ananymous function
    if err := recover(); err != nil { // recover get panic, if no panic return nil
      log.Println("Error:", err)
    }
  }() // call function in defer
  panic("something happen")
  fmt.Println("end") // not run this line
}
// program not panic, only see panic statement
```

```go
package main

import (
  "fmt"
  "log"
)

func main() {
  fmt.Println("start")
  paniker()
  fmt.Println("end") // run at the end
}
func paniker() {
  fmt.Println("about to panic")
  defer func() {
    if err := recover(); err != nil {
      log.Println("Error:", err)
      // panic(err) -> if you can't handle error
    }
  }()
  panic("something happen")
  fmt.Println("done panicking") // not run
}
```

## Pointer

```go
var a int = 42
var b *int = &a
fmt.Println(&a, b) // return address of memory
fmt.Println(a, *b)

a := [3]int{1, 2, 3}
b := &a[0]
c := &a[1]
fmt.Printf("%v %p %p",a ,b ,c) // [1 2 3] 0x1040a124 0x1040a128
// for achange pointer arithmetic must use unsafe package
```

```go
package main

import "fmt"

type myStruct struct {
  foo int
}
func main() {
  var ms *myStruct // pointer to struct
  ms = &myStruct{foo: 42}
  fm.Println(ms) // &{42} -> &:holding a address of object

  var ms2 *myStruct
  fm.Println(ms) // -> <nil>
  ms2 = new(myStruct) // -> use new function
  fm.Println(ms) // &{0} -> default value
  ms.foo = 42 // or use (*ms).foo = 42
  fm.Println(ms.foo) // 42
}
```

```go
// Array
a := [3]int{1, 2, 3}
b := a // copy (clone) a to b
b[1] = 42
fm.Println(a, b) // [1 2 3] [1 42 3]

// Slice
a := []int{1, 2, 3}
b := a // copy adress a to b -> same thing
b[1] = 42
fm.Println(a, b) // [1 42 3] [1 42 3]

// Map
a := map[string]string{"foo":"bar", "baz":"buz"}
b := a  // copy adress a to b -> same thing
```

## Function

```go
package main

import "fmt"

func main() {
  sayMessage("Hello Go!")
}
func sayMessage(msg string) {
  fmt.Println(msg)
}

func sayMessage(greeting, name string){ // same as (greeting string, name string)
  fmt.Println(greeting, name)
}

func sayMessage(greeting, name *string){ // send with pointer -> can change
  fmt.Println(*greeting, *name)
}

// sum(1, 2, 3, 4, 5)
func sum(values ...int) { // only as last parameters & make it Slice
  fmt.Println(values)
  result := 0
  for _, v := range values {
    result += v
  }
  fmt.Println("The sum of values: ", result)
}

// sum("The sum of values: ",1, 2, 3, 4, 5)
func sum(msg string, values ...int) { // only as last parameters & make it Slice
  fmt.Println(values)
  result := 0
  for _, v := range values {
    result += v
  }
  fmt.Println(msg, result)
}

// s := sum(1, 2, 3, 4, 5)
func sum(values ...int) int { // return value
  result := 0
  for _, v := range values {
    result += v
  }
  return result
}

// s := sum(1, 2, 3, 4, 5)
// fmt.Println(*s)
func sum(values ...int) *int { // return pointer
  result := 0
  for _, v := range values {
    result += v
  }
  return &result
}

func sum(values ...int) (result int) { // return pointer
  for _, v := range values {
    result += v
  }
  return
}

// d ,err := devide(5.0,3.0)
// if err != nil { ... }
func devide(a, b float64) (float64, error) {
  if b == 0.0 {
    // panic("Cannot provide zero as second parameter")
    return 0.0, fmt.Errorf("Cannot divide by zero")
  }
  return a / b , nil
}

// Ananyoumos function
func() {
  fmt.Println("Hello Go!")
}() // invoke function

i := 10
func(i int) {
  fmt.Println(i)
}(i)

// var f func()
f := func() {
  fmt.Println("Hello Go!")
}
f()
// var f func(string,string,int) (int, error)
```

## Interface

* interface dont describe data, describe behavior

```go
type Writer interface{
  Write([]byte) (int, error)
}

type ConsoleWriter struct {}

func (cw ConsoleWriter) Write(data []byte) (int, error) {
  n, err := fmt.Println(string(data))
  return n, err
}

func main() {
  var w Writer = ConsoleWriter{}
  w.Write([]byte("Hello Go!"))
}
```

```go
func main() {
  myInt := IntCounter(0)
  var inc Incrementer = &myInt
  for i := 0; i < 10; i++ {
    fmt.Println(inc.Increment())
  }
}

type Incrementer interface{
  Increment() int
}

type IntCounter int

func (ic *Incrementer) Increment() int {
  *ic++
  return int(*ic)
}
```

```go
package main
import (
  "fmt"
  "bytes"
  "io"
)

func main() {
  var wc WriterCloser = NewBufferWriterCloser() // return pointer
  wc.Write([]byte("Hello Listener, this is test")) // return 8 char in every line
  wc.Close() // return the last character if they are less than 8

  bwc := wc.(*BufferWriterCloser) // type convertion
  fmt.Println(bwc) // memory address

  // bwc := wc.(io.Reader) -> can not convert
  r, ok := wc.(io.Reader)
  if ok {
    fmt.Println(r)
  } else {
    fmt.Println("Convertion Failed")
  }
}

type Writer interface {
  Write([]byte) (int, error)
}
type Closer interface {
  Close() error
}
type WriterCloser interface {
  Writer
  Close
}
type BufferWriterCloser struct {
  buffer *bytes.Buffer
}
func (bwc BufferWriterCloser) Write(data []byte) (int, error){
  n, err = bwc.buffer.Write(data)
  if err != nil {
    return 0, err
  }

  v := make([]byte, 8)
  for bwc.buffer.len() > 8 {
    _, err := bwc.buffer.read(v)
    if err != nil {
      return 0, err
    }
    _, err := fmt.Println(string(v))
    if err != nil {
      return 0, err
    }
  }
  return n, nil
}
func (bwc BufferWriterCloser) Close(data []byte) error {
  or bwc.buffer.len() > 0 {
    data := bwc.buffer.Next(8)
    _, err := fmt.Println(string(v))
    if err != nil {
      return err
    }
  }
  return nil
}
func NewBufferWriterCloser() *BufferWriterCloser{
  return &BufferWriterCloser{
    buffer: bytes.NewBuffer([]byte{})
  }
}
```

```go
// Empty interface
var myObj interface{} // -> everything can cast obj from it, when need to work with multiple things

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
```

* try to use many, small interfaces
* Design function and methods to recieve interfaces whenever possible

```go
// type convertion
bwc := wc.(*BufferWriterCloser)
  fmt.Println(bwc) // memory address

  // bwc := wc.(io.Reader) -> can not convert
  r, ok := wc.(io.Reader)
  if ok {
    fmt.Println(r)
  } else {
    fmt.Println("Convertion Failed")
  }
```

## Go Routhins

```go
func main() {
  go sayHello()
  time.sleep(400*time.Millisecond) // whitout this cant see sayHello -> kill before run
}
func sayHello() {
  fmt.Println("Hello Go!")
}
```

```go
func main() {
  msg := "Hello Go!"
  go func() {
    fmt.Println(msg)
  }()
  msg := "Goodbye"
  time.sleep(100 * time.Millisecond)
} // Goodbye -> not Guarantee -> for solving that problem we can send data directly

func main() {
  msg := "Hello Go!"
  go func(msg string) { // prevent race condition
    fmt.Println(msg)
  }(msg)
  msg := "Goodbye"
  time.sleep(100 * time.Millisecond)
} // Hello Go!
```

```go
import (
  "fmt"
  "sync"
)

var wg = sync.WaitGroup{} // sync multiple go routhin

func main() {
  msg := "Hello Go!"
  wg.Add(1)
  go func(msg string) {
    fmt.Println(msg)
    wg.Done()
  }(msg)
  msg := "Goodbye"
  wg.Wait()
}
```

```go
import (
  "fmt"
  "sync"
)

var wg = sync.WaitGroup{}
var counter = 0

func main() {
  for i := 0; i < 10;i++ {
    wg.Add(2)
    go sayHello()
    go increment()
  }
  wg.Wait()
}

func sayHello() {
  fmt.Printf("Hello #%v\n", counter)
  wg.Done()
}

func increment() {
  counter++
  wg.Done()
}
// the result change every time
```

```go
import (
  "fmt"
  "runtime"
  "sync"
)

var wg = sync.WaitGroup{}
var counter = 0
var m = sync.RWMutex{} // read/write mutax -> one time can access to a piece of code

func main() {
  runtime.GOMAXPROCS(100)
  for i := 0; i < 10;i++ {
    wg.Add(2)
    m.RLock()
    go sayHello()
    m.Lock()
    go increment()
  }
  wg.Wait()
}

func sayHello() {
  fmt.Printf("Hello #%v\n", counter)
  m.RUnlock()
  wg.Done()
}

func increment() {
  counter++
  m.Unlock()
  wg.Done()
}
```

```go
fmt.Printf("Threads: %v\n",runtime.GOMAXPROCS(-1)) // show available threads -> by default show os threads = cpu core
runtime.GOMAXPROCS(100) // set program run thread to 100
// use when program need use a lot of syncronize routhine
// more threads can increase performance, but too many can slow it down
```

* Don't creat gorouthines in libraries -> let consumer control concurrency
* always know how to end end gorouthines -> avoid subtle memory leaks
* check for gorouthines race condition -> use `-race` when run or build program

## Channels

```go
ch := make(chan int)
wg.add(2) // sync.WaitGroup
go func() {
  i := <- ch // recieve data from channel
  fmt.Println(i)
  wg.Done()
}()
go func() {
  ch <- 42 // send data to channel
  wg.Done()
}()
wg.Wait()
```

```go
ch := make(chan int)
go func() {
  i := <- ch // recieve data from channel
  fmt.Println(i)
  wg.Done()
}()

for j := 0; j < 5; j++ {
  wg.add(2) // sync.WaitGroup
  go func() {
    ch <- 42 // send data to channel
    wg.Done()
  }()
}
wg.Wait()
// get Deadlock because send 5 time but recieve 1 time -> can't buffer in channel
```

```go
ch := make(chan int)
wg.add(2) // sync.WaitGroup
go func() {
  i := <- ch  // recieve 42
  fmt.Println(i)
  ch <- 27 // send 27
  wg.Done()
}()
go func() {
  ch <- 42 // send 42
  fmt.Println(<- ch) // recieve 27
  wg.Done()
}()
wg.Wait()
// 42
// 27
// both reader/writer
```

```go
ch := make(chan int)
wg.add(2) // sync.WaitGroup
go func(ch <-chan int) { // recieve only channel
  i := <- ch  // recieve 42
  fmt.Println(i)
  wg.Done()
}(ch)
go func(ch chan<- int) { // send only channel
  ch <- 42 // send 42
  wg.Done()
}(ch)
wg.Wait()
```

```go
// buffer
ch := make(chan int, 50) // get 50 buffer for channel
wg.add(2) // sync.WaitGroup
go func(ch <-chan int) { // recieve only channel
  i := <- ch  // recieve 42
  fmt.Println(i)
  wg.Done()
}(ch)
go func(ch chan<- int) { // send only channel
  ch <- 42 // send 42
  ch <- 27 // send 27 -> whitout buffer get deadlock, now we lost it
  wg.Done()
}(ch)
wg.Wait()
// 42
```

```go
ch := make(chan int, 50) // get 50 buffer for channel
wg.add(2) // sync.WaitGroup
go func(ch <-chan int) { // recieve only channel
  for i := range ch {
    fmt.Println(i)
  }
  wg.Done()
}(ch)
go func(ch chan<- int) { // send only channel
  ch <- 42 // send 42
  ch <- 27 // send 27
  close(ch) // prevent deadlock for loop
  wg.Done()
}(ch)
wg.Wait()
// 42
// 27
```

* can't send to closed channel, it make panic

```go
ch := make(chan int, 50) // get 50 buffer for channel
wg.add(2) // sync.WaitGroup
go func(ch <-chan int) { // recieve only channel
  for {
    if i, ok := <- ch; ok {
      fmt.Println(i)
    } else {
      break
    }
  }
  wg.Done()
}(ch)
go func(ch chan<- int) { // send only channel
  ch <- 42 // send 42
  ch <- 27 // send 27
  close(ch) // prevent deadlock for loop
  wg.Done()
}(ch)
wg.Wait()
// 42
// 27
```

```go
const (
  logInfo = "INFO"
  logWarning = "WARNING"
  logError = "ERROR"
)

type logEntry struct {
  time time.Time
  severity string
  message string
}

var logCh = make(chan logEntry, 50)

func main() {
  go logger()
  // for prevent deadlock
  defer func() {
    close(logCh)
  }()
  logCh <- logEntry{time.Now(), logInfo, "App is starting"}

  logCh <- logEntry{time.Now(), logInfo, "App shutting down"}
  time.Sleep(100 * time.Millisecond)
}

func logger() {
  for entry := range logCh {
    fmt.Printf("%v - [%v]%v\n", entry.time.Format("2006-01-02T15:04:05"), entry.severity, entry.message)
  }
}

```

```go
// use select
const (
  logInfo = "INFO"
  logWarning = "WARNING"
  logError = "ERROR"
)

type logEntry struct {
  time time.Time
  severity string
  message string
}

var logCh = make(chan logEntry, 50)
var doneCh = make(chan struct{}) // can't send or recieve data -> signal only channel

func main() {
  go logger()
  logCh <- logEntry{time.Now(), logInfo, "App is starting"}

  logCh <- logEntry{time.Now(), logInfo, "App shutting down"}
  time.Sleep(100 * time.Millisecond)
  doneCh <- struct{}{}
}

// use select for prevent deadlock instead of defer
func logger() {
  select {
    case entry <- logCh:
      fmt.Printf("%v - [%v]%v\n", entry.time.Format("2006-01-02T15:04:05"), entry.severity, entry.message)
    case <- doneCh
      break
  }
}
```

## Context

* work like channel, must be a first arg and named ctx
* make context from parent context except background.
* background is a parent of all context and define in main
* parnt context kill child but not effect on its parent

```go
func leaf2() {
  select {
    case <- time.After(7 * time.Second):
      fmt.Println("ok - end of leaf 1")
    case <- ctx.Done():
      fmt.Println(ctx.Err())
      fmt.Println("Close -leaf1 closed by ctx")
  }

  fmt.Println("leaf 1")
}

func leaf2() {
  select {
    case <- time.After(3 * time.Second):
      fmt.Println("ok - end of leaf 2")
    case <- ctx.Done():
      fmt.Println(ctx.Err())
      fmt.Println("Close -leaf2 closed by ctx")
  }

  fmt.Println("leaf 2")
}

func branch(ctx context.Context) {
  ctx2, cnl := context.WithCancel(ctx) // return new context and cancel func

  go leaf1(ctx2)
  go leaf2(ctx2)

  time.Sleep(5 * time.Second)
  fmt.Println("end of Branch")
  cnl() // send signal to close
}

func main() {
  ctx := context.Background()

  go branch(ctx)

  // prevent close
  ch := make(chan os.Signal)
  signal.Notify(ch)
  <-ch
}
```

```go
// define
ctx := context.WithValue(context.Background(), k, "Go")
// use
if v := ctx.Value(k); v != nil {
  fmt.Println("found value:", v)
  return
}
```

```go
// use context in library
req, err := http.NewRequest("GET","http://google.com")
if err != nil {
  panic(err)
}

req = rea.WithContext(ctx) // can close from outside

cli := &http.Client{}
resp, err := cli.Do(req)
if err != nil {
  panic(err)
}

fmt.Println("Status:",resp.Status)
```

```go
type key string // define type -> only for this package (lowercase) and can access to it from outside of package
// use
ctx := context.WithValue(ctx, key("string"), 10)
//
fmt.Println(ctx.Value(key("string")))
```

* [more info about contex](https://golang.org/pkg/context/)

## Refrences

* [Golang](www.golang.org)
* [Learn Go Programming - Golang Tutorial for Beginners](https://www.youtube.com/watch?v=YS4e4q9oBaU)
