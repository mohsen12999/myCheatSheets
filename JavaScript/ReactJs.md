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