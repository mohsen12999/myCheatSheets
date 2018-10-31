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
angularCli generate component course
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
angularCli generate service readlist
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
angularCli generate pipe mypipe
```
ng g c mypipe
```
send variable to Pipe ` {{ bigString | summary:40 }}`
```
export class SummaryPipe implements PipeTransform {

  transform(value: string, limit?: number): any {
    if(!value)
      return null;
    let actualLimit = (limit)?limit:50;
    if(value.length <= actualLimit)
      return value;
    return value.substr(0,actualLimit)+'...';
  }
}
```

### Component Api
send recieve information from component
state for input & event for output

### Input Properties
for send information to component
```
<mycomponent [isFavorite]="post.isfavorite"></mycomponent>
```
2 way for send
* first way
```
import {... , Input} from '@angular/core'
...
export class mycomponent{
    @input() isFavorite = false;
}
```
* second way
```
@component{(
    ...
    input:['isFavorite']
)}
export class mycomponent{
    isFavorite = false;
}
```
* Aliasing input
```
<mycomponent [is-favorite]="post.isfavorite"></mycomponent>
```
can not define or use `is-favorite` as variable in typescript or javascript
```
export class mycomponent{
    @input('is-favorite') isFavorite = false;
}
```
### Output Properties
for recieve
```
<mycomponent (change)="onFavoriteChange()"></mycomponent>
```
```
import {... , Output,EventEmitter} from '@angular/core'
...
export class mycomponent{
    @output()  change = new EventEmitter();

    onClick(){
        ...
        this.change.emit();//raise event
    }
}
```
### Passing Event Data
```
export class mycomponent{
    ...
    onClick(){
        ...
        this.change.emit(this.count);//a variable
        //or
        this.change.emit({count:this.count });//an object
    }
}
```
```
<mycomponent (change)="onFavoriteChange($event)"></mycomponent>
```
* Aliasing Output
```
<mycomponent (change)="onFavoriteChange()"></mycomponent>
```
```
export class mycomponent{
    @output('change')  changeEvent = new EventEmitter();
}
```

### view Encapsulation
* `Shadow Dom` Allows us to apply scoped styles to elements without bleeding out to the outer world.
```
@Component({
  ...
  encapsulation: ViewEncapsulation.Emulated // angular try to emulate shadow dom
  //or
  encapsulation: ViewEncapsulation.Native // use directly shadow dom [not support by all browser] and not use other css from outside of shadow dom
})
```

### ngContent
sending information to component
mypanel.component.html
```
<div class="panel panel-default">
    <div class="panel-heading">
        <ngContent select=".headercontent"></ngContent> //element with class headercontent come hear
    </div>
    <div class="panel-body">
        <ngContent select=".bodycontent"></ngContent> //element with class bodycontent come hear
    </div>
</div>
```
* `select` like css selector & can be class or id or element.
```
<mypanel>
    <div class="headercontent"> header title </div>
    <div class="bodycontent">
        <h1>body</h1>
        <p>some thing ...</p>
    </div>
</mypanel>
```
* dont need `select` if we have only one `ngContent`.

### ngContainer
if use ngContainer for sending information, only inside it send
```
<mypanel>
    <ngContainer class="headercontent"> header title </ngContainer>
    <ngContainer class="bodycontent">
        <h1>body</h1>
        <p>some thing ...</p>
    </ngContainer>
</mypanel>
```

### ngIf
```
<div *ngIf="courses.lenght > 0"> // or function with true/false return
    courses list
</div>
<div *ngIf="courses.lenght == 0">
    no courses
</div>
```
or use `else` and `ng-template`
```
<div *ngIf="courses.lenght > 0; else noCourse">
    courses list
</div>
<ng-template #noCourse>
    no courses
</ng-template>
```
or use `then`, `else` and `ng-template`
```
<div *ngIf="courses.lenght > 0; then courseList else noCourse"></div>
<ng-template #courseList>
    no courses
</ng-template>
<ng-template #noCourse>
    no courses
</ng-template>
```

