# React

make a new project

```sh
npm install -g create-react-app
create-react-app my-app
cd my-app
npm start
```

[Tutorial: Intro to React](https://reactjs.org/tutorial/tutorial.html)

`npm start`: Starts the development server.

`npm run build`: Bundles the app into static files for production.

`npm test`: Starts the test runner.

`npm run eject`: Removes this tool and copies build dependencies, configuration files and scripts into the app directory. If you do this, you can’t go back!

## Mosh

* React: a JavaScript library for building user interface
* Component: a piece of user interface
  * javascript class with `state`:data and `render`:method
  * output of render is React element, a simple javascript element for virtual dom
* install nodejs
* `npm i -g create-react-app`
* add extention for vscode
  * simple React Snippets -> shortcut like imrc (import react componrnt) & cc (class component)
  * prettier-code formatter -> goto file -> perferences -> setting -> usersetting -> "editor.formatOnsetting": true
* `create-react-app [app-name]`
* `npm start`
* babel is a compiler for jsx (javascript xml) [babel compiler online](https://babeljs.io/repl)

### Hello World

* in src -> index.js

```js
import React from 'react';
import ReactDom from 'react-dom';
cons ele = <h1>Hello Worls!</h1>;
ReactDom.render(ele, document.getElementById('root'));
```

### First component

* install bootstrap: `npm i bootstrap`
* import in index.js: import `import 'bootstrap/dist/css/bootstrap.css'`
* in src make folder 'components' -> counter.jsx
  * use imrc & cc to create component
* import component in index.js
* jsx need to have one parent element, we can use `React.Fragment` tag fir it

```jsx
class Counter extends Component {
    state = {
        count = 1;
    };
    render() {
        return (
            <div>
                <span>{ this.state.count }</span>
                <span>{ this.formatCount() }</span>
                <button>increase</button>
            </div>
        );
    }
    formatCount() {
        //return this.state.count === 0 ? 'zero':this.state.count;
        const { count } = this.state;
        //return count === 0 ? 'zero':count;
        return count === 0 ? <h1>Zero</h1>:count;
    }
}
```

* can not use 'class' in jsx -> className

```jsx
styles = {
    fontSize: 10 ,//or '10px'
    fontWeight: bold
}
render() {
    return (
        <div>
            <span style={this.styles} className="badge">{ this.formatCount() }</span>
            <button style={{fontSize: 20}}>increase</button>
        </div>
    );
}
```

### render class dynamicly

```jsx
render() {
    let classes = "badge m-2 bagde-";
    classes += (this.state.count === 0)?"warning":"primary";
    return (
        <div>
            <span style={this.styles} className={classes}>{ this.formatCount() }</span>
            <button style={{fontSize: 20}}>increase</button>
        </div>
    );
}
```

* select line -> right click -> refactor...

### Rendering List

```jsx
state = {
    tags: ['tag1','tag2','tag3']
}
render() {
    return (
        <ul>
            { this.state.tag.map(tag => <li key={tag}>{ tag }</li>) }
        </ul>
    );
}
```

* condition

```jsx
renderTag(){
    if(this.state.tags.length == 0){
        // return 'no tag!';
        // return null;
        return <p>there are no tag</p>;
    }
    return <ul>{ this.state.tag.map(tag => <li key={tag}>{ tag }</li>) }</ul>
}
```

* one way condition in javascript 'true && "hi"'->"hi"

```jsx
render() {
    return (
        { this.state.tags.length == 0 && <p>there are no tag</p>} // render tag when array empty
    )
}
```

### Handle Event

```jsx
// first way
// constroctor() {
//     super();
//     this.handleIncreament = this.handleIncreament.bind(this);
// }
// handleIncreament() {}
// new way
handleIncreament = () => {
    this.setState({ count: this.state.count+1 })
}
render() {
    return (
        <div>
            <span >{ this.state.count }</span>
            <button onClick={ this.handleIncreament }>increase</button>
        </div>
    );
}
```

### Passing Event Arg

```jsx
handleIncreament = (arg) => {
    this.setState({ count: this.state.count + 1 });
}
// doHandleIncreament = () => {
//     this.handleIncreament({ id: 1 });
// }
render() {
    return (
        <div>
            <span >{ this.state.count }</span>
            <button onClick={ this.doHandleIncreament }>increase</button>
            <button onClick={ () => this.handleIncreament({ id: 1 }) }>increase</button>
        </div>
    );
}
```

### Compose Component

* counters component

```jsx
state = {
    counters: [
        { id: 1, value: 0 }
        { id: 2, value: 0 }
        { id: 3, value: 0 }
        { id: 4, value: 0 }
    ]
}
render() {
    return (
        <div>
            { this.state.counters.map(counter => <Counter key="counter.id" value="counter.value" />) }
        </div>
    );
}
```

* counter component

```jsx
state = {
    count: this.props.value
}
render() {
    return (
        <div>
            { this.state.counters.map(counter => <Counter key="counter.id" value="counter.value" selected="true" />) }
        </div>
    );
}
```

### Passing Children

send information between tags -> `this.props.children`

```jsx
<Counter>
    <h4>title</h4>
</Counter>
```

### Debugging React App

* React Developer Tools for browser -> new tab in developer tool
* `$r` -> instanse of first component in debugger

### Prop vs State

* state is local
* props is read only

* the component that own a piece of state, should be the one modifying it.

### Assign Event handler

in Counters

```jsx
handleDelete = counterId => {
    const counters = this.state.counters.filter(c => c.id !== counterId);
    // this.setState({ counters: counters});
    this.setState({ counters });
}
render() {
    return(
        <Counter onDelete={ this.handleDelete } />
    )
}
```

in Counter

```jsx
render() {
    return(
        <button onClick={ () => this.prop.onDelete(this.prop.id) } ></button>
    )
}
```

### Remove local State

* reset button

```jsx
onReset = () => {
    const counters = this.state.counters.map(c => {
        c.value = 0;
        return c;
    });
    this.setState({ counters });
}
```

* but child element not change, need to remove their state
