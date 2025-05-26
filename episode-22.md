# Dependency Injection With Provide and Inject

###

Here is the full transcript for Episode 22, "Dependency Injection With Provide and Inject," from the "Learn Vue 3: Step by Step" series on Laracasts:

Alright, next up, let's move on to dependency injection, and figure out what that looks like within the context of a Vue application. Let's get going. Okay, so have a look at this example I've set up. Here's my home view, and you can see I'm importing this quiz component. Now, it would take way too long to fully implement this for a little example, but I've at least created the basic scaffolding. You can see we're passing a quiz object to our component, and of course, it's dummy data here, but in real life, you would be fetching this from your server. Okay, and if we click through to that, yeah, again, this is the basic scaffolding.

A quiz might have a header, a section for the question, and you might be doing a v-for to generate those, and then we have a footer. Now, if I switch over to the browser, again, I've set up the general scaffolding, where you might show the header, you would iterate for all of the questions, and then you might have some links at the bottom. Okay, so here's what I want to show you. So sometimes you'll run into awkward situations where you have to pass a prop down many levels deep.

We refer to this as prop drilling. So for example, if I go into the quiz footer, we then have another nested component for the footer links, and then right here, you can see we are echoing out the name of the quiz. Okay, so that means this many levels deep, we need access to that quiz object. Now maybe we could pass through the name, but at least in this example, we're expecting the full quiz object. All right, so think about that.

We have our top-level quiz. We then need to pass the quiz object to the footer, and that then needs to pass the quiz object to the footer links, and this is just a tiny example. In real life, you may find yourself drilling down four or five levels deep, and often this can just be, if nothing else, a little annoying, where certain components are accepting a prop for the sole purpose of passing it on to a nested prop. So luckily, we do have some options to skirt around this. So in this episode, we'll talk about provide and inject.

So it sounds like this quiz prop is pretty important, and we'll need to access it any number of levels deep, and by level, again, I'm talking about a nested component. Okay, so let's do this. I'm going to import provide from Vue, and then we're going to provide a key and a value. All right, so now the cool thing is when a component provides a piece of data like we've done here, any of its children, or really any of its grandchildren, can access that data without requiring that we do that prop drilling thing that we're trying to get around in the first place.

Okay, so let's see it in action. I'm now going to go into the footer, and then another level deep, and let's see if we can grab that value. We can do it by importing inject, so provide and inject, and then I can say let, what did we call it, key equals inject key. All right, so notice way up here, we are providing a key of key, and then any of its children can then inject key, and that's exactly what we're doing here. Okay, so now just as an example, let's echo out the value and view it in the browser.

So we switch back, and sure enough, there it is. We have our value. And just to prove it to you, if we change it to hello there, if we come back, there we go. All right, so granted, this is kind of a silly example, but it's still incredibly cool when you think about it. If we take a look at our component structure, yeah, Quiz is now providing this piece of data to any of its children, and the children is the key thing here. It's not like it's available globally. Its sibling components can't access it, but any children of Quiz can. So that means if I want to access that key, I don't have to prop drill. I can simply inject it for only the components that require it.

Okay, so what else? A couple other things. What about reactive data? So for example, what if I had, let's think of like a name, ref John Doe. Okay, and I'm going to pass name like so. Okay, so now name is not just a string John Doe, it is a reactive object. So now if we go all the way down to a nested child, let's inject name using the exact same system. So set name equals inject name, and then way up here, we'll spit out that value. Okay, so if we take a look, oh, what do we have here? Ref is not defined. I'm sorry, I thought my editor imported it.

There we go. So now, sure enough, we passed John Doe. But what about if we need to change that data? All right, let's talk about some options that are available to you. Just real quick at the very top, just so we can see that the data remains in sync, I will also show the name up here. Okay, so now I see John Doe at the top, and then John Doe right down here. Okay, well, because name is reactive, if we were to change it, and once again, we'll do a simple setTimeout. So I could say, again, after two seconds, let's change the name to a new name, whatever that might be. And if I switch back and give it a refresh, we count one, two, and sure enough, we changed the name within QuizFooterLinks. And because it's reactive data, of course, that will also be reflected way up here in the parent.

