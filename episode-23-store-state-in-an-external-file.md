# Store State in an External File

###

Here's the full transcript for Episode 23, "Store State in an External File," from the "Learn Vue 3: Step by Step" series:

Okay, at this point, we've reviewed, what is it, two different ways that we can share state across a wide range of components. So effectively, what we're talking about here is basically global state. We need some state that can be accessed by any component that requires it. So we started by reviewing what's commonly known as prop trailing. And that's where you have a piece of data, and you pass it to a component, and that component passes it to another component, and then to the child, and then to that child, and then to that child. And very, very quickly, it gets very, very annoying. So then after that, in the last episode, we reviewed provide and inject.

And very, very quickly, it gets very, very annoying. So then after that, in the last episode, we reviewed provide and inject. And yeah, that works, and that's better. But we're not done yet. So in this episode, maybe in the next two episodes, I want to show you a couple more options that you might consider. So let's get going. Now I'm still using that dummy quiz example from the last episode. If I visit my home view, you'll remember that we hard-coded the initial state for a quiz. So if you think about it, we could always extract this, and I could call it state.

If I visit my home view, you'll remember that we hard-coded the initial state for a quiz. So if you think about it, we could always extract this, and I could call it state. And let's select all of it, and assign it within script setup. Okay, so now if I did something like this, we will get the exact same output. No change here. But now, think about this. Is there anything keeping you from storing this state, or this data? That's what it is. Is there anything keeping you from storing this within its own file? Hmm.

Is there anything keeping you from storing this within its own file? Hmm. Let's play around with that idea. Why don't we create in my source directory a new folder, and we'll call it stores. And within here, we'll have a file. There are conventions around this, but for now, let's keep it super simple, and we'll call it quiz store. All right, this is interesting. So now I will grab all of this, and I will store it within this new file, and then I want this to be accessible to the outside world.

So now I will grab all of this, and I will store it within this new file, and then I want this to be accessible to the outside world. So we're going to export it like so. All right, we still have a little bit to do here, but yeah, we're playing around with this idea. What if we could place state within its own file, and then any component that needs to work with that state can simply import it? All right, let's give it a shot. So we go back to home view, and now we will import it. Imports and what did we call it?

So we go back to home view, and now we will import it. Imports and what did we call it? We called it state. All right, import state from our quiz store. Okay, well, let's see if it works. I switch back to Chrome, give it a refresh, and yeah, everything seems to be up and running. But just to be entirely sure, let's change the name to my second quiz. Switch back, and it looks like down here is the only place we use it, but sure enough, it is working. Okay, cool.

it is working. Okay, cool. Very interesting. So now let's think about it. So now if I go into quiz, let's get rid of provide and inject. And by the way, that's still very much a valid option. I'm just showing you different approaches here. So we'll get rid of that entirely. And with this approach, we're not going to accept any prop. We will instead import our quiz state.

And with this approach, we're not going to accept any prop. We will instead import our quiz state. All right, so now I can get rid of this. Go into quiz footer, clean this up a little bit. Same thing here. So yeah, notice how we're removing the need to prop drill. Okay, finally, way down here in quiz footer links, I can get rid of inject entirely. And once again, import our state. All right, and then I can update this, rename it, whatever you want. All right, so now if I switch back, yeah,

All right, and then I can update this, rename it, whatever you want. All right, so now if I switch back, yeah, everything's working exactly the way it did before. But now we're playing around with this alternative way of managing our state, and particularly a state that needs to be accessible globally, or at least across a wide range of components. And yeah, keep in mind that you're not limited to a single store. You can create as many files as you want. So maybe you could have one that works with the current user. Maybe you have another that works with a shopping cart.

So maybe you could have one that works with the current user. Maybe you have another that works with a shopping cart. That's a really good example, because when you have a shopping cart, you need to access its state across the entire page, and therefore across a wide range of components. Maybe up in the nav bar, you have a label that shows how many items are in your cart. Maybe elsewhere down here in a floating panel, it'll show what your current shopping cart total is. You get the basic idea. These are situations where you need to access information

