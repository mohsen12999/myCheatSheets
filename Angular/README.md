# Angular CheatSheet

"Udemy The Complete Angular Course Beginner to Advanced" from mosh hamedani video

## Install Component

### pre-install

`node -v`

`npm -v`

### install globaly

`npm install -g @angular/cli`

### make project name: my-app

`ng new my-app`

### run app

`cd my-app`

`ng serve --open`

--------------------------------------

## Type Script

### install type script

`npm install -g typescript`

### typescript version

`tsc --version`

### compile and get `main.js` and run

```ts

tsc main.ts
node main.js
//or
tsc main.ts && node main.js

```

### variables

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

### Type assertions

for having intellisence

```ts
let strLength: number = (<string>someValue).length;
let strLength: number2 = (someValue as string).length;
```

### Arrow Function

```ts
let log = (message) => console.log(message);
```

### Interface

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

### Class

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

### Modules

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

### Use Backtick

```ts
let user = {name:'mohsen',email='...'};
console.log(`Username is ${user.name}, email is ${user.email}`);
```

--------------------------------------

## Angular Fundamental

* Modules is some related component
* component Date + html + logic
  * creat component
  * register in modules
  * add element to html markup

### Creat Component

angularCli generate component course

`ng g c course`

### Template

```ts
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

`ng g s readlist`

* using service

```ts
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

```html
<h2>{{title}}</h2>
//or
<h2 [textContent]="text"></h2>

<img src="{{imageUrl}}">
//or
<img [src]="imageUrl">
```

* for element not in Dom like `colspan` use `[attr.colspan]`.

### Add Bootstrap

`npm install botstrap --save`

`save` flag add boorstrap as dependency in `package.json`

add bootstrap to global style file: `styles.css`

```ts
@import "~bootstrap/dist/css/bootstrap.css";
```

* `^3.4.7` (minor.minor.patch) means last version of 3

### Class Binding

```ts
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

```ts
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

```ts
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

```ts
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

```ts
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

```ts
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

```ts
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

```ts
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

#### Custome Pipe

angularCli generate pipe mypipe

`ng g c mypipe`

send variable to Pipe `{{ bigString | summary:40 }}`

```ts
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

#### Input Properties

for send information to component

```html
<mycomponent [isFavorite]="post.isfavorite"></mycomponent>
```

2 way for send

* first way

```ts
import {... , Input} from '@angular/core'
...
export class mycomponent{
    @input() isFavorite = false;
}
```

* second way

```ts
@component{(
    ...
    input:['isFavorite']
)}
export class mycomponent{
    isFavorite = false;
}
```

* Aliasing input

```html
<mycomponent [is-favorite]="post.isfavorite"></mycomponent>
```

can not define or use `is-favorite` as variable in typescript or javascript

```ts
export class mycomponent{
    @input('is-favorite') isFavorite = false;
}
```

#### Output Properties

for recieve

```html
<mycomponent (change)="onFavoriteChange()"></mycomponent>
```

```ts
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

```ts
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

```html
<mycomponent (change)="onFavoriteChange($event)"></mycomponent>
```

* Aliasing Output

```html
<mycomponent (change)="onFavoriteChange()"></mycomponent>
```

```ts
export class mycomponent{
    @output('change')  changeEvent = new EventEmitter();
}
```

### view Encapsulation

* `Shadow Dom` Allows us to apply scoped styles to elements without bleeding out to the outer world.

```ts
@Component({
  ...
  encapsulation: ViewEncapsulation.Emulated // angular try to emulate shadow dom
  //or
  encapsulation: ViewEncapsulation.Native // use directly shadow dom [not support by all browser] and not use other css from outside of shadow dom
})
```

#### ngContent

sending information to component
mypanel.component.html

```ts
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

```ts
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

```ts
<mypanel>
    <ngContainer class="headercontent"> header title </ngContainer>
    <ngContainer class="bodycontent">
        <h1>body</h1>
        <p>some thing ...</p>
    </ngContainer>
</mypanel>
```

### ngIf

```html
<div *ngIf="courses.lenght > 0"> // or function with true/false return
    courses list
</div>
<div *ngIf="courses.lenght == 0">
    no courses
</div>
```

or use `else` and `ng-template`

```html
<div *ngIf="courses.lenght > 0; else noCourse">
    courses list
</div>
<ng-template #noCourse>
    no courses
</ng-template>
```

or use `then`, `else` and `ng-template`

```html
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

```html
<div [hidden]="courses.lenght == 0"> // or function with true/false return
    courses list
</div>
<div [hidden]="courses.lenght > 0">
    no courses
</div>
```

### ngSwitch & ngSwitchCase

```ts
export class mycomponent{
    viewName;
}
```

```html
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

```ts
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

```html
<ul>
    <li *ngFor="let course of courses; index as i"> // export index
        {{i}} - {{course}} <button (click)="removeCourse(course)">Remove</button>
    </li>
</ul>
```

* can export `index`, `first`, `last`, `even` & `odd`

#### TrackBy

use track by to better performance & not make dom every time

```html
<button (click)="loadCourse()">load</button>
<ul>
    <li *ngFor="let course of courses; trackBy: trackCourse">
        {{i}} - {{course}}
    </li>
</ul>
```

```ts
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

#### leading Astrisk

* the * before `ngIf`, `ngFor` & `ngSwitch` is means angular rewrite block with `ng-template` and put block in it

```html
<div *ngIf="courses.length > 0">
    list of course
</div>
```

convert to

```html
<ng-template [ngIf]="courses.length > 0">
    <div>
        list of course
    </div>
</ng-template>
```

### ngClass

```html
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

