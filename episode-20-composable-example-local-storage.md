# Composable Example: Local Storage

Here's the full transcript for Episode 20, "Composable Example: Local Storage," from the "Learn Vue 3: Step by Step" series on Laracasts:

All right, next up, why don't we keep working with composables? In this video, I will show you a new example that makes use of, of course, the Composition API, as well as Reactivity. All right, so here's what I'm thinking. I'll set up a basic example here. What is your favorite food? And then we'll have a simple input. Now, of course, I want to track the user's answer, so I will add vModel, and we'll call it food, and then I'll set that up as a reactive property. So I can say let food equals a ref, and that will default to an empty string.

it food, and then I'll set that up as a reactive property. So I can say let food equals a ref, and that will default to an empty string. Okay, well, of course, if we switch to the browser, I will open up Vue DevTools, here's our component, and yeah, notice as I type into it, we keep track of it. Okay, but maybe we also want to take this a step further and save the user's input to local storage. That way, if they leave and come back or accidentally refresh the page, they don't lose everything they've written. And this is actually very common for things like forums, where you might potentially write a long reply, and if something happens, if your internet goes out, you lose all of your

And this is actually very common for things like forums, where you might potentially write a long reply, and if something happens, if your internet goes out, you lose all of your input. Let's see if we can prevent that. And as always, I will show you this in two steps. First, we will do it inline, and then second, we will extract it to a composable. Now your first thought might be, well, let's listen for when the user types into this input and when they do write to local storage. So there is an input event we could use. I could say when the user types into it, let's call a function write.

So there is an input event we could use. I could say when the user types into it, let's call a function write. All right, so we could define that here, write. Now if you're familiar with the local storage API, I could say a set item, we'll call it food, and I'll make it equal to the value for this ref. So food.value. And yeah, that should work. Just keep in mind, in real life, we should throttle this. At the moment, we are calling this write function for every keystroke, but it's probably not necessary.

At the moment, we are calling this write function for every keystroke, but it's probably not necessary. Maybe you call it once every few seconds or something like that. Okay, but anyways, just an example. If I bring up the application tab, I will click on storage, and then down to our current site. Okay, and of course, we don't have anything in local storage. Let's see if we can fix that. Pizza, and there we go. So now, even if I refresh the page, of course the input is cleared, but we do remember that

Pizza, and there we go. So now, even if I refresh the page, of course the input is cleared, but we do remember that the user typed pizza into that input. So now, how can we remember it on page load? We basically want to say, okay, when the page loads, check into local storage, and if you have something for this input, then set it as the default value. Okay, well maybe we could do something like local storage.getitem for food. And let's see if that works. Come back, have a look, and there we go. It works.

Come back, have a look, and there we go. It works. But if we go to application, I can right click here and delete it. What happens if we refresh and there is nothing in local storage? Then it's blank, we type into it, everything seems to be working. Refresh and we've remembered. But now, let's say I want to do this for multiple inputs. So I could say, I don't know, how old are you? And this will be vmodel for age. All right, let's set that up, see how it might work.

And this will be vmodel for age. All right, let's set that up, see how it might work. We now have one for age, where we get a key called age from local storage. Next, the write function can't be so generic. We're going to need a key as well as a value to write to. That way I can substitute these. Okay, so now when we type into this input, we could write to food the value of food. All right, and then the same thing here for age. All right, let's give that one a shot. So we'll say here, pizza, maybe you're 12 years old.

All right, let's give that one a shot. So we'll say here, pizza, maybe you're 12 years old. We give it a refresh, and that has been saved. And once again, if we go into local storage, sure enough, we are tracking that. Let's do my age, 37, tacos, you get the idea. Everything is working here. Okay, but it is a little bit messy. But then there's so much more we need to deal with, things like serialization. What if you were writing an object or an array to local storage? We should also set up maybe a watcher.

What if you were writing an object or an array to local storage? We should also set up maybe a watcher. So what if the value of food changes outside of this input? Well, do we also write it to local storage? Let's give it a shot. Let's say setTimeout, and we'll say after two seconds, I'm going to set the food value equal to changed. Okay, well, when we do that, it would be nice if we also update local storage in the process. But right now, if I give it a refresh, one, two, we check local storage, and

it would be nice if we also update local storage in the process. But right now, if I give it a refresh, one, two, we check local storage, and of course, that's not changing anything here. Okay, well, one way we can solve this is instead of listening for an input event, let's just watch for when the value of food changes. So if we take that approach, I get rid of all of this, and same thing down here. And now, to set up a watcher, we're going to import watch from view. Or if you're using the options API, you can just add a watch object directly to that object. So I'm going to watch food, and when it changes, I'll have the value here,

