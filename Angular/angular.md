# Angular

## pre-install
`node -v`

`npm -v`

## install globaly
`npm install -g @angular/cli`


## make project name: my-app
`ng new my-app`

## run app
`cd my-app`

`ng serve --open`

--------------------------------------
## install type script
`npm install -g typescript`

### typescript version
`tsc --version`

### compile and get `main.js` and run
```
tsc main.ts
node main.js
//or
tsc main.ts && node main.js
```

### variables 
`var i=8` => global variable

`let i=4` => compile to var but have scope & type

```
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

### Type assertions
for having intellisence
```
let strLength: number = (<string>someValue).length;
let strLength: number = (someValue as string).length;
```

### Arrow Function
```
let log = (message) => console.log(message);
```

### Interface
inline annotation
```
let func = (point:{x:number,y:number})=>{ ...... }
```
interface
```
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

### Class
```
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
```
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
```
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
```
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
```
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

### Modules

Modules file need to expot something(one or more class, function, variable, ...)
```
//point.ts
export class Point{ ..... }
```
use Modules
```
//main.ts
import {Point} from './point'

let point:Point = new Point();
```

### Use Backtick
```
let user = {name:'mohsen',email='...'};
console.log(`Username is ${user.name}, email is ${user.email}`);
```
--------------------------------------
* Modules is some related component
* component Date + html + logic
    * creat component
    * register in modules
    * add element to html markup

### Creat Component 
angular generate component course
```
ng g c course
```

### Template

```
@component{(
    template:` // backtick for many line
    <h1>{{"Title: "+title+ " " + getCount() }}</h1>
    <ul>
    <li *ng-for="let ele of list">{{ele}}</li>
    </ul>
    `
)}
export class mycomponent{
    title='app title';
    count=4;
    list=['ali','hasan','saeed']
    getCount(){
        return this.count;
    }
}
```

### Creat Service 
angular generate service readlist
```
ng g s readlist
```
* using service
```
export class mycomponent{
    list;
    constructor(read: readlist){ // dependency injection
        list=readlist.getlist()
    }
}
```
for use dependency injection, declare service in module providers

### Property Binding
one way from component to Dom
```
<h2>{{title}}</h2>
//or
<h2 [textContent]="text"></h2>

<img src="{{imageUrl}}">
//or
<img [src]="imageUrl">
```
* for element not in Dom like `colspan` use `[attr.colspan]`

### Add Bootstrap
```
npm install botstrap --save
```
`save` flag add boorstrap as dependency in `package.json`

add bootstrap to global style file: `styles.css`
```
@import "~bootstrap/dist/css/bootstrap.css";
```
* `^3.4.7` (minor.minor.patch) means last version of 3

### Class Binding
```
@component{(
    template:`
    <button class="btn btn-primary" [class.active]="isActive"></button>
    `
)}
export class mycomponent{
    isActive=true;
}
```
if `isActive==true` class `active` add to button, else not adding.

### Style Binding
```
@component{(
    template:`
    <button [style.backgroundColor]="isActive? 'blue':'white' "></button>
    `
)}
export class mycomponent{
    isActive=true;
}
```
* for more info see Dom style object list

### Event Binding
```
@component{(
    template:`
    <button (click)="onSave()"></button>
    <button (click)="onSave2($event)"></button>
    `
)}
export class mycomponent{
    onSave(){}
    onSave2($event){}
}
```
* Event Bubbling mean from inner object to outer one.
* for stop Bubbling `$event.stopPropagation()`

### Event Filter
```
@component{(
    template:`
    <input (keyup)="OnKeyUp($event)" />
    <input (keyup.enter)="onEnter()" />
    `
)}
export class mycomponent{
    OnKeyUp($event){
        if ($event.keycode == 13)
            console.log("Enter presssed.");
    }
    onEnter(){
        console.log("Enter presssed.");
    }
}
```
### Template Variable
```
@component{(
    template:`
    <input (keyup.enter)="onEnter($event)" />
    <input #name (keyup.enter)="onEnter2(name.value)" />
    `
)}
export class mycomponent{
    onEnter($event){
        console.log($event.target.value);
    }
    onEnter2(name){
        console.log(name);
    }
}
```

### Two Way Binding
* Banana in the box [()]
```
@component{(
    template:`
    <input [value]="name" (keyup.enter)=" email=$event.target.value; onEnter(name.value)" />
    <input [(ngModel)]="name2" (keyup.enter)="onEnter2(name.value)" />
    `
)}
export class mycomponent{
    name = 'ali';
    name2 = 'saeed';
    onEnter(){
        console.log(name);
    }
    onEnter2(){
        console.log(name2);
    }
}
```
* need to add forms module to modules
```
import { FormsModule } from '@angular/forms'
...
@ngMoModule({
    ...
    imports:[
        ...
        FormsModule
    ]
    ...
})
...
```

### Pipes
```
@component{(
    template:`
    {{ course.title }} <br />
    {{ course.title | lowercase }} <br />
    {{ course.title | uppercase }} <br />
    {{ course.student }} <br />
    {{ course.student | number }} <br />
    {{ course.rating }} <br />
    {{ course.rating | number:'2.2-3' }} <br /> // 'integernumber.minafterpoint-maxafterpoin'
    {{ course.price }} <br />
    {{ course.price | currency }} <br />
    {{ course.price | currency:'AUD' }} <br />
    {{ course.price | currency:'AUD':true }} <br /> //with sign
    {{ course.price | currency:'AUD':true:'3.1-2' }} <br />
    {{ course.releaseDate }} <br />
    {{ course.releaseDate | date:'shortdate' }} <br />
    `
)}
export class mycomponent{
    course={
        title: 'Angular App',
        student: 30146 
        rating: 4.9745
        price: 1990.95
        releaseDate: new Date(2016,3,1)
    }
}
```

### Custome Pipe