```html
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

#### safe Traversal Operator

* prevent error when object is null

```html
<span>{{ user.job?.title }}</span>
```

#### Custome Directive

Angular generate directive [directive-name]

`ng g d input-format`

* angularCli add app in front of directive name to prevent clash html attribute

```ts
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

```html
<input type="text" appInputFormat>
```

with sengding value

```ts
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

```html
<input type="text" appInputFormat [format]="'something'">
```

* if we have only one variable we can use

```html
<input type="text" [appInputFormat]="'something'">
```

```ts
...
@Input('appInputFormat') format;
...
```

## Template-Driven Forms

### ngModel

```html
<form>
    <div class="form-group">
        <label for="firstName">First Name</label>
        <input required ngModel name="firstName" id="firstName" class="form-control" type="text">
        <div class="alert alert-danger" *ngif="firstname.touched && !firstName.valid">First Name is required</div>
    </div>
    <div class="form-group">
        <label for="coment">Comment</label>
        <textarea ngModel name="coment" id="coment"></textarea>
    </div>
</form>
```

* for see all change

```html
<input required ngModel #firstName="ngModel" name="firstName" (change)="console.log(firstName);" id="firstName">
```

* can use other HTML5 validator such as `minlenght ='3'`, `maxlenght ='30'` or `pattern='banana'`.

```html
<form>
    <div class="form-group">
        <label for="firstName">First Name</label>
        <input required minlenght ='3' ngModel name="firstName" id="firstName" class="form-control" type="text">
        <div class="alert alert-danger" *ngif="firstname.touched && !firstName.valid">
        <div *ngIf="firstName.error.required">First Name is required</div>
        <div *ngIf="firstName.error.minlength">First Name should be minimum 3 characters</div> //or minimum {{ firstName.error.minlength.requiredLenght }}
        </div>
    </div>
    <div class="form-group">
        <label for="coment">Comment</label>
        <textarea ngModel name="coment" id="coment"  class="form-control"></textarea>
    </div>
</form>
```

* angular add class depend to validation roles

```css
.form-control.ng-touched.ng-invalid{
    border: 2px solid red;
}
```

### ngForm

* if we have not `ngNoForm` or `formGroup` in form tag, angular add ngForm to it.

```html
<form #f='ngForm' (ngSubmit)="console.log(f)">
...
<p>{{ f.value | json }}</p> //see all form value as json
<button class="btn btn-primary" [disabled]="!f.valid"></button> //validation depend on ngForm valid
</form>
```

### ngModelGroup

* use to categorise ngModels

```html
<form>
<div ngModelGroup="contact">
...
</div>
...
</form>
```

* use Drop-down list

```html
<select>
    <option *ngFor="let item of list" [value]=""item.id>{{ item.name }}</option>
</select>
```

for recieve everything use `ngValue`

```html
<select>
    <option *ngFor="let item of list" [ngValue]=""item>{{ item.name }}</option>
</select>
```

## Reactive Form

### Creating Control

* need to add `ReactiveFormModule` in app.moduls imports

```ts
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

```html
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

### Custome Validate

define

```ts
import { AbstractControl, ValidationErrors } from '@angular/forms';

export class usernameValidators{
  static cannotContainSpace(control: AbstractControl): ValidationErrors | null{
    if((control.value as string).indexOf(' ') >= 0)
      return { cannotContainSpace: true };
    return null;
    // for minlength
    // return { minlength: { requiredLength:10 , actualLength: control.value.length }}
  }
}
```

use

```ts
...
userName: new FormControl('',[
    Validators.required,
    Validators.minlenght(3)
    usernameValidators.cannotContainSpace //because its static
    ])
```

* we can add validaton in `src/app/common/validators/`

### Asynchronouse Validators

* simulate asnc `setTimeout(()=>{console.log('time out'); },2000)`

define

```ts
static shouldBeUnique(control: AbstractControl): Promise<ValidationErrors | null> {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (control.value == 'mohsen1299')
          resolve({ cannotContainSpace: true });
        else
          resolve(null);
      }, 2000);
    })
  }
```

use

```ts
userName: new FormControl('',[
    Validators.required,
    Validators.minlenght(3)
    usernameValidators.cannotContainSpace //because its static
    ],
    usernameValidators.shouldBeUnique
    )
```

* we can use `pending` for waiting time

```html
<div *ngIf="username.pending">checking username uniqueness ..</div>
```

### Validation Form

```html
<form [formGroup]='form' (ngSubmit)="login()">
    <div *ngIf="form.errors">...</div>
...
```

```ts
login(){
    let valid = server.checkuser(this.form.value);
    if(!valid){
        this.form.setError({ invalidLogin: true})
    }
}
```

### Nested FormGroup

```ts
...
form = new FormGroup({
    account: new FormGroup({
        userName: new FormControl('',[Validators.required, Validators.minlenght(3)]),
        password: new FormControl('',Validators.required)
    )}
})

get username(){
    return this.form.get('account.userName');
}
...
```

```html
<form [formGroup]='form'>
    <div 'formGroup'='account'>
    ...
</form>
```

### Form Array

```ts

form = new FormGroup({
    topic: new FormArray([])
})
addTopic(topic: HTMLInputElement){
    (this.form.get('topic') as FormArray).push(new FormControl(topic.value));
    topic.value='';
}
removeTopic(topic: FormControl){
    let index = this.form.get('topic').indexOf(topic)
    this.form.get('topic').removeAt(index);
}
```

```html
<form [formGroup]='form'>
    <input type="text" class="form-control"
        (keyup.enter)="addTopic(topic)" #topic>
    <ul clss="list-group">
        <li
            *ngFor="let topic of form.get('topic').control"
            (click)="removeTopic(topic)"
            class="list-group-item">
            {{ topic.value }}
        </li>
    </ul>