you can just add a watch object directly to that object. So I'm going to watch food, and when it changes, I'll have the value here, the new value, why don't we then write to local storage? So write to food, the given value. All right, let's see if that works. So we come back, I will change food to once again pizza, and now that's working as well. But also notice, we have this timeout here where we change it to changed. So give it a refresh, and let's see if that works. One, two, and everything's working now.

So give it a refresh, and let's see if that works. One, two, and everything's working now. All right, and that's a better approach in my mind. But yeah, once again, we'd have to set up a watcher for everything. So watch age, and then write to local storage. So you can see, something as simple as remembering basic input data, yeah, it gets kind of annoying to write. So instead, I think this is a perfect use case for extracting a reusable composable. Okay, so open up the sidebar, I will add a new composable.

extracting a reusable composable. Okay, so open up the sidebar, I will add a new composable. I'm going to call it useStorage. And as we've learned, I'll hide the sidebar. We should export a function with that same name. That will return an object that we can receive from our component. All right, so let's switch back to home view. We now know that we're going to import useStorage from our composable. And then ideally, if I get rid of all of this, yeah, I want to say something like, all right, I want to useStorage for food.

And then ideally, if I get rid of all of this, yeah, I want to say something like, all right, I want to useStorage for food. And then I will catch that into this variable. Yeah, ideally, that's all I need to do here. And as you can imagine, this will look into local storage. It will try to find something for the key food. If it does, it returns it, and maybe it should also return it as a ref. That way, we can instantly use it within our input. Okay, so let's keep it very simple for now, get rid of all of that. And if we try it, of course, nothing is going to happen because useStorage is blank.

Okay, so let's keep it very simple for now, get rid of all of that. And if we try it, of course, nothing is going to happen because useStorage is blank. So let's write a little code before trying this out. We're going to accept a key, and we've learned that we can run localStorage.getItem for key. Now, if there is anything in localStorage for that key, it of course returns the value, otherwise it returns null. So why don't we save this to a variable like storedValue, whatever is in localStorage. But then ultimately, I want to return a ref to the user.

whatever is in localStorage. But then ultimately, I want to return a ref to the user. So I could say let value equal ref, import that, storedValue, and then ultimately return this value to the user. All right, so if we switch back, we now know that this food variable is at the very least reactive, which means if we add vModel to it, we can keep track of what the user types in. So open up viewDevTools, here's our home view. Right now, food is null. We type into it, and yeah, we are tracking that, which is great.

Right now, food is null. We type into it, and yeah, we are tracking that, which is great. Okay, the next step is to take what the user types and also write it to localStorage. So let's switch back, and we learned that we could add a watcher. So I will import watch from view. Remember, this is how the composition API works. We import the APIs that we require. So let's watch that value, and when it changes, I want to write to localStorage.

So let's watch that value, and when it changes, I want to write to localStorage. Okay, let's switch back and find our write function that we wrote earlier. I'll cut that out and bring it, how about, right down here. But this time, write doesn't need the key and value. We already have it, so let's get rid of that. The key was passed in when we called the function, and the value is our ref here. So just keep in mind, when you have a ref, you always got to tack on .value, which makes this property name a little weird, val.value.

So just keep in mind, when you have a ref, you always got to tack on .value, which makes this property name a little weird, val.value. Maybe we can think of a better name later, but nonetheless, I think this should work. All right, so think about it. Let's go through this. At the very top, I say, all right, I want to use storage for food. So immediately, it looks in localStorage to see if we have anything for it. And if we do, we wrap it in a ref. And in fact, if we don't, we also wrap it in a ref, but it's just set to null.

And if we do, we wrap it in a ref. And in fact, if we don't, we also wrap it in a ref, but it's just set to null. Then we keep an eye on that model. And if it changes, we instantly call this write function that writes the value back to localStorage. All right, so let's give this a shot now. I'll go into application, it looks like my localStorage is clear. I will type pizza into it, and now we're up and running. So have a look. We are keeping food in sync, which means if I were to change it here to tacos,

So have a look. We are keeping food in sync, which means if I were to change it here to tacos, well, that change should also trigger a write to localStorage. So back to application, and now notice that's been updated. All right, pretty cool. But now a few edge cases, like what if we empty this out? Well, now we have food equal to nothing. So what we could do is say, look for the value. If it's an empty string, then in that case, maybe you want to call localStorage.removeItem key.