### hidden property
* exist but hidden
```
<div [hidden]="courses.lenght == 0"> // or function with true/false return
    courses list
</div>
<div [hidden]="courses.lenght > 0">
    no courses
</div>
```

### ngSwitch & ngSwitchCase
```
export class mycomponent{
    viewName;
}
```
```
<ul class="nav nav-pills">
    <li [class.active]="viewName == 'map'" ><a (click)="viewName = 'map'">Map View</a></li>
    <li [class.active]="viewName == 'list'" ><a (click)="viewName = 'list'">List View</a></li>
</ul>
<div [ngSwitch]="viewName">
    <div *ngSwitchCase="'map'">Map View Content</div>
    <div *ngSwitchCase="'list'">List View Content</div>
    <div *ngSwitchDefault>Otherwise</div> //when none of them
</div>
```

### ngFor
```
export class mycomponent{
    courses ={
        {id:1 , name:'ali'}
        {id:2 , name:'hasan'}
        {id:3 , name:'mahdi'}
    }
    removeCourse(course){
        let index = this.courses.indexOf(course);
        this.courses.splice(index,1);
    }
}
```
```
<ul>
    <li *ngFor="let course of courses; index as i"> // export index 
        {{i}} - {{course}} <button (click)="removeCourse(course)">Remove</button>
    </li>
</ul>
```
* can export `index`, `first`, `last`, `even` & `odd`

### TrackBy
use track by to better performance & not make dom every time
```
<botton (click)="loadCourse()">load</botton>
<ul>
    <li *ngFor="let course of courses; trackBy: trackCourse">
        {{i}} - {{course}}
    </li>
</ul>
```
```
export class mycomponent{
    courses;
    loadCourse(){
        this.courses = {
                {id:1 , name:'ali'}
                {id:2 , name:'hasan'}
                {id:3 , name:'mahdi'}
            }
    }
    trackCourse(index, course){
        return course ? course.id : undefined;
    } // track by id
}
```
* use only when need

### leading Astrisk
* the * before `ngIf`, `ngFor` & `ngSwitch` is means angular rewrite block with `ng-template` and put block in it
```
<div *ngIf="courses.length > 0">
    list of course
</div>
```
convert to
```
<ng-template [ngIf]="courses.length > 0">
    <div>
        list of course
    </div>
</ng-template>
```

### ngClass
```
<span class="glyphicon"
    [class.glyph-star]="isSelected" 
    [class.glyph-star-empty]="isSelected"
    ></span>
//or
<span class="glyphicon" 
    [ngClass]="{
        'glyph-star' : isSelected,
        'glyph-star-empty' : !isSelected
    }"
></span>
```

### ngStyle
```
<button
    [style.color]="canSave ? 'blue' : 'yellow'" 
    [style.fontWeight]="canSave ? 'bold' : 'normal'" 
    >submit</button>
//or
<button 
    [ngStyle]="{
        'color': canSave ? 'blue' : 'yellow',
        'fontWeight' : canSave ? 'bold' : 'normal'
    }"
>submit</button>
```

### safe Traversal Operator
* prevent error when object is null
```
<span>{{ user.job?.title }}</span>
```

### Custome Directive
Angular generate directive [directive-name]
```
ng g d input-format
```
* angularCli add app in front of directive name to prevent clash html attribute

```
import { Directive, HostListener, ElementRef } from '@angular/core'; //HostListener for hande dome event, ElementRef for reading value
@Directive({
    selector: 'appInputFormat'
})
export class InputFormatDirective{

    cunstructor(private el: ElementRef){} //dependencu injection

    @HostListener('fucus') onFucus(){
    }
    @HostListener('blure') onBlure(){
        let value = this.el.nativeElement.value;
    }
    
}
```
use
```
<input type="text" appInputFormat>
```

