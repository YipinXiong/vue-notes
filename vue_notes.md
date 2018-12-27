#### `v-show`  vs `v-if`

`v-if` is “real” conditional rendering because it ensures that event listeners and child components inside the conditional block are properly destroyed and re-created during toggles.

`v-if` is also **lazy**: if the condition is false on initial render, it will not do anything - the conditional block won’t be rendered until the condition becomes true for the first time.

In comparison, `v-show` is much simpler - the element is always rendered regardless of initial condition, with CSS-based toggling.

Generally speaking, `v-if` has higher toggle costs while `v-show` has higher initial render costs. So prefer `v-show` if you need to toggle something very often, and prefer `v-if` if the condition is unlikely to change at runtime.



comfirm (yes or no, dialog in browser provided by javascript)



You can use $refs to get some DOMs; however, if you make some changes, you will only get changes once. Because `Vue` instance will hold a template that will be used whenever the `vue` instance re-renders. 



Virtual DOM:

Because of overhead to update a DOM element is quite high, thus, `vue`  provides us with a layer called `virtual Dom`. Only check the difference part then update the corresponding part in DOM.



![1545738620966](imgs/1545738620966.png)



## Vue instances' life cycle diagram:

![The Vue Instance Lifecycle](imgs/lifecycle.png)



![1545739984811](imgs/1545739984811.png)



## What is a *"development workflow"*?

![1545827714668](imgs/1545827714668.png)

This workflow provide us with a build process where ES6 code can be converted into ES5 code that can be run directly in the browser. There are various imports. Thus, you require a way to bind them together.

The key idea behind scene is that we compiled the code into executable code before sending it to the user, which tremendously decreases the size of code and improve user experience. (preprocessor)

#### 

## The function of  `webpack` in our project:

 In the `webpack`, every module will be converted by a specific *loader* before being packed into *bundle*. `Vue` provides users with vue-loader plugin to execute the transformation of `.vue` (Single File Component).  For instance, convert ES6 to ES 5 so that every browser can run our code. It will bundle tons of dependencies into a single bundle.js file. `webpack` provides various *loaders* to compile different files into primary files. 



## What are the `build` process has done?

You can compile any template, any html code to javascript in the end because there are JS object representations of your html elements. In this way, we don't have to ship the compiler when deploying our app, that reduces the file size of the `vuejs`. Second, to unlock some features which are not possible to be used in the native DOM.

We have the main.js file that will be the first file which gets executed when the bundle here gets loaded in the index.html file.



## The Virtual DOM

Vue accomplishes this by building a **virtual DOM** to keep track of the changes it needs to make to the real DOM. Taking a closer look at this line:

```
return createElement('h1', this.blogTitle)
```

What is `createElement` actually returning? It’s not *exactly* a real DOM element. 

*It could perhaps more accurately be named `createNodeDescription`, as it contains information describing to `Vue` what kind of node it should render on the page, including descriptions of any child nodes.* We call this node description a “virtual node”, usually abbreviated to **VNode**. “Virtual DOM” is what we call the entire tree  of  VNodes, built by a tree of Vue components.

 

To avoid interfering our main Vue instance, vue `components` defines its inner `data` property as a function that will return a new object:

 ```javascript
Vue.component('my-cmp', {
	data: function() {
		return {
			status: 'critical'
		}
	},
    template: '<p> Server Status: {{status }} </p>'
});
 ```



The name of the .vue file is irrelevant to the component's name; you can rename it in main.js file.

component-registration

## How does `vue` achieve the scoped style?

`vue` will give \<template> a special attribute, like `data-v-aswqgfq`. Then, after compiling process, you can see that `vue` will create a \<style> link for each `.vue` file, adding them into the header of the final html. Here is the trick: in the style, `div[data-v-aswqgfq] ` CSS selector will select the element to style it. In this way, `vue` achieves the goal (scoped styling).



## Component communication

```html
<app-user-detail prop="name"></app-user-detail>
<--! below one is dynanmic binding; the above one is assigning a static string-->
<app-user-detail :prop="name"></app-user-detail>
```



> Note that the property name in html is **insensitive!**
>
> In child component, `props` array's elements can be used as `data`

> Note 2: `props` array supports type validation:
>
> ```javascript
> props: {
>    myName: String
> }
> 
> // another advacned settings:
>  
> props: {
>     myName: {
>         type: String,
>         requiredL true,
>         default: "Yipin" 
>     }
> }
> ```



Another thing needs attention is that if you pass a object from parent component to child component, you are passing the `reference`! 



*Using customized event to pass messages to parent component*

 ```javascript
this.$emit('customizedEvent', this.myName);
 ```

 In the parent component, use `@` to listen to the event and extract the data from `$event` keyword.



![1545947554695](imgs/1545947554695.png)



###  Event Bus

It is that kind of an object serving as a place to listen to events and passing data on.

`eventBus` here is an abstract concept. Literally, `eventBus` is a new vue instance.  

```javascript
//using the hook function to achieve eventBus
import { eventBus } from '../main'
//create eventBus, new vue instance, in `main.js` and `export const eventBus`
methods: {
    //bind the eventListener to the event from eventBus on receiving component
    created(){
		eventBus.$on('customizedEvent', callback);        
    }
}

// for the sender component, you just need to refactor the code from 
 this.$emit('customizedEvent', callback/augments);

// ↓↓↓↓↓↓↓↓↓↓↓
import { eventBus } from '../main'
eventBus.$emit('customizedEvent', callback/augments);

```

With the application becomes more and more complicated, we require a external tool, `vuex`.

> Here we introduced a very significant concept in programming
>
> You can always create a new instance independent from all components and store some states or data in this specific instance as data center. Thus, your data can be shared across the component and you can easily manage the data. 

Let's refactor the code above:

```javascript
//in main.js
export const eventBus = new Vue({
    methods: {
        eventHandler(data) {
            this.$event('customizedEvent', data);
        }
    } 
});

//--------------------- in this way, refactor sender-----------------
eventBus.eventHandler(data);
// Generally speaking, the concept is very similar to Angular that owns
//dependencies injection.
```

![State Management](imgs/state.png)