</form>
```

### Form Builder

```ts
form = new FormGroup({
    name: new FormControl('', Validator.required),
    account: new FormGroup({
        username: new FormControl(),
        password: new FormControl()
    })
    topic: new FormArray([])
})
```

use form builder

```ts
form;
constroctor(fb: FormBuilder){
    this.form = fb.group({
        name:['', Validator.required],
        account: fb.group({
            username: [],
            password: []
        }),
        topic: fb.array([])
    })
}
```

## Http Service

* [`JSONPlaceholder`](https://jsonplaceholder.typicode.com/) Fake Online REST API for Testing and Prototyping Serving.

### Getting Data

* Add `httpModule`  to app.module imports

```ts
posts: any[];
constructor(http: Http){ // from '@angular/http'
    http.get('https://jsonplaceholder.typicode.com/posts')
        .subscribe(response => {
            this.posts= response.json();
        });
}
```

### Creating Data

```html
<input (keyup.enter)="creatPost(title)" #title ...>
```

```ts
posts: any[];
constructor(private http: Http){}
creatPost(input: HtmlInputElement){
    let postdata = { title: input,value };
    input.value = '';
    this.http.post('https://jsonplaceholder.typicode.com/posts',        JSON.stringify(postdata))
        .subscribe(response => {
            post['id'] = response.json().id;
            this.posts.splite(0,0,post)
        });
}
```

* better to call http in OnInit event
* `OnInit` is a lifecycle hook that is called after Angular has initialized a directive. call function => `ngOnInit`
* lifecycle hook: `OnInit`, `OnChange`, `Docheck`, `AfterContentInit`,...

### Updating Data

```html
<li *ngFor="let post in posts">
    <button (click)="updatePost(post)"></button>
    {{ post.title }}
    </li>
```

```ts
updatePost(post: HtmlInputElement){
    this.http.patch('https://jsonplaceholder.typicode.com/posts/' +     post.id, JSON.stringify({isRead: true}))
        .subscribe(response => {
                post['id'] = response.json().id;
                this.posts.splite(0,0,post)
            });
}
```

* `http.patch`use for update only few property in the object. only send the property should modify.

* `http.put` use for send object to server.

### Delete Data

```ts
DeletePost(post: HtmlInputElement){
    this.http.delete('https://jsonplaceholder.typicode.com/posts/' +    post.id)
        .subscribe(response => {
                let index = this.posts.indexOf(post);
                this.posts.splice(index,1);
            });
}
```

* `Sepration of Concern`: better to use service for calling server.

### Handeling Error

* Unexpected Errors: `Server is Offline`,`Network is down`, `Unhandled expections`.

```ts
...
.subscribe(response => {
        ...
    },error => {
        console.log(error); //see error
    });
...
```

* Expected: `Not Found` Errors (404), `Bad Request` Errors (400)

```ts
...
.subscribe(
    response => {
        ...
    },
    (error: Response) => {
        if(error.status == 404)
            console.log('this post already deleted');
        else
            console.log(error); //see error
        //if(error.status == 400)
            //this.form.setError(error.json())
    });
...
```

#### Throwing Specefic Errors

* can catch error in service

make error

```ts
//app/common/app-error.ts
export class AppError{
    constroctor(public originalError?: any){}
}
```

```ts
//app/common/not-found-error.ts
export class NotFoundError extend AppError{}
```

use in service

```ts
import  'rxjs/add/operator/catch';
import  'rxjs/add/Observable/throw';
...
deletePost(id){
    return this.http.delete(this.url+'/'+id)
        .catch((error: Response) =>{
            if(error.status == 404)
                return Observable.throw(new NotFoundError(error));
            return Observable.throw(new AppError(error));
        });
}
```

in component

```ts
...
.subscribe(
    response => {
        ...
    },
    (error: AppError) => {
        if(error instanceof NotFoundError)
            console.log('this post already deleted');
        else
            console.log(error); //see error
        //if(error.status == 400)
            //this.form.setError(error.json())
    });
...
```

### Global Error Handler

```ts
//app/common/app-error-handler.ts
export class AppErrorHandler implements ErrorHandler{
    handleError(error){
        // log
    }
}
```

* add in app.module providers

```ts
providers:[
    ... ,
    { provide: ErrorHandler, useClass: AppErrorHandler } //use AppErrorHandler instead of Error handler
]
```

use

```ts
(error: AppError) => {
        if(error instanceof NotFoundError)
            console.log('this post already deleted');
        else
            throw error;
    });
```

### reusable Error handling method

```ts
...
catch(this.handelError);
...
handelError(error){
    if(error.status == 400)
        this.form.setError(error.json())
    if(error instanceof NotFoundError)
        console.log('this post already deleted');
    else
        console.log(error); //see error
}
```

### Reusable Data service

define

```ts
export class DataService{
    constroctor(private url: string, private http: Http){}
    getAll(){ ... }
    create(resource){ ... }
    updete(resource){ ... }
    delete(id){ ... }
}
```

use

```ts
export class PostService extend DataService{
    constroctor(http: Http){
        super('url',http);
    }
}
```

### Map Operator

```ts
import 'rxjs/add/operator/map'
...
getAll(){
    return this.http.get(this.url)
        .map(response => response.json())
        .catch(this.handleError);
}

```

use

```ts
this.service.getAll()
    .subscribe(posts => this.post = posts);
