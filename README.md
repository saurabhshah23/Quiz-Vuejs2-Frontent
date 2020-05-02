# vue-quiz

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

=============================================================

## Vue JS 2.0 (020520)

```
cmd:
npm install -g @vue/cli
vue --version
vue create vue-quiz
cd vue-quiz
npm run serve
npm i --save bootstrap-vue bootstrap
```

## LEARN:

```
ref: https://www.youtube.com/watch?v=4deVCNJq3qc
Vuejs2 + bootstrap-vue + API(fetch) // till time 01:50:00
Vuex + Vue-Router
```

===================================================

## ===DIRECTIVES:=====================================

```
- v-model // 2-way binding, msg is the data/state attribute
  <input v-model="msg" />

- v-if // evaluates expression in bool
  - chaining with if:
- v-else-if
- v-else

    <div v-if="count===1">Display if</div>
    <div v-else-if="count===2">Display else-if</div>
    <div v-else>Display else</div>

- v-show // same as v-if, but this is hidden and present in dom.

- : / v-bind: // binds html attributes with variable values.

  - :disabled (colon: is the shorthand for v-bind)
    <button onclick="alert('Submit clicked.')" v-bind:disabled="email.length<2" >Submit</button>
    <input v-model="email" :class="redBorderClass: email.lenght<2" />
    <input v-model="email" :class="[email.lenght<2 ? redBorderClass : GreenBorder]" /> // Another Syntax for multiple classes

- v-text // same as interpolation {{}}
    <p v-text="msg"></p>
    <p>{{msg}}</p>
- v-html // parse the text as html while rendering.
- v-once // no updates will be done to once rendered dom.

- v-for // looping an array.

- @ / v-on:event // event handling in vue

  - @click (@ is shorthand)
    <input v-on:keyup.enter="addCat" v-model="newCat" /> // adds new cat on enter.
    <button @click="addCat">Add</button> // adds new cat on button click
  - chaining can also be done.
    <button v-on:click.prevent.stop="addCat">Add</button> // chains event.preventDefault and stopPropagation by these shorthands.

- | filters // apply filter logic to the values using pipe sign |.

  - multiple filters can be chained
    <li>{{cat.name | capitalize | trimIt}}</li>

- {{}} computed // displays the computed value as per the logic
```

===================================================

## ===new Vue({})=====================================
new Vue({options object}) - to create new app.

```
el: "#app1" // root dom element
component: [] // list of all components used
data: {} // data/state to be used in app
methods:{} // functions used in app
filters: {} // filters for value display
computed:{} // dynamic computation functions

created: function(){}
mounted: function(){} // very useful for manual mounting of Vue app (vm.\$mount(el))
updated: function(){}
destroyed: function(){}
and various other lifecycle methods... (refer lifecycle diagram on vue docs)
```

---

```
OPTIONS OBJECT in new Vue(
{
el: "#app1", // el to bind app to a dom element
component: [ // component to add re-usable components in app.
'cat-list'
]
data: { // data object to bind state variables in vue app.
msg: "hello Vue!",
cats : [{name: " cat1"},{name: "cat2"}],
newCat: ''
},
methods: { // methods provide various functions to be used in app.
addCat: function(){
return this.cats.push({name:this.newCat});
}
},
filters: { // filters to apply pipe filters on values while rendering.
capitalize: function(value){
return value.toUpperCase()
},
trimIt: function(value){return value.trim()}
},
computed: { // computed functions are used for display and more useful with vuex
kittify: function(){
if(this.newCat.length>2) return this.newCat+"y";
}
}
})
```

===================================================

## ===Vue.component('c1',{})==========================

```
props: [] // props received from parent.
template: "" // html template
```

---

```
Vue.component('cat-list',{
props: [ // props are dynamic props received while invoking component
'cats'
],
template: `// template for dynamic html <ul><li>cat</li></ul>`
})
```

===================================================

## ===EXAMPLES========================================

```
1. NEW APP:
   <div id="root">
       {{msg}}
   </div>
   let vm = new Vue({
       el: "#root",
       data: {
           msg: "Hello Vue!"
       }
   })

2) COMPONENT:
   Vue.component('cat-list',{
   template: `<ul><li>cat</li></ul>`
   })
```

===================================================
