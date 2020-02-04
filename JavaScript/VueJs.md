# Vue JS

## Vue CLI

[Vue CLI](https://cli.vuejs.org/)

* Install `npm install -g @vue/cli`
* Create project `vue create hello-world` or `vue ui`
* Run => `vue serve`
* Build => `vue build`
* Installing Plugins in an Existing Project: `vue add @vue/eslint`

## Veu data

```html
<div id="root">
  {{greeting}}
<div>

<script>
  new Vue({
    el:'#root', // required
    data: {
      greeting: 'hello world!'
    }
  })
</script>
```

## Vue model

```html
<div id="root">
  <h1>{{greeting}}</h1>
  <input v-model="greeting">
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      greeting: 'hello world!'
    }
  })
</script>
```

## Vue if

* if not true -> dont render ele

```html
<div id="root">
  <div v-if="count === 1">
    Green
  </div>
  <div v-if="count === 2">
    Red
  </div>
  <div v-else>
    Orange
  </div>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      count: 0
    }
  })
</script>
```

## Vue show

* if not true -> render element but not show (display:none)
* sometime better for performance

```html
<div id="root">
  <div v-show="count === 1">
    Green
  </div>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      count: 0
    }
  })
</script>
```

## Vue bind

* can write `vbind:...` -> `:...`

```html
<div id="root">
  Sign Up
  <br>
  <input v-model="email">
  <br>
  <button onclick="alert('sing out')" :disabled="email.length<2">
    Submit
  <button>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      email: ''
    }
  })
</script>
```

```html
<style>
  .red {
    border: 2px solid red;
  }
  .green {
    border: 2px solid green;
  }
</style>

<div id="root">
  Sign Up
  <br>
  <input v-model="email" :class="{red: email.lenght < 2}">
  <input v-model="email2" :class="[email2.lenght < 2? 'red':'green' ]">
  <br>
  <button onclick="alert('sing out')" :disabled="email.length<2">
    Submit
  <button>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      email: '',
      email2: ''
    }
  })
</script>
```

## Vue text

```html
<div id="root">
  <h1 v-text="greeting"></h1>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      greeting: 'hello world!'
    }
  })
</script>
```

## Vue html

```html
<div id="root">
  <h1 v-html="greeting"></h1>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      greeting: '<span>sds</span>'
    }
  })
</script>
```

## Vue once

* `v-once` make static html and not change

```html
<div id="root">
  <p v-once>{{email}}</p>
  <p>{{email}}</p>
  <br>
  <input v-model="email" :class="{red: email.lenght < 2}">
  <br>
  <button onclick="alert('sing out')" :disabled="email.length<2">
    Submit
  <button>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      email: 'sample@mail.com'
    }
  })
</script>
```

## Vue for

```html
<div id="root">
  <ul>
    <li v-for="cat in cats">{{ cat }}</li>
  </ul>
  <ul>
    <li v-for="people in peoples">{{ people.name }}</li>
  </ul>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      cats: ['kitkat','fish','henry'],
      name: [{name:'ali'},{name:'saeed'},{name:'hamid'}]
    }
  })
</script>
```

## Vue on

* can use `v-one:...` -> `@...` 

```html
<div id="root">
  <input v-model="newCat" v-on:keyup.enter="addKitty">
  <button v-on:click="addKitty">
    + Add
  </button>
  <ul>
    <li v-for="cat in cats">{{ cat }}</li>
  </ul>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      cats: [{name:'kitkat'},{name:'fish'},{name:'henry'}],
      newCat: ''
    },
    methods: {
      addKitty: function() {
        this.cats.push({ name:this.newCat})
        this.newCat=''
      }
    }
  })
</script>
```

* `@click.prevent` -> prevent defalut
* `@click.stop` -> stop propegation
* `@click.prevent.stop`

## Vue filter

```html
<div id="root">
  <input v-model="newCat" @keyup.enter="addKitty">
  <button @click="addKitty">
    + Add
  </button>
  <ul>
    <li v-for="cat in cats">{{ cat | capitalize | kittify }}</li>
  </ul>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      cats: [{name:'kitkat'},{name:'fish'},{name:'henry'}],
      newCat: ''
    },
    methods: {
      addKitty: function() {
        this.cats.push({ name:this.newCat})
        this.newCat=''
      }
    },
    filters: {
      capitalize: function(value) {
        return value.toUpperCase()
      },
      kittify: function(value) {
        return value+'y'
      }
    }
  })
</script>
```

## Vue computed

* return new variable by computing

```html
<div id="root">
  {{ kittifyName }}
  <input v-model="newCat" @keyup.enter="addKitty">
  <button @click="addKitty">
    + Add
  </button>
  <ul>
    <li v-for="cat in cats">{{ cat  }}</li>
  </ul>
<div>

<script>
  new Vue({
    el:'#root',
    data: {
      cats: [{name:'kitkat'},{name:'fish'},{name:'henry'}],
      newCat: ''
    },
    methods: {
      addKitty: function() {
        this.cats.push({ name:this.newCat})
        this.newCat=''
      }
    },
    computed: {
      kittifyName: function() {
        if(this.newCat.length > 1) {
          return this.newCat + 'y'
        }
      }
    }
  })
</script>
```

## Vue component

```html
<div id="root">
  <input v-model="newCat" @keyup.enter="addKitty">
  <button @click="addKitty">
    + Add
  </button>
  <ul>
    <li v-for="cat in cats">{{ cat  }}</li>
  </ul>
  <cat-list :cats="cats" />
<div>

<script>

  Vue.component('cat-list',
    props: ['cats'],
    template:`<ul>
      <li v-for="cat in cats">{{ cat.name }}</li>
    </ul>`
  )

  new Vue({
    el:'#root',
    component: ['cat-list']
    data: {
      cats: [{name:'kitkat'},{name:'fish'},{name:'henry'}],
      newCat: ''
    },
    methods: {
      addKitty: function() {
        this.cats.push({ name:this.newCat})
        this.newCat=''
      }
    },
    computed: {
      kittifyName: function() {
        if(this.newCat.length > 1) {
          return this.newCat + 'y'
        }
      }
    }
  })
</script>
```

## Vue lifecycle

```html
<div id="root">
  <input v-model="newCat" @keyup.enter="addKitty">
  <button @click="addKitty">
    + Add
  </button>
  <ul>
    <li v-for="cat in cats">{{ cat  }}</li>
  </ul>
<div>

<script>
  new Vue({
    el:'#root',
    component: ['cat-list']
    data: {
      cats: [{name:'kitkat'},{name:'fish'},{name:'henry'}],
      newCat: ''
    },
    methods: {
      addKitty: function() {
        this.cats.push({ name:this.newCat})
        this.newCat=''
      }
    },
    created: function() {
      console.log('Created')
    },
    mounted: function() {
      console.log('Mounted')
    },
    updated: function() {
      console.log('Updated')
    },
    destroyed: function() {
      console.log('Destroyed')
    },
  })
</script>
```