with sengding value
```
import { Directive, HostListener, ElementRef, Input } from '@angular/core'; //HostListener for hande dome event, ElementRef for reading value, Input for recieve value
@Directive({
    selector: 'appInputFormat'
})
export class InputFormatDirective{
    @Input('format') format;
    cunstructor(private el: ElementRef){} //dependencu injection

    @HostListener('fucus') onFucus(){
    }
    @HostListener('blure') onBlure(){
        let value = this.el.nativeElement.value;
        if(this.format == 'something')
        {

        }
    }
    
}
```
use
```
<input type="text" appInputFormat [format]="'something'">
```

* if we have only one variable we can use
```
<input type="text" [appInputFormat]="'something'">
```
```
...
@Input('appInputFormat') format;
...
```

### Template-Driven Forms
### ngModel
```
<form>
    <div class="form-group">
        <lable for="firstName">First Name</lable>
        <input required ngModel name="firstName" id="firstName" class="form-control" type="text">
        <div class="alert alert-danger" *ngif="firstname.touched && !firstName.valid">First Name is required</div>
    </div>
    <div class="form-group">
        <lable for="coment">Comment</lable>
        <textarea ngModel name="coment" id="coment"></textarea>
    </div>
</form>
```

* for see all change
```
<input required ngModel #firstName="ngModel" name="firstName" (change)="console.log(firstName);" id="firstName">
```

* can use other HTML5 validator such as `minlenght ='3'`, `maxlenght ='30'` or `pattern='banana'`.
```
<form>
    <div class="form-group">
        <lable for="firstName">First Name</lable>
        <input required minlenght ='3' ngModel name="firstName" id="firstName" class="form-control" type="text">
        <div class="alert alert-danger" *ngif="firstname.touched && !firstName.valid">
        <div *ngIf="firstName.error.required">First Name is required</div>
        <div *ngIf="firstName.error.minlength">First Name should be minimum 3 characters</div> //or minimum {{ firstName.error.minlength.requiredLenght }} 
        </div>
    </div>
    <div class="form-group">
        <lable for="coment">Comment</lable>
        <textarea ngModel name="coment" id="coment"  class="form-control"></textarea>
    </div>
</form>
```

* angular add class depend to validation roles
```
.form-control.ng-touched.ng-invalid{
    border: 2px solid red;
}
```

### ngForm
* if we have not `ngNoForm` or `formGroup` in form tag, angular add ngForm to it.
```
<form #f='ngForm' (ngSubmit)="console.log(f)">
...
<p>{{ f.value | json }}</p> //see all form value as json
<button class="btn btn-primary" [disabled]="!f.valid"></button> //validation depend on ngForm valid
</form>
```

### ngModelGroup
* use to categorise ngModels
```
<form>
<div ngModelGroup="contact">
...
</div>
...
</form>
```

* use Drop-down list
```
<select>
    <option *ngFor="let item of list" [value]=""item.id>{{ item.name }}</option>
</select>
```
for recieve everything use `ngValue`
```
<select>
    <option *ngFor="let item of list" [ngValue]=""item>{{ item.name }}</option>
</select>
```

### Reactive Form
#### Creating Control
* need to add `ReactiveFormModule` in app.moduls imports
```
import { FormGroup, FormControl, Validators } from '@angular/forms'
...
export class signupFormComponent{
    form = new FormGroup({
        userName: new FormControl('',[Validators.required, Validators.minlenght(3)]),
        password: new FormControl('',Validators.required),
    })

    get username(){ // for easiar access to form controll
        return this.form.get('userName');
    }
}
```
```
<form [formGroup]='form'>
...
    <input formControlName="userName" ...>
    <div *ngIf="form.get('userName').touched && username.invalid" //2way
    class="alert alert-danger">
        <div *ngIf="username.errors.required">...</div>
        <div *ngIf="username.errors.minlength">...</div>
    </div>
...
</form>
```