You get the basic idea. These are situations where you need to access information across a wide range of components. And a store can offer that for you. Okay, but right now, of course, what we have is incredibly simple and is not altogether flexible. Here's what I mean. Let's add a quick button here, and we'll say Change Quiz Name. And when you click on it, what if we said state.name equals a new quiz name? Okay, let's see if that works.

And when you click on it, what if we said state.name equals a new quiz name? Okay, let's see if that works. Switch back, and we have our little button here. I give it a run, and no, it doesn't update. All right, let's have a look here. We'll open up View DevTools, and we'll come down all the way to our footer links. And sure enough, we did update the name property here, but it's not being reflected. And that's because we just updated a string.

but it's not being reflected. And that's because we just updated a string. At no point did we specify that it should be reactive. Okay, so we could switch back here into our store, and we could say, all right, it sounds like this state also needs to be reactive. You learned about ref. We can also use reactive, and this is especially useful for objects. Now I can say all of these items should be reactive.

and this is especially useful for objects. Now I can say all of these items should be reactive. All right, so let's give this another try. Here's our title. I click on it, and sure enough, we updated our store or our state, and that's then reflected anywhere else we reach for it. Just to be crystal clear, why don't we go into quiz header, and I need to switch to script setup.

why don't we go into quiz header, and I need to switch to script setup. We will import our state, and then right here, we'll update this to the name of the quiz. Okay, so now, yeah, we give it a refresh. I change it. We update that global state, and it's then reflected anywhere else that we import the file,

and it's then reflected anywhere else that we import the file, and yeah, it's such a laughably simple approach, but you know what? This is gonna get the job done more often than not. In so many cases, this is really all you need. It's not until you start building significantly more complex applications that you might run into some roadblocks, and those roadblocks are usually things like,

that you might run into some roadblocks, and those roadblocks are usually things like, this state is changing, and I don't know why, and I don't know what triggered that change, or I need to hook into when this state changes and do some kind of operation, maybe update local storage, maybe make an AJAX query, so it's those situations when you might need to reach for something a bit more flexible,

so it's those situations when you might need to reach for something a bit more flexible, and in the next episode, I'll show you what that is.

You can also watch the episode directly here: 0:00-7:25

If you want me to extract specific code examples or explain any part of this episode, just ask!

## Translation

Aqui está a tradução completa do texto do episódio 23, “Armazene o Estado em um Arquivo Externo”, da série "Learn Vue 3: Step by Step":

Certo, até agora revisamos, o quê, duas maneiras diferentes de compartilhar estado entre uma grande variedade de componentes. Então, basicamente, estamos falando aqui de estado global. Precisamos de um estado que possa ser acessado por qualquer componente que precise dele.

Começamos revisando o que é comumente conhecido como prop drilling. É quando você tem um dado, e passa para um componente, e esse componente passa para outro componente, e depois para o filho, e depois para o filho daquele, e assim por diante. E, muito rapidamente, isso se torna muito irritante.

Depois disso, no último episódio, revisamos `provide` e `inject`. Sim, isso funciona, e é melhor. Mas ainda não terminamos.

Então, neste episódio — talvez nos próximos dois episódios — quero te mostrar mais algumas opções que você pode considerar. Vamos lá.

Ainda estou usando aquele exemplo fictício do quiz do episódio anterior. Se eu visitar a Home View, você vai lembrar que nós definimos manualmente o estado inicial do quiz. Se você pensar bem, sempre poderíamos extrair isso e chamar de state.

Selecionamos tudo isso e atribuimos dentro do script setup. Agora, se eu fizer algo assim, teremos exatamente a mesma saída. Nada mudou aqui.

Mas agora pense: existe algo que te impede de armazenar esse estado, ou esses dados — que é o que são — em seu próprio arquivo? Hmm...

Vamos brincar com essa ideia. Que tal criar dentro do diretório src uma nova pasta chamada stores. E dentro dela, criamos um arquivo. Existem convenções para isso, mas por enquanto, vamos manter super simples e chamar de quizStore.

Legal. Agora, vou pegar tudo isso e armazenar nesse novo arquivo. E quero que isso seja acessível de fora. Então, vamos exportar assim:

```js
export const state = { ... }
```

