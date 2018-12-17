# Express.js

* RESTful Services: Representational State Transfer
* CRUD Operations: Create, Read, Update, Delete
* HTTP Methods: GET: for getting data, POST: for creating data, PUT: for updating data, DELETE: fore delete data

[express website](expressjs.com)
[from mosh tutorial video](https://www.youtube.com/watch?v=pKd0Rpw7O48)

## make express project

```sh
mkdir express-demo
cd express-demo
npm init --yes
nom i express
```

## make first web server

index.js

```js
const express = require('express');
cons app = express();
app.get('/',(req,res) => {
    res.send('Hello World!');
});
// app.post()
// app.put()
// app.delete()
app.listen(3000, () => {
    console.log('Listenning on Port 3000')
})
```

// see in expressjs website -> API refrense -> Request

## nodemon

node monitor

```sh
npm i -g nodemon
```

* use `nodemon` to start application, if app change, it restart app.

## Enviroment variable

```js
const port = proccess.env.PORT || 3000;
app.listen(port,() => { console.log(`Listenning on Port ${port}`) });
```

* env variable mac: export PORT=5000
* env variable windews: set

## Route Parameter

```js
app.get('/api/courses/:id', (req, res) => {
    res.send(req.params.id);
    const course = courses.find(c => c.id === parsInt(req.params.id));
    if(!course) return res.status(404).send('the course not find');
    res.send(course);
    res.send(req.params); // read params /218/05/14
    res.send(req.query); // read query ?sort=name&filter=all
});
```

## POST

```js
app.use(express.json);//send jason to post
app.post('/api/courses',(req,res) => {
    const course = {
        id:courses.lenght +1 ;
        name: req.body.name
    };
    courses.push(course);
    res.send(course);
});
```

* for test post we can use `postman` extention for chrome

## Input Validation

```js
app.post('/api/courses',(req,res) => {
    if(!req.body.name || req.body.name.length<3) {
        // 400 bad request
        res.status(400).send('name is required and min 3 character');
        return;
        //return res.status(400).send('name is required and min 3 character');
    }
    const course = {
        id:courses.lenght +1 ;
        name: req.body.name
    };
    courses.push(course);
    res.send(course);
});
```

* JOI -> for validation input data

```sh
npm i joi
```

```js
const Joi = require('joi');
...
app.post('/api/courses',(req,res) => {
    const schema = {
        name:Joi.string().min(3).required()
    }
    const result = Joi.validate(req.body, schema);
    console.log(result);

    if(result.error) {
        // 400 bad request
        res.status(400).send(result.error);
        //res.status(400).send(result.error.detail[0].message);
        return;
    }
    const course = {
        id:courses.lenght +1 ;
        name: req.body.name
    };
    courses.push(course);
    res.send(course);
});
```

## Handling Put Request

```js
app.put('/app/courses/:id', (req, res) => {
    const course = courses.find(c => c.id === parsInt(req.params.id));
    if(!course) return res.status(404).send('the course not find');

    const schema = {
        name:Joi.string().min(3).required()
    }
    const result = Joi.validate(req.body, schema);
    if(result.error) {
        res.status(400).send(result.error);
        return;
    }

    course.name = req.body.name;
    res.send(course);
})
```

refactor code for validation

```js
function validateCourse(course)
{
    const schema = {
        name:Joi.string().min(3).required()
    }
    return Joi.validate(course, schema);
}
// const result = validateCourse(req.body);
// const { error } = validateCourse(req.body); // result.error
```

## Handling Delete Request

```js
app.delete('/app/courses/:id', (req, res) => {
    const course = courses.find(c => c.id === parsInt(req.params.id));
    if(!course) return res.status(404).send('the course not find');

    //delete
    const index = courses.indexOf(course);
    courses(index,1);

    res.send(course);
})
```