If it's an empty string, then in that case, maybe you want to call localStorage.removeItem key. Otherwise, we can set it, or we can check for null, whatever you want. All right, so now if we once again give it a shot, pizza, there it is. But if we empty it out, then we clear it entirely. And maybe that's what you want, maybe it's not. What else? What about setting default values? So for example, maybe I want to say the default value for this, if it's not in localStorage, will be salad.

So for example, maybe I want to say the default value for this, if it's not in localStorage, will be salad. All right, let's see if we can get that to work. So now, our signature now accepts a default value, and it looks like we'll have to tweak this a little bit. So let's say, all right, well, if there's a stored value already, then maybe that's the one we want to return. So I could bring this up and say, okay, well, if that's the case, then overwrite value equal to a ref for the stored value. Otherwise, we'll set value equal to a ref for the default value.

then overwrite value equal to a ref for the stored value. Otherwise, we'll set value equal to a ref for the default value. And then, well, we would also need to write to localStorage, because it doesn't yet exist there. So we create our ref, and then instantly save it to storage. So I could call write. All right, let's see if that works. And it looks like it did, just so we can see it live though. Let's delete it, and then manually refresh the page. And there we go, the default value is salad, so we saved it, and

Let's delete it, and then manually refresh the page. And there we go, the default value is salad, so we saved it, and we also wrote to localStorage. But if we change it to pizza, well, now we already have something in storage. So when we refresh the page, we should ignore that default value. Or this is a great example of something where maybe we should make it configurable. When you provide this default, should that override whatever's in localStorage, or should it not? And that's the sort of thing that could maybe be part of

should that override whatever's in localStorage, or should it not? And that's the sort of thing that could maybe be part of a configuration object that you provide. But we're not going to worry about that. All right, so like I said, there's other serialization things we might want to consider. What if you're writing an array to storage or an object? In that case, you'd want to use things like json.stringify or json.parse. But for basic examples like this, we were able to take all of that code and reduce it to a simple composable.

But for basic examples like this, we were able to take all of that code and reduce it to a simple composable. So now if we bring back that age example, how old are you, age? Well, now if we want to track this, all I have to do is say let age equals useStorage, and our key is age, and we'll have no default values in this case. All right, come back, and there they are. Ooh, age is being set to undefined. Yes, because value by default should be null. You don't have to give it to us. Okay, so let's empty those out, give it one more shot.

You don't have to give it to us. Okay, so let's empty those out, give it one more shot. And ooh, another mistake. What have I done wrong here? Value is null, so that's null. So we run this, we write value equals null, or we might need to check both, because I don't want to make this a Boolean. So something like that, I don't know, we might want to come back to that. But nonetheless, I think that would fix it. So we're just handling the use cases where we should clear it from storage.

But nonetheless, I think that would fix it. So we're just handling the use cases where we should clear it from storage. Give it a refresh, and there we go. We don't have any default values, so we don't see anything here. But as we type into it, we track it, there we go. Give it a refresh, and we've remembered it. Clear them out, switch back, and this time, let's provide defaults. Tacos, 10 years old. Now, this refreshes instantly because of feet. But yeah, when the page loads, we immediately store those in local storage.

Now, this refreshes instantly because of feet. But yeah, when the page loads, we immediately store those in local storage. And then they're rendered on the screen. And yet again, we can always track it and update it on the fly. Okay, so that's enough for this tiny example. Just keep in mind, if you implement this on your own, you should take this a little further. You need to handle serialization and a few edge cases. Now, a quick little bit of cleanup. We could just say write like this.

Now, a quick little bit of cleanup. We could just say write like this. And then what else can we do to clean this up? We have a function write. Let's also set up one to read, and that will simply wrap this call here. Okay, so I can say stored value equals read from storage. If we have anything there, then let's create a ref, watch it for changes, and when it does

## Summary of Key Concepts from Episode 20: Composable Example: Local Storage

In this episode, Jeffrey demonstrates how to create a reusable Vue 3 composable that syncs reactive state with the browser's localStorage. The example starts with a simple input bound to a reactive ref using v-model. The goal is to persist user input so it is not lost on page refresh or navigation.

Initially, he shows how to write to localStorage on every input event, but then improves the approach by using Vue's watch API to reactively update localStorage whenever the reactive value changes. This ensures changes from anywhere in the app are persisted.

To avoid repeating code for multiple inputs, Jeffrey extracts the logic into a composable called useStorage. This composable accepts a key and an optional default value, reads from localStorage, returns a reactive ref, and watches for changes to update localStorage accordingly. It also handles clearing localStorage when the value is empty.

He discusses edge cases like serialization for objects/arrays (using JSON.stringify and JSON.parse) and deep watching for nested objects to detect changes in properties. Finally, he notes that this pattern is useful for browser apps but would need adjustments for server-side rendering (SSR) where localStorage is not available.