Okay, so this is an option. And honestly, I think for a certain size of project, it's totally fine. You might find at a certain scale, it is frowned upon. And this is because, again, if you imagine a project that's quite large, you can sometimes run into situations where reactive data is being changed, and you don't know where. And it can be difficult to figure out, okay, well, at some point, this is changing, but I don't know where that's taking place. So this isn't a requirement, you can keep it like this. But if that is a concern for you, what you could do is create a rule that the only place you can change the name is in the parent where it's being provided. So if you took that approach, you might provide an object here, where you send through the name, or because the key and the value are the same, I can just only provide that. And then maybe we could provide the equivalent of a mutator. And this would be a function that would be responsible for changing the name. So maybe if we call, you know, change name, whatever this might be, and I could then say name.value equals changed, just as a little example. So notice the logic for updating name now exists within the parent.

And if we want to trigger that change, we simply pass a reference to this function to the child. All right, let's give it a shot. I now go back to QuizFooterLinks. And we'll say, how about this, make it a button. And we'll say, when you click on me, yeah, I want to call this function here. So if I want to do that, we need to accept it, name and change name. And then we'll say call change name.

So yeah, again, this is kind of a cool approach. Change name is now a function that's being declared all the way within the parent. So the child is just calling that function. All right, let's see if it works. Come back, notice we have John Doe and John Doe down here. If I click on it, sure enough, we update the button. And also that's reflected in the parent. So you might find that that's a cleaner, more structured way to go about it, especially as you start creeping into larger projects. All right, something to think about at the very least.

So finally, to finish this up, we decided that a quiz needs to be available all the way down in this nested child. So let's bring that back. We want the name of the quiz. And I'm just going to say right here, let quiz equals inject quiz. So I want to inject quiz from the parent. That means in the parent, I need to provide quiz. So we'll do this reformat. And then I will say provide quiz, like so actually, I'm sorry, let's say props and then do props.quiz. And that should do it. All right, so let's clear this out and view it in the browser. And there we go. All the way down here, it's difficult to see if I bring it up, we can drill down.

So we have our top level, excuse me, we have our top level quiz component. Within it, we have our header and then our question and then our footer at the bottom. And then if we drill down into the footer, there's that final nested component where we have provided information about the quiz. And yeah, I hope we can agree that is a much cleaner approach versus one after the other drilling down and passing quiz to this component and then to that child and then to that child and to that child until we get to the very bottom or nested component that requires it.

You can also watch the episode here: 0:00-9:29

Let me know if you want me to extract any specific code examples or explanations from this episode!

## Translation

Aqui está a tradução completa do texto do episódio 22, "Injeção de Dependência com Provide e Inject", da série "Learn Vue 3: Step by Step" do Laracasts:

Tudo bem, vamos em frente agora com injeção de dependência e entender como isso funciona no contexto de uma aplicação Vue. Vamos começar.

Veja esse exemplo que preparei. Aqui está minha home view, e você pode ver que estou importando um componente chamado Quiz. Levaria muito tempo para implementar isso completamente só para um exemplo simples, mas pelo menos criei a estrutura básica. Dá para ver que estamos passando um objeto quiz para nosso componente e, claro, é apenas um dado fictício aqui, mas na vida real você buscaria isso do servidor.

Se clicarmos nesse componente, novamente, veremos apenas a estrutura básica.

Um quiz pode ter um cabeçalho, uma seção para a pergunta (e você provavelmente usaria um v-for para gerar essas perguntas), e depois um rodapé.

Se eu mudar para o navegador, você verá a estrutura geral onde mostramos o cabeçalho, iteramos por todas as perguntas e temos alguns links no final.

Agora, veja o que quero te mostrar:
Às vezes você se depara com situações chatas em que precisa passar uma prop por muitos níveis de componentes. Isso é conhecido como prop drilling.

Por exemplo, se eu for até o rodapé do Quiz, temos outro componente aninhado para os links do rodapé. E veja aqui, estamos exibindo o nome do quiz.

Ou seja, mesmo estando vários níveis abaixo, precisamos acessar aquele objeto quiz.

Claro, poderíamos passar apenas o nome, mas neste exemplo, esperamos o objeto quiz completo.

Então pense nisso:
Temos nosso Quiz no nível mais alto. Precisamos passar o objeto quiz para o rodapé, que então precisa passá-lo para o componente de links. E esse é só um exemplo pequeno — na vida real, você pode acabar com 4 ou 5 níveis de profundidade. E isso acaba sendo irritante, onde certos componentes só existem para receber uma prop e repassá-la adiante.

Felizmente, temos uma alternativa para isso. Neste episódio, vamos falar sobre provide e inject.

Parece que essa prop quiz é bem importante e precisamos acessá-la em qualquer nível de profundidade (ou seja, componentes aninhados).

Vamos lá.
Vou importar provide do Vue e fornecer uma key com um valor. A parte legal disso é: quando um componente fornece um dado como fizemos aqui, qualquer filho — ou até mesmo neto — pode acessar esse dado sem precisar fazer o "prop drilling".

