# Type Script

## install type script

`npm install -g typescript`

## typescript version

`tsc --version`

## compile and get `main.js` and run

```ts

tsc main.ts
node main.js
//or
tsc main.ts && node main.js

```

## variables

`var i=8` => global variable

`let i=4` => compile to var but have scope & type

```ts

let a:number;
let a:boolean;
let a:string;
let a:any; => let a;

//array
let a:number[];
let a:number[]=[1,2,3];
let a:any[]=[1,true,'salam'];

//Tuple
let x: [string, number];
x = ["hello", 10];

//Enum
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
let background = Color.Red;
enum Color {Red = 1, Green = 2, Blue = 3}//add values  manually to prevent any problem after change enum

```

we have `void`: mean nothing (null or Undefined), `never`: if function go to throw error, `object`: for object ;)

## Type assertions

for having intellisence

```ts
let strLength: number = (<string>someValue).length;
let strLength: number2 = (someValue as string).length;
```

## Arrow Function

```ts
let log = (message) => console.log(message);
```

## Interface

inline annotation

```ts
let func = (point:{x:number,y:number})=>{ ...... }
```

interface

```ts
interface Point{
    x:number,
    y:number
}
let func = (point:Point)=>{ ...... }

interface Other{
    color?: string, //optional
    readonly x: number; //can not change,
    func: () => void
}
```

## Class

```ts
class Point{
    //fileds
    x:number;
    y:number;

    //method
    draw(){ .... }
}
let point:Point = new Point();
```

constructor

```ts
class Greeter {
    greeting: string;
    constructor(message?: string) { //optional variable
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```

inherit

```ts
class Point {
    x: number;
    y: number;
}
class Point3d extends Point {
    z: number;
}
```

also have `private`, `protected`, `abstract` & `static`

use Access Modifier in construct parameters

```ts
class Point {
    constructor(private x: number,private y: number) {
    }
}
// same as
class Point {
    private x: number;
    private y: number;
    constructor(x: number,y: number) {
        this.x = x;
        this.y = y;
    }
}
```

access property
if have error `tsc *.ts --target ES%`

```ts
class num{
    private _x:number;

    get x(){
        return this._x;
    }
    set x(value){
        if(value > 0){
            this._x = value;
        }
    }
}
```

## Modules

Modules file need to expot something(one or more class, function, variable, ...)

```ts
//point.ts
export class Point{ ..... }
```

use Modules

```ts
//main.ts
import {Point} from './point'

let point:Point = new Point();
```

## Use Backtick

```ts
let user = {name:'mohsen',email='...'};
console.log(`Username is ${user.name}, email is ${user.email}`);
```