Ainda temos um pouco a fazer aqui, mas sim, estamos testando essa ideia. E se pudéssemos colocar o estado em seu próprio arquivo, e então qualquer componente que precise desse estado simplesmente importe esse arquivo? Vamos tentar.

Voltamos para HomeView e agora vamos importar o que chamamos de state. Assim:

```js
import { state } from '@/stores/quizStore'
```

Vamos ver se funciona. Troco para o Chrome, dou um refresh, e sim, tudo parece estar funcionando. Mas só para ter certeza, vamos mudar o nome para "My Second Quiz". Voltamos e, sim, parece que só usamos aqui embaixo — mas está funcionando.

Legal, muito interessante. Agora vamos pensar: se eu for até Quiz.vue, vamos remover provide e inject. E, só para constar, isso ainda é uma opção válida. Estou apenas te mostrando abordagens diferentes.

Vamos remover completamente. E com essa abordagem, não vamos mais aceitar props. Em vez disso, vamos importar o estado do quiz diretamente.

Assim posso remover isso. Indo para QuizFooter, limpamos um pouco. Mesmo processo aqui. Veja como estamos eliminando a necessidade de fazer prop drilling.

Finalmente, lá em QuizFooterLinks, posso remover o inject completamente. Mais uma vez, importamos o estado. E então podemos atualizar isso, renomear, o que quiser.

Voltando... sim, tudo está funcionando exatamente como antes. Mas agora estamos usando uma forma alternativa de gerenciar nosso estado — especialmente um estado que precisa ser acessado globalmente ou por muitos componentes.

E sim, lembre-se: você não está limitado a uma única store. Pode criar quantos arquivos quiser. Talvez você tenha um para o usuário atual, outro para o carrinho de compras.

Esse é um ótimo exemplo. Porque com um carrinho de compras, você precisa acessar o estado dele na página inteira, ou seja, em muitos componentes. Talvez no topo, na barra de navegação, você tenha um rótulo mostrando o número de itens no carrinho. Em outro ponto, num painel flutuante, ele mostra o valor total.

Você entendeu a ideia. São situações em que você precisa acessar informações em muitos componentes. E uma store pode fornecer isso pra você.

Mas agora, claro, o que temos é muito simples e não é tão flexível assim. Vou te mostrar o que quero dizer.

Vamos adicionar um botão aqui com o texto “Mudar nome do quiz”. Quando clicar nele, vamos fazer:

```js
state.name = 'Um novo nome de quiz'
```

Vamos ver se isso funciona. Voltamos, o botão aparece, clico — e não, não atualiza.

Vamos analisar. Abrimos o Vue DevTools, descemos até o FooterLinks, e sim, atualizamos a propriedade name, mas não está sendo refletido. Isso porque só atualizamos uma string. Em nenhum momento dissemos que deveria ser reativa.

Então voltamos para nossa store e dizemos: "Ok, parece que esse state também precisa ser reativo."

Você já aprendeu sobre ref. Podemos usar reactive, que é especialmente útil para objetos.

```js
import { reactive } from 'vue'

export const state = reactive({
  name: 'My Second Quiz',
  ...
})
```

Agora, todos os itens dentro serão reativos.

Vamos testar de novo. Clico no botão e, com certeza, o estado foi atualizado e refletido em qualquer outro lugar que o utilizamos.

Só para deixar bem claro, vamos até QuizHeader, e mudamos para script setup. Importamos nosso state e atualizamos o título para o nome do quiz.

Damos um refresh, mudo o nome — e pronto! Atualizamos o estado global e ele é refletido em qualquer lugar que importamos o arquivo.

É uma abordagem absurdamente simples, mas sabe de uma coisa? Vai funcionar na maioria dos casos. Em muitas situações, isso é tudo o que você precisa.

Só quando começar a construir aplicações mais complexas que talvez encontre obstáculos — e esses obstáculos geralmente são:

"Esse estado mudou, e eu não sei por quê..."

"Preciso reagir quando esse estado muda, para atualizar o localStorage ou fazer uma requisição AJAX."

São nesses casos que você talvez precise de algo mais flexível.

E no próximo episódio, vou te mostrar o que é isso.