```

* Optimistic (Hopefull) vs Pessimistic (Hopeless)

* obsevable : nothing happen until we have subscribe
* obsevables are lazy, Promise are eager
* `retry(3)` if obsevable fail, retry 3 time
* can alwayse convert observable to promise by `toPromise` operator.

## Routing

* configure the routes
* add a router outlet
* add link

### Configuring Routes

* add `RouterModule.forRoot()` to app.module imports.

```ts
RouterModule.forRoot([
    { path: '', component: HomeComponent }, // note use '/'
    { path: 'followers', component: FollowersComponent },
    { path: 'profile/:username', component: ProfileComponent },
    { path: '**', component: NotFoundComponent } // wildcart catch any route
])
```

* more specefic route must be higher. `products/:product` before `products`

### Router Outlet

* add `<router-outlet></router-outlet>` to app.module.html

### Router Link

* do not use `href` in link to refresh all page data, use `routerLink`.

```html
<a routerLink="/followers">...</a>
<a [routerLink]="['/followers' , follower.id]">...</a> // [ path, args ]
```

#### Router Active Link

```html
<a routerLinkActive="cssClass other-class" routerLink="/followers">...</a>
```

* add class "cssClass", "other-class" when we are in current link

### Getting Route Parameter

```ts
constroctor(private route: ActivatedRoute){}
ngOnInit(){
    this.route.paramMap
        .subscribe(params => {
            let username = param.get('username') //name set in route
            // for number: let id = +param.get('id')
        })
}
```

* `param.key` get all key send to param
* convert string to number with `+` => +string
* route param observable help us to change info without destroy component
* we can use `snapshot` if we 100% sure component destroy and creat (navigate somewhere else and back again)

```ts
ngOnInit(){
    let id = +this.route.snapshot.paramMap.get('id');
}
```

### Route with multiple Parameter

* 'profile/157/saeed'

```ts
{ path: 'profile/:id/:username', component: ProfileComponent }
```

```html
<a [routerLink]="['/profile' , profile.id, profile.username ]">...</a>
```

### Query Parameter

sending

```html
<a routerLink="/profile" [queryParams] ="{ page:1,  order: 'newest' }">...</a>
```

recieve

```ts
constroctor(private route: ActivatedRoute){}
ngOnInit(){
    this.route.queryParamMap
        .subscribe(params => {
            let username = param.get('username') //name set in route
        })
}
```

* we can use query and other in a component

### Subscribe to multiple Observable

```ts
import { observable } from 'rxjs/observable';
import 'rxjs/add/observable/combineLatest';
...
ngOnInit(){
    observable.combineLatest([
        this.route.paramMap,
        this.route.queryParamMap
    ]).subscribe( combine =>{
        let id = combine[0].get('id'); //paramMap
        let page = combine[1].get('page'); //queryParamMap

        //this.service.getAll({ id: id, page: page});
        this.service.getAll()
            .subscribe(folowers => this.flowers = flowers );
    });
}
```

### SwitchMap Operator

* solve problem subscribe in subscribe

```ts
import { observable } from 'rxjs/observable';
import 'rxjs/add/observable/combineLatest';
import 'rxjs/add/operator/map';
import 'rxjs/add/operator/switchMap';
...
ngOnInit(){
    observable.combineLatest([
        this.route.paramMap,
        this.route.queryParamMap
    ])
    .switchMap(combine =>{
        let id = combine[0].get('id');
        let page = combine[1].get('page');
        return this.service.getAll(); //subscribe method
    })
    .subscribe( folowers => this.flowers = flowers);
}
```

### Programmatic Navigation

```ts
constroctor(private router: Router){}

submit(){
    this.router.navigate(['/followes'],{
        queryParams: { page:1, order: 'newst' }
    }); //['path', args]
}
```

## Authentication and Authorization

* `JWT: JSON Web Token` save in local storage.
* we need to have in both the client and server. more info [`JWT`](https/jwt.io)
* JWT on clent: Dispaly current user name, show/hide part of page, prevent access to certain route

### Login

```ts
invalidLogin: boolean;
constructor(private router: Router, private authService: AuthService){}