This episode highlights how composables can encapsulate common reactive logic and side effects, making Vue 3 apps cleaner and more maintainable.

0:28-17:00
17:00-30:00

Episode Summary
The summary below is AI-generated, based upon this video's transcript. It may occasionally contain mistakes.

Let's continue working with composables by creating a simple example that tracks a user's favorite food input and persists it to local storage. This way, if the user refreshes or leaves the page, their input won't be lost.

Basic Setup
We start with a reactive property using Vue's ref:

import { ref } from 'vue';

let food = ref('');
Bind this to an input using v-model:

<input v-model="food" placeholder="What is your favorite food?" />
As you type, Vue DevTools will show the reactive state updating.

Saving to Local Storage Inline
You might think to listen for the input event and write to local storage on every keystroke:

function write() {
  localStorage.setItem('food', food.value);
}
Bind this to the input event:

<input v-model="food" @input="write" />
This works, but calling write on every keystroke is inefficient. You might want to throttle or debounce it in a real app.

Loading from Local Storage on Page Load
To restore the input value on page load, check local storage and set the reactive property accordingly:

food.value = localStorage.getItem('food') || '';
Now, when the page loads, the input will be pre-filled if there is stored data.

Handling Multiple Inputs
If you want to track multiple inputs, like age, you need to generalize the write function to accept a key and value:

function write(key, val) {
  localStorage.setItem(key, val);
}
Then call it with the appropriate key and value for each input.

Using Watchers Instead of Input Events
A better approach is to watch the reactive property and write to local storage whenever it changes:

import { watch } from 'vue';

watch(food, (newValue) => {
  localStorage.setItem('food', newValue);
});
This ensures local storage stays in sync even if the value changes programmatically.

Extracting to a Reusable Composable
To avoid repeating this logic, create a composable useStorage:

import { ref, watch } from 'vue';

export function useStorage(key, defaultValue = null) {
  const storedValue = localStorage.getItem(key);
  const value = ref(storedValue !== null ? storedValue : defaultValue);

  watch(value, (val) => {
    if (val === '' || val === null) {
      localStorage.removeItem(key);
    } else {
      localStorage.setItem(key, val);
    }
  });

  return value;
}
Now in your component:

import { useStorage } from './composables/useStorage';

const food = useStorage('food', 'salad');
const age = useStorage('age');
Bind these to inputs with v-model as usual.

Handling Serialization and Deep Watching
For objects or arrays, use JSON.stringify when saving and JSON.parse when loading.
To watch nested properties in objects, use Vue's deep watcher:
watch(value, (val) => {
  // write to localStorage
}, { deep: true });
Be aware that deep watching can have a performance cost with large objects.

Edge Cases
Clear local storage when the value is empty or null.
Consider whether default values should override existing stored values.
For server-side rendering (SSR), local storage is unavailable, so additional handling is needed.
Summary
Use Vue's ref and watch to sync reactive data with local storage.
Extract this logic into a reusable composable for cleaner code.
Handle serialization for complex data types.
Use deep watchers for nested objects.
Be mindful of SSR limitations.
This composable pattern makes it easy to persist user input and state across page reloads in a clean, maintainable way.

## Tradução para Português

Neste episódio, Jeffrey mostra como criar um composable reutilizável no Vue 3 que sincroniza um estado reativo com o localStorage do navegador. O exemplo começa com um input simples ligado a um ref reativo usando v-model. O objetivo é persistir o que o usuário digita para que não se perca ao atualizar a página ou navegar.

Inicialmente, ele mostra como gravar no localStorage a cada evento de input, mas depois melhora a abordagem usando o watch do Vue para atualizar o localStorage sempre que o valor reativo mudar. Isso garante que mudanças feitas em qualquer lugar do app sejam salvas.

Para evitar repetir código para vários inputs, Jeffrey extrai a lógica para um composable chamado useStorage. Esse composable recebe uma chave e um valor padrão opcional, lê do localStorage, retorna um ref reativo e observa mudanças para atualizar o localStorage automaticamente. Ele também trata casos onde o valor fica vazio, removendo a chave do localStorage.

Ele discute casos especiais como serialização para objetos/arrays (usando JSON.stringify e JSON.parse) e o uso de watch profundo para detectar mudanças em propriedades de objetos aninhados. Por fim, ele comenta que essa técnica é útil para apps no navegador, mas precisaria de ajustes para SSR, onde localStorage não existe.

O episódio destaca como composables podem encapsular lógica reativa comum e efeitos colaterais, deixando apps Vue 3 mais limpos e fáceis de manter.