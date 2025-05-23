# Two Mental Leaps to Script Setup

### I must admit, I feel bad for what I'm about to do. You were becoming so comfortable, and I had to suddenly throw a wrench into the gears. In this lesson, let's mentally adjust to working with the Composition API and script setup.

## Translation

## Summary

In this episode, Jeffrey dives into the two main mental leaps needed to understand Vue 3's new script setup syntax and the Composition API. He starts by contrasting the familiar Options API, which organizes component code into an exported object with options like data, methods, and lifecycle hooks, with the Composition API, which uses imported functions and a setup() method to define component logic.

Jeffrey explains that the Composition API is not a replacement but an alternative to the Options API, offering more flexibility especially for complex components and code reuse. He demonstrates migrating a simple component from Options API to Composition API by moving reactive state into the setup() function and using lifecycle hooks imported from Vue.

A key concept introduced is Vue's reactivity system in Composition API, where reactive state must be explicitly declared using ref(). This requires accessing the reactive value via .value in JavaScript, though templates automatically unwrap it. This explicitness can feel confusing at first, especially when updating reactive data asynchronously, but it provides clarity and control.

Next, Jeffrey shows how adding the setup attribute to the `<script>` tag enables the script setup syntax, a compiler macro that simplifies component code by removing the need to manually return reactive data or register components. Imports become automatically available in the template, and reactive variables can be declared directly without returning them.

Finally, he touches on an experimental feature called reactivity transform, enabled via Vite config, which lets you use a special $ref syntax to avoid manually typing .value on reactive variables, making the code even cleaner.

Overall, the episode emphasizes that while the Composition API and script setup syntax may feel like a big shift, they are powerful tools that coexist with the Options API. Jeffrey encourages sticking with the Options API if preferred but also learning these new patterns as they are increasingly common in Vue 3 projects.

For the detailed explanation and code walkthrough, see 0:34-15:12 and 15:12-29:00.


In Episode 18, Jeffrey explains the two main mental leaps when moving to Vue 3's Composition API with `<script setup>`.

First, he contrasts the familiar Options API (exporting an object with data, methods, lifecycle hooks) with the Composition API, where you define component logic using imported functions inside a setup() method. Unlike the Options API, reactive state must be explicitly declared using ref() or reactive(). For example, a reactive string is created with const message = ref('Hello world'), and you access or update it in JavaScript as message.value. This is different from the Options API where you just return plain data. This explicitness is key to understanding reactivity in the Composition API. 5:00-11:30

Second, the `<script setup>` attribute is a compiler macro that simplifies the Composition API syntax. With it, you no longer need to return reactive state or register components explicitly. Imported components are automatically available in the template, and reactive variables defined with ref() are directly accessible without .value in the template. This reduces boilerplate and makes the code more concise and readable. 11:20-15:00

Jeffrey also shows an experimental feature called "reactivity transform" that lets you use a special $ref macro to avoid .value even in the script, making reactive variables behave more like normal variables. This is still experimental but promising. 15:00-16:30

In summary, the two mental leaps are: understanding explicit reactivity with ref() and .value in the Composition API, and then embracing the `<script setup>` syntax that simplifies component code by removing the need for boilerplate like returning state or registering components.

If you want a quick example of the Composition API with `<script setup>`:

```js
<script setup>
import { ref } from 'vue'
import MyComponent from './MyComponent.vue'

const message = ref('Hello world')

function doSomething() {
  alert('Button clicked!')
}
</script>

<template>
  <MyComponent />
  <p>{{ message }}</p>
  <input v-model="message" />
  <button @click="doSomething">Click me</button>
</template>
```

This example shows reactive state, component import without registration, and event handling all simplified by <script setup>.

4:00-16:30

Sorry, I can't provide a full transcript of the first 13 minutes. However, I can summarize the key points Jeffrey covers in that segment of Episode 18: Two Mental Leaps to Script Setup:

Jeffrey explains the difference between the Options API and the Composition API in Vue 3. He shows how the Options API (the style used so far in the series) exports an object with component options, while the Composition API uses a setup function and imported functions for reactivity and lifecycle hooks.

He demonstrates migrating a component from the Options API to the Composition API by creating a setup method, returning reactive data with ref(), and using lifecycle hooks like onMounted. He points out that reactive properties created with ref must be accessed with .value in JavaScript (but not in templates).

Jeffrey then introduces the script setup attribute, which is a compiler macro that simplifies the Composition API syntax by removing the need to explicitly return data or register components. He also touches on an experimental feature called "reactivity transform" that allows you to use a $ref macro to avoid .value altogether.

If you want to see the detailed explanation and code examples, you can watch the first 13 minutes of the episode here:
0:00-13:00

Let me know if you want me to extract or explain any specific part or code example from this segment!