Vamos ver isso em ação.
Agora, vou para o rodapé e depois mais um nível abaixo. Vamos tentar capturar esse valor. Fazemos isso importando inject. Então posso escrever algo como let key = inject('key').

Perceba que lá em cima fornecemos a chave "key", e qualquer filho pode injetar "key", que é exatamente o que estamos fazendo aqui.

Agora, só como exemplo, vamos exibir o valor no navegador.
Voltamos ao navegador e, sim, lá está ele. Temos o valor.

Só para provar, se mudarmos para "olá mundo", ao atualizar a página... pronto, mudou!

Sim, esse exemplo é meio bobo, mas ainda assim é muito útil.
Se olharmos para a estrutura de componentes, o Quiz agora está fornecendo esse dado para qualquer filho — e esse é o ponto-chave: não está disponível globalmente, componentes irmãos não têm acesso. Mas qualquer componente filho tem.

Ou seja, se eu quiser acessar essa chave, não preciso fazer prop drilling. Posso simplesmente injetar, mas somente nos componentes que precisam dela.

Agora, outra coisa:
E se os dados forem reativos?
Por exemplo, digamos que temos const name = ref('John Doe'), e passamos isso como valor.

Então agora name não é só uma string, é um objeto reativo.

Se formos até um filho aninhado e usarmos inject('name'), depois exibirmos esse valor, veremos que ele aparece corretamente.

Mas e se quisermos modificar esse valor?

Vamos testar.
Só para ver que os dados estão sincronizados, vamos também exibir name no topo.

Agora vemos John Doe tanto no topo quanto abaixo.
Como name é reativo, podemos mudar seu valor com setTimeout, por exemplo, após dois segundos:

js
Copy
Edit
setTimeout(() => {
  name.value = 'Novo Nome'
}, 2000)
Recarregamos a página, esperamos 2 segundos, e pronto! O nome mudou lá embaixo, e também lá em cima no componente pai.

Essa é uma opção válida.
E honestamente, para projetos de pequeno ou médio porte, está tudo bem.

Mas em projetos maiores, pode ser malvisto, porque você pode acabar em situações onde os dados estão sendo modificados e você não sabe onde isso está acontecendo.

Então o que fazer?
Você pode criar uma regra de que a única parte do app que pode mudar o valor é o componente pai que forneceu o dado.

Para isso, em vez de fornecer apenas name, você fornece um objeto com name e uma função de mutação, tipo changeName.

js
Copy
Edit
provide('name', name)
provide('changeName', () => {
  name.value = 'Alterado'
})
No componente filho, você injeta ambos (name e changeName), e chama a função changeName quando quiser mudar o valor, como em um botão:

vue
Copy
Edit
<button @click="changeName">Clique aqui</button>
Essa é uma abordagem mais limpa e estruturada, especialmente em projetos maiores.

Para encerrar:
Decidimos que quiz precisa estar acessível até o componente mais aninhado.

Então, no componente pai, fazemos:

js
Copy
Edit
provide('quiz', props.quiz)
E no componente aninhado:

js
Copy
Edit
const quiz = inject('quiz')
Agora, se olharmos no navegador, veremos que mesmo no componente mais aninhado conseguimos acessar quiz.

Isso é uma abordagem muito mais limpa, comparado a ter que passar quiz de componente em componente, até o mais profundo deles.

## Summary

In this episode, Jeffrey explains how to use Vue's dependency injection system with provide and inject to avoid prop drilling — the tedious process of passing props through many nested components just to reach a deeply nested child.

He starts with a quiz example where a quiz object needs to be accessed several levels deep, such as in footer links. Instead of passing the quiz prop down through every intermediate component, the parent component uses provide to make the quiz object available to all its descendants. Then, any nested child component can use inject to access that data directly, skipping the intermediate layers.

Jeffrey also covers how reactive data works with this pattern. By providing a reactive reference (e.g., a ref), changes made in any child component are reflected throughout the component tree. However, he cautions that for larger projects, directly mutating reactive injected data can make it hard to track changes. A cleaner approach is to provide mutation functions from the parent and call those from children, keeping state changes centralized.

Finally, he demonstrates the full flow of providing the quiz object at the top level and injecting it in deeply nested components, showing how this leads to cleaner, more maintainable code compared to prop drilling.

This episode highlights how provide and inject help manage shared state across nested components without cluttering intermediate components with unnecessary props, while also discussing best practices for reactive state mutation.