signIn(credentials){
    this.authService.login(credentials)
        .subscribe(result => {
            if(result)
                this.router.navigate(['/']);
            else
                this.invalidLogin = true;
        })
}
```

```html
<form #f="ngForm" (ngSubmit)="signIn(f.value)">
...
<div *ngIf="invalidLogin"> invalid user/password </div>
```

we dont need to have observable function for login so we use `map`.
in service

```ts
login(credentials){
    return this.http.post('...',JSON.stringify(credentials)) // its observable
    .map(response => {
        let result = response.json();
        if(result && result.token){ // when login we have token
           localstorage.setItem('token',result.token);
           return true;
        }
        return false;
    })
}
```

* in chrome -> developer tools -> Application we can see local storage

### Logout

```html
<a (click)="authService.logout()">logout</a>
```

in service

```ts
logout(){
    localstorage.removeItem('token');
}
```

### Show or hide Element

install jwt
`npm install angular2-jwt --save`

in service

```ts
isLoggedIn(){
    let jwtHelper = new JwtHelper();
    let token = localStorage.getItem('token');
    if (!token)
        return false;

    let expirationDate = jwtHelper.getTockenExpirationDate(token);
    let isExpired = jwtHelper.isTokenExpired(token);

    return !isExpired;
}
// or only use
isLoggedIn(){
    return tockenNotExpired();
}
```

```html
<a *ngIf="authService.isLoggedIn()">log out</a>
```

#### Show or hide Element base on role

in service

```ts
get currentUser(){
    let token = localStorage.getItem('token');
    if (!token)
        return null;

    let jwtHelper = new JwtHelper();
    return jwtHelper.decodeTocken(ticken);
    //or
    return new JwtHelper().decodeTocken(ticken);
}
```

```html
<a *ngIf="authService.isLoggedIn() && authService.currentUser.admin">Admin Page</a>
```

### CanActivate Interface

* check route with auth-guard servise

```ts
export class AuthGuard implement CanActivate{
    constroctor(
        private router: Router,
        private authService: AuthService){}
    canActivate(){
        if(this.authService.isLoggedIn())
            return true;

        this.router.navigate(['/login']);
        return false;
    }
}
```

add auth-guard to app.module in provider and use in imports RouterModule.

```ts
RouterModule.forRoot([
    { path: '', component: HomeComponent },
    {
        path: 'admin',
        component: HomeComponent,
        canActive: [AuthGuardServise]
    }
    ...
])
...
provider:[
    ...
    AuthGuardServise
]
```

### Redirect User

```ts
export class AuthGuard implement CanActivate{
    constroctor(
        private router: Router,
        private authService: AuthService){}
    canActivate(route, state: RouteStateSnapeshot){
        if(this.authService.isLoggedIn())
            return true;

        this.router.navigate(['/login'],{ queryParams: { returnUrl: state.url });
        return false;
    }
}
```

in login componen

```ts
invalidLogin: boolean;
constructor(
    private router: Router,
    private route: ActivatedRoute,
    private authService: AuthService){}

signIn(credentials){
    this.authService.login(credentials)
        .subscribe(result => {
            if(result){
                let returnUrl = thise.route.snapshot.queryParamMap.get('returnUrl');
                this.router.navigate([returnUrl || '/']);
            }
            else
                this.invalidLogin = true;
        })
}
```

### Protecting Route Base One Users Role

* a service like auth-guard inmplement from `CanActivated`such as admin-auth-guard.

```ts
export class AdminAuthGuard implement CanActivate{
    constroctor(
        private router: Router,
        private authService: AuthService){}
    canActivate(){
        if(this.authService.currntUser && this.authService.currntUser.admin)
            return true;

        this.router.navigate(['/no-access']);
        return false;
    }
}
```

use in app.module

```ts
RouterModule.forRoot([
    { path: '', component: HomeComponent },
    {
        path: 'admin',
        component: HomeComponent,
        canActive: [AuthGuardServise, AdminAuthGuard]
    }
    ...
])
...
provider:[
    ...
    AuthGuardServise,
    AdminAuthGuard
]
```

### Accessing Protected API

in service

```ts
import { AuthHttp } from 'angular2-jwt'
import { Http, RequestOption, Headers } from '@angular/http';
import 'rxjs/add/operator/map'
...
constroctore(private http: Http,private authHttp: AuthHttp){}
getOrder(){
    // when use Http
    //let header = new Header();
    //let token = localStorage.getItem('token');
    //header.append('Authorizaion','Bearer' + token);
    //let options = new RequestOption({ headers: headers })
    //return this.http.get('url', options)
        //.map(response => response.json());

    //when use AuthHttp
    return this.authHttp.get('url')
        .map(response => response.json());
}
```

## Deployment

* Optimization technices
  * Minification: remove all comment and white space.
  * Uglification: rename long descriptive variable and function to little one.
  * Bundling: combine file to one file.
  * Dead code elimination: delete the code that not use.
  * Ahead-of-time (AOT) compilation: pre-compile angular component.

do all that in: `ng build -prod`

### JIT vs AOT

* JIT compilation problem:
  * Inefficient for production
  * Happens for every user
  * More components, slower
  * We have to ship Angular compiler

* AOT compilation bebefits:
  * Faster startup
  * Small bunle size
  * Catch template error earlier
  * Better security

### Angular compiler

* see version in pavkage.json dependency '@angular/cmpiler'.

run compiler from moduls: `node_modules/.bin/ngc`
send nothind if we have not any error

### Building Aplication with Angular Cli

if use `ng build` -> compile without optimization.

`ng build --prod`: make 'dist' folder. folder name with hash number for each change to prevent cach them in browser.

### Enviroment

* Enviroment like Deployment, Test, Production.
* in 'src/enviroment/': 'enviroment.prod.ts' for production, 'enviroment.ts' for development.
* for show us the enviroment, and prevent any change in production enviroment.
* we can add variable to each enviroment

use in component:

```ts
import { enviroment } from './../../enviroments/enviroment' //not enviroment.prod
...
backgroungColor = enviroment.production;
```

* `ng serve` default run in develop enviroment. for product enviroment `ng serve --prod` or `ng serve --enviroment=prod`

#### Add custom Enviroment

make new enviroment file like 'enviroment.test.ts'
register in angular-cli.json -> inviroments

```json
"inviroments":{
    "test": "enviroments/enviroment.test.ts"
}
```

use `ng serve --enviroment=test` or `ng build --enviroment=test`.

* only in develpment enviroment change immedietly can see in browser.

### Linter

#### Linter with Angular Cli

* programs roles like [`tslint`](https://github.com/plantir/tslint)
* install by default in angular. see 'package.json'
* run tslint `ng lint` and see errors.
* for find and fix error run `ng lint --fix`

#### Linter with VSCode

install TSLint extention for VScode

* See all problem in page
* use `ctrl+shift+p` for command pallet and type T`TSLint:Fix all auto-fixable problems`.

### Deployment Option

* Github Page: no back-end.
* Firebase: as backend.
* Heroku: custome backend.

#### Deploying to GitHub Pages

* first deployment
  * Create GitHub Repository
  * connect to project `git remote add origin http://github/somting.git`
  * send project `git push origin master`
  * install node package for deploy our app `npm i -g angular-cli-ghpages`
  * build project for github `ng build --prod --base-href="https://mohsen1299.github.io/repositoryname/"`
  * run `angular-cli-ghpages` or `ngh`

* other deployment
  * `ng build --prod --base-href="https://mohsen1299.github.io/repositoryname/"`
  * `ngh`

or in package.json onther the script add command

```json
"scrips": {
    "deploy:gh": "ng build --prod --base-href='https://mohsen1299.github.io/repositoryname/' && ngh"
}
```

and use `npm run deploy:gh`

#### Deploying to Firebase

* provide by google for backend mobile/web app
* go to [firebase](https://console.firebase.google.com) and add project
* install firebase tool: `npm install -g firebase-tools`
* login to fire base: `firebse login`
* in project folder: `firebase init` and select hosting after than select project name
* in firebase.json

```json
{
    "Hosting": {
        "public": "dist",
        "rewrites": [
            {
                "source": "**",
                "destination": "index.html"
            }
        ]
    }
}
```

* run `ng build --prod`
* deploy with `firebase deploy` and get app address
* can add `"deploy:firebase": 'ng buil --prod && firebase deploy'` to package.json -> scripts. and use `npm run deploy:firebase`

#### Deploying to Heroku

* go to [Heroku](https://www.heroku.com/) and add project
* search for Heroku-cli, and download and install it, check `heroku --version`
* login with `heroku login`
* create heroku app with `heroku creat [app-name]` or `heroku creat` (and heroku generate a name) and get address
* go to app page `heroku open`
* in package.json:
  * move 'angular/cli' & 'angular/compiler-cli' & 'typescript' from devDependencies to dependencies.
  * add `"postinstall": "ng build --prod"` in scripts
  * chande `"start": "ng server.js"`
* add express to dependency `npm i express --save`
* `git add .` & `git commit -m "prepare for Heroku"`
* `git push heroku master`
* `heroku open` to see app

* if hade probelem we can set engine for heroku in package.json:

```json
{
    "engines": {
        "node": "6.10.3", // our machin version
        "npm": "5.3.0"
    }
}
```

### Building Real-time Server-less Apps with Firebase

* Fast, scalable and real-time database in the cloud
* Authentication
* Cloud messaging
* Storage
* Analytics

#### Firebase project

* go to [firebase console](console.firebase.google.com) and add project.
* firebase database in NOSQL database, thats like tree of node
* make project `ng new firebase-demo`
* `cd firebase-demo` & `npm install firebase angularfire2 --save`
* in firebase project page go to 'add fire base to your app' copy all config property like `appkey` to out project enviroment.ts -> firebase

```ts
export const enviroment = {
    production: false,
    firebase:{
        apikey: '',
    }
}
```

* in app.module.ts

```ts
import { enviroment } from './../../enviroments/enviroment'
import { AngularFireModule } from 'angularfire2'
import { AngularFireDatabaseModule } from 'angularfire2/database'
...
imports:{
AngularFireModule.initializedApp(enviroment.firebase),
AngularFireDatabaseModule
}
```

#### Read from Firebase Database

* need to change role in project page and change `"read": true`

```ts
import { AngularFireDatabase } from 'angularfire2/database'
...
courses: any[];
constroctor(db: AngularFireDatabase){
    db.list('/courses')
        .subscribe(courses => {
            this.courses = courses;
        })
}
```

* firebase database is real time, change reflected in app immedietly. very good for chat app. sometime its make memory leak for records change that does not see in client.

#### Unsubscribe from Subscription

```ts
expot class AppCompoment implements onDestroy{
    courses: any[];
    subscription: Subscription;

    constroctor(db: AngularFireDatabase){
        this.subscription = db.list('/courses')
            .subscribe(courses => {
                this.courses = courses;
            })
    }
    ngOneDestroy(){
        this.subscription.unsubscribe();
    }
}
```

#### Async Pipe

async get latest value and subscribe when component destroy unsubscribe.

```ts
expot class AppCompoment{
    courses$; // $ means its observable

    constroctor(db: AngularFireDatabase){
        this.courses$ = db.list('/courses');
    }
}
```

use

```html
<li *ngFor="let course of courses$ | async"> ...</li>
```

#### Reading an Object

```ts
expot class AppCompoment{
    courses$; // $ means its observable
    course$;

    constroctor(db: AngularFireDatabase){
        this.courses$ = db.list('/courses');
        this.course$ = db.object('/courses/1');
    }
}
```

```html
<p> {{ course$ | async | json }} </p>
<p> {{ (course$ | async).title | json }} </p>
```

#### As Keyword

```html
<ul *ngIf="author$ | async as author">
    <li> {{ author.name }}</li>
    <li> {{ author.age }}</li>
</ul>
```

#### Add Object

* need to change role in fire base console `".write":true`

```html
<input type="text" (keyup.enter)="add(course)" #course >
```

```ts
expot class AppCompoment{
    courses$: FirebaseListObservable<any[]>; // $ means its observable

    constroctor(db: AngularFireDatabase){
        this.courses$ = db.list('/courses');
    }

    add(course: HtmlInputElement){
        this.courses$.push(course.value);
            //.then({})
        course.value='';
    }
}
```

#### Update Object

```html
<li *ngFor="let course of courses$ | async"> ...
    <button (click)="update(course)">update</button>
</li>
```

```ts
constroctor(this db: AngularFireDatabase){
    this.courses$ = db.list('/courses');
}

update(course){
    this.db.object('/courses/' + course.$key)
        //.set(course.$value + ' updated');
        //.set({title: course.$value + ' updated', price:150});
        .update({title: course.$value + ' updated', price:150});
}
```

* set change object exactly to new thing, but update change exist and add new thing not delete any thing.

#### Remove Object

```ts
delete(course){
    this.db.object('/courses/' + course.$key)
        .remove();
}
```

* other work with firebase: Joining, Check for existence of an object, Sorting, Filterng, Indexing, Limiting, Multiple updates, Authentication, Facebook Login

## Animation

* two way to creat animation: `css`, `javascript`
  * `css`: limit control, suitable for simple, one shote animations
  * `javascript`: `jQuery`, `GSAP`, `Zepto`, `Web Animation API`
* recommend: `Web Animation API` for animate dom element and support natively in chrome, firefox & opera.
* `@angular/animations` amodules top of standard `Web Animation API`.
* [`CanIUse`](https://caniuse.com/) for check support browser
* css animation: `transient`, `animation`
* can use `animate.css`

## Angular Animations

* `@angular/animations`: trigger(), transition(), state(), animate(), ...
* States: void, default(*) & custom.
  * void: not part of DOM. creat from outside or remove element.
* `Polyfill` allow to use modern javascript feature in old browser.

### Import the Animation Module and Polyfills

* in app.mudule.ts

```ts
import { BrowserAnimationModule } from '@angular/platform-browser/animation';
...
import:[
    BrowserAnimationModule
]
```

* in src/polyfills.ts in line 40,41 uncomment `import web-animation-js;`
* in terminal: `npm install web-animation-js --save`

### Implement Animation

```ts
import { trigger } from '@angular/animation';
....
@component({
    ...
    animation: [
        trigger('fade',[
            //state(),
            transition('void => *',[
                style({ backgroundColor: 'yellow',opacity: 0 }), // in transient time
                animate(2000, style({ backgroundColor: 'white',opacity: 1 }))) //at the end after 2 sec
                // animate(2000) //undo all style at the end
            ]), //fade-in effect

            transition('* => void',[
                animation(2000,{ opacity: 0})
            ]) //fade-out effect

        ])
    ]
})
```

```html
<button @fade></button>
```

### States

```ts
....
@component({
    ...
    animation: [
        trigger('fade',[
            state('void', style({ opacity: 0})),

            transition('void => *',[
                // no need style { opacity: 0}
                animate(2000)
            ]),

            transition('* => void',[
                animate(2000) //no need { opacity: 0}
            ])

            //or
            //transition('void => *, * => void',[ //or 'void <=> *'
            //    animate(2000)
            //])
        ])
    ]
})
```

### Transition

* `void => *` and `* => void` equel to `void => *, * => void` or `void <=> *`
* `void => 0`: `:enter`
* `* => void`: `:leave`

### Reusable Triggers

animate.ts

```ts
import { trigger, transition, state, style, animate } from '@angular/animation';
export fade = trigger('fade',[
            state('void', style({ opacity: 0})),
            transition(':enter, :leave',[
                animate(2000)
            ])
        ])
```

use

```ts
import { fade } from './animate.ts'
....
@component({
    ...
    animation: [
        fade
    ]
})
```

### Easing

```ts
transition(':leave',[
    animate(500, style({ transform: 'translateX(-100%)'}))
   ])
```

* we can use string for time: 'duration [delay] [easing]'
  * duration and delay: '500ms', '.5s'
  * Easing: a function that determines the speed of animation over time.
    * Linear: same speed
    * Ease-in: start slow, end fast
    * Ease-out: start fast, end slowly
    * Ease-in-out: start slow, middle fast, end slowly
    * Cubic Bezier: for custom easing like 'cubic-bezier(.17, .67,.17, .67)'. [online tool for design cubic-bezier](cubic-bezier.com)

### Keyframes

```ts
transition(':leave',[
    animate(500, keyframes([
        style({ offset: .2, opacity: 1, transform: 'translateX(20px)' }),
        style({ offset: 1, opacity: 0, transform: 'translateX(-2000px)' })
    ]))
   ])
```

### Reuse Animations

animate.ts

```ts
export let bounceOutLeftAnimation = Animation(
    animate(500, keyframes([
        style({ offset: .2, opacity: 1, transform: 'translateX(20px)' }),
        style({ offset: 1, opacity: 0, transform: 'translateX(-2000px)' })
    ]))
)
```

use

```ts
...
transition(':leave',[
    style({ backgroundColor: 'red'}),
    animate(1000),
    useAnimation(bounceOutLeftAnimation)//after changing bg to red in 1 sec, this start
])
```

### Parametrize Reuse Animations

```ts
export fadeInAnimation = animation([
    style({ opacity: 0})
    animate('{{ duration }} {{ easing }}')
],{
    params: {
        duration: '2s', // default value for duration
        easing: 'ease-out' // default value for ease functoin
    }
})

export fade = trigger('fade',[

    transition(':enter',
        useAnimation(fadeInAnimation,{
            params: {
                duration: '500ms'
            }
        })
    ),

    transition(':leave',[
        animate(2000,style({ opacity: 0}))
    ])
])
```

### Animation Callbacks

```html
<button type="button"
    @todoAnimation
    (@todoAnimation.start)="animationStarted($event)"
    (@todoAnimation.done)="animationDone($event)"
    ></button>
```

component

```ts
animationStarted($event){}
animationDone($event){}
```

### Querying Child Element with query

```html
<div @todosAnimation>
    <h1>Todos</h1>
    <input />
</div>
```

```ts
@component({
    animations:[
        trigger('todosAnimation',[
            transition(':enter',[
                query('h1',[
                    style({ transform: 'translateY(-20px)' }),
                    animate(1000)
                ])
            ])
        ])
    ]
})
```

* Pseudo-selectors tockens
  * query(':enter'), query(':leave'): for child enter or leave
  * query(':animating'): when child animating
  * query('@trigger'): for trigger [name: triger] triggerd
  * query('@*'): all animation when triggerd
  * query(':self')

### Querying Child Element with animateChild

* parent animation block child animations

```ts
@component({
    animations:[
        trigger('todosAnimation',[
            transition(':enter',[
                query('h1',[
                    style({ transform: 'translateY(-20px)' }),
                    animate(1000)
                ]),
                query('@todoAnimation', animateChild()) // select trigger name @todoAnimation
            ]) // first do h1 and after that child
        ])
    ]
})
```

### Parallel Animation with group

```ts
transition(':enter',[
    group([
        query('h1',[
            style({ transform: 'translateY(-20px)' }),
            animate(1000)
        ]),
        query('@todoAnimation', animateChild())
    ]) // do is same time
])
```

```ts
transition(':enter',[
    group([
        animate(1000, style({ background: 'red' })),
        animate(2000, style({ transform: 'translateY(50px)' })) // 2 animate at same time
    ])
])
```

### Stagger

```ts
trigger('todosAnimation',[
    transition(':enter',[
        query('h1',[
            style({ transform: 'translateY(-20px)' }),
            animate(1000)
        ]),
        query('@todoAnimation', stagger(200, animateChild())) // add 200ms delay for every child animation
        //or query('@todoAnimation', stagger(200, useAnimation(fadeINAnimation))
        //or query('.list-group-item', stagger(200, [ style({ transform:'translateX(-20px)' }), animate(1000) ]) // do it only for making parent and not do for making child
    ])
])
```

### Custom States

```html
<div [@expandCollapse]="isExpanded ? 'expanded' : 'collapse'" class="zippy-body" [hidden] = "!isExpanded">
```

```ts
animation:[
    trigger('expandCollapse',[
        state('collapsed', style({
            height: 0,
            padding: 0,
            overflow: 'hidden'
        })),
        state('expanded', style({
            height: '*', //angular fill it dynamicly at runtime
            padding: '*',
            overflow: 'auto'
        })),
        transition('collapse => expanded', [
            animate('300ms ease-out')
        ]),
        transition('expanded => collapse', [
            animate('300ms ease-in')
        ])
    ])
]
```

### Multi-step Animation

```ts
trigger('expandCollapse',[
    state('collapsed', style({
        height: 0,
        paddingTop: 0,
        paddingBottom: 0,
        opacity: 0
    })),
    transition('collapse => expanded', [
        animate('300ms ease-out',style({
            height: '*',
            paddingTop: '*',
            paddingBottom: '*',
        })),
        animate('1s',style({
            opacity: 1
        }))
    ]) // first expand and second show data
])
```

### Sepration of Consern

zippy.component.animation.ts

```ts
export const expandCollapse = trigger(...)
```

use

```ts
@Component({
    animation:[ expandCollapse ]
})
```

## Angular Material

Material Design components for Angular, [Home Page](https://material.angular.io/), [github Page](https://github.com/angular/material2), [Getting started](https://material.angular.io/guide/getting-started)

* Angular Material Components
  * Internationalized
  * Clean and Simple API
  * Well-tested
  * customizable
  * fast
  * Well-documented

### install Angular Material

```sh
npm install --save @angular/material @angular/cdk @angular/animations
```

* `hammerjs` powerfull libery for Add multi-touch gestures to site.

### Add Theme

* include theme is in project > node_modules > @angular > material > prebuild-themes.
* for Add Theme: in styles.css

```css
@import "~@angular/material/prebuild-themes/indego-pink.css";
```

* in app.module.ts

```ts
import { BrowserAnimationModule } from '@angular/platform-browser/animations'; // if want to use animation
import { NoopAnimationModule } from '@angular/platform-browser/animations'; // if dont want to use animation

import:[
    BrowserAnimationModule,
    // or NoopAnimationModule
]
```

* for use every component of Angular Material, must to import its modules in app.module.ts

### CheckBox

* use `md-checkbox` tag & import `mdCheckboaModule` to app.module

```html
<md-checkbox #showDetail
    [value]="" [checked]="isChecked" (change)="onChange($event)" >Show Detail</md-checkbox>
    <div *ngIf="showDetail.checked">Some Detail</div>
```

### Radio Button

* need to import `MatRadioModule` to app.module

```html
<mat-radio-group>
  <mat-radio-button value="1">Male</mat-radio-button>
  <mat-radio-button value="2">Female</mat-radio-button>
</mat-radio-group>
```

### Selects

* need to import `MatSelectModule` to app.module

```html
<mat-form-field>
  <mat-select placeholder="Favorite food">
    <mat-option *ngFor="let food of foods" [value]="food.value">
      {{food.viewValue}}
    </mat-option>
  </mat-select>
</mat-form-field>
```

### Input

* need to import `MatInputModule` to app.module

```html
<mat-form-field class="example-full-width">
    <input matInput placeholder="Favorite food" value="Sushi">
</mat-form-field>
```

### Text Areas

```html
<mat-form-field class="example-full-width">
    <textarea matInput placeholder="Leave a comment"></textarea>
</mat-form-field>
```

### datepicker

* need to import `MatDatepickerModule` to app.module

```html
<mat-form-field>
  <input matInput [matDatepicker]="picker" placeholder="Choose a date">
  <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
  <mat-datepicker #picker></mat-datepicker>
</mat-form-field>
```

* better UI for mobile: `touchUi=true`.

### Icons

* see [material icon](https://material.io/icons/)
* add to `styles.css`:

```css
@import "https://fonts.googlepis.com/icon?family=Material+Icons";
```

* add `MdIconModule` to app.module
* omport icon by icon name (underline for space in name).

```html
<md-icon></md-icon>
```

### Button

* add `MdButtonModule` to app.module

```html
<button mat-button>Click me!</button>
<button mat-rased-button>Click me!</button>
```

### Chips

* add `MdChipsModule` to app.module

```html
<mat-chip-list>
  <mat-chip>One fish</mat-chip>
  <mat-chip>Two fish</mat-chip>
  <mat-chip color="primary" selected>Primary fish</mat-chip>
  <mat-chip color="accent" selected>Accent fish</mat-chip>
</mat-chip-list>
```