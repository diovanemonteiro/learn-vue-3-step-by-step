# Direct Mutation Concerns

###

Here is the full transcript for Episode 24, "Direct Mutation Concerns," from the "Learn Vue 3: Step by Step" series on Laracasts:

All right, welcome back. So in just a little bit, maybe the next video, I will introduce you to a tool called Pymia. But you know what? Why don't we take five minutes or so and just talk a little bit more about how you would wire this up yourself. Okay. So let's do this. Why don't we introduce a new page here? I want to show you an incredibly simple example, and we'll use the common counter. So we'll call this counter view.

I want to show you an incredibly simple example, and we'll use the common counter. So we'll call this counter view. And of course, right now, just creating the page doesn't change anything. I have to register it with the router and then add the link here. Okay. So this will be a nice little recap into my router. Let's add a new one here. If the user visits counter, this will have a name of counter, and then it will load a component called counter view. And I'll need to import that at the top.

Component called counter view. And I'll need to import that at the top. Import counter view. Like so. All right. Next, if I go into app.view, here's our navigation. So I will add a new one here for our counter. And let's have a look. Yeah. So now if I click on it, we have a dedicated page for our counter.

Yeah. So now if I click on it, we have a dedicated page for our counter. And don't worry, this is going to be pretty basic. So we'll have an H1 here where we track the count. Yeah. Granted, this is a laughably basic example, but we're going to go with the idea that we need to access this counter from other pages in our application. So with that in mind, I'm going to use a dedicated store, right? Here's our store directory. And we'll call it counter store.js.

Here's our store directory. And we'll call it counter store.js. And just like we did before, we'll declare our counter. It'll be reactive. And to start, we'll have a count that initializes to zero. Finally, I will export this. All right. Let's get going. So now in counter view, I can import that and then reference it like so. Counter.count.

So now in counter view, I can import that and then reference it like so. Counter.count. All right. Let's have a look in the browser. And yeah, this is going to work. And you know what? This is fine. But in fact, if you have a look at the view documentation, they will somewhat discourage this approach, this approach of referencing and mutating the state directly. Instead, they would recommend that you use a method.

This approach, this approach of referencing and mutating the state directly. Instead, they would recommend that you use a method. And I think that's fair. But you know what? Just one thing. The documentation would say it's OK for small projects. But once you get a little bit larger, you shouldn't take that approach. Just keep in mind, are you sure you're not building a small project? Everyone likes to imagine they're building the next Twitter. And maybe you are.

Everyone likes to imagine they're building the next Twitter. And maybe you are. Or maybe you're building something pretty small. So just keep that in mind. Always choose the simplest approach that will get the job done. And yeah, maybe you will eventually get to a point where for the application you're building, you need something not so simple. But yeah, just keep that in mind, OK? So now if we come back to our counter store, if we were to switch over to a method, we might have one like increment.

So now if we come back to our counter store, if we were to switch over to a method, we might have one like increment. And this can now be exclusively responsible for incrementing the count. And we get the benefit of assigning a dedicated name to what this action is. And in fact, you're going to start seeing these referred to as actions. So you can imagine this being your state, which is effectively the data. And then methods like this will sometimes be called actions. But again, state, data, method, action, they're all kind of the same thing. You can use them interchangeably. OK, cool.

You can use them interchangeably. OK, cool. So now if I come back, instead of mutating directly, I can instead call a method, counter.increment. And now we'll get the exact same thing as we had before. Pretty cool. And of course, the benefit now is, well, it's a little bit easier to debug this. For example, maybe we are incrementing the count somewhere in the application, but you're not sure why. Well, now you have a dedicated place to, for example, debug, do a console.log. You could even add guard logic.

Well, now you have a dedicated place to, for example, debug, do a console.log. You could even add guard logic. So for example, maybe, just as a silly illustration, maybe if the count is 10, then we don't go over that for some weird reason. We don't go above 10. This counter is good for 1 through 9, not 10 or 11. So if that's the case, we will return. Yeah, now you have a dedicated place to store logic and behavior and guard clauses like this. So yeah, now if we go up, we should be able to increment to 10.

This. So yeah, now if we go up, we should be able to increment to 10. But if I keep clicking, it will not go beyond that. OK, so yeah, that's definitely a benefit to this approach. And again, whether you call this a method or an action, they're kind of interchangeable. I only bring up these terms because once we, in the next episode, review a tool called Pinya, you're going to see these terms like getters, actions, state. But they're really just data, methods, computed properties, kind of the same thing. So yeah, think about it. Now, if we need to access the current count from any of the pages in our application,

So yeah, think about it. Now, if we need to access the current count from any of the pages in our application, it's really easy to do so. Whereas if we had instead stored it all on counter view, like maybe you had something like this, well, then it's not so easy. Because as soon as I switch to a different page, the counter view is swapped out with a totally different view. And we no longer have access to that data. So let's just have a look. Maybe the user goes to about page.

So let's just have a look. Maybe the user goes to about page. We're going to import our counter. And now I can say the current count is counter.count. All right, let's see. Give it a refresh. Let's go to number six. And if I switch to about, yes, we have access to that state. And that is the huge benefit to an approach like this. Okay, so hopefully you're getting a little bit more comfortable with creating your own

And that is the huge benefit to an approach like this. Okay, so hopefully you're getting a little bit more comfortable with creating your own stores. And again, I want to stress, you know what, this might be all you need. It just depends on what you're building. But there are some benefits to using a dedicated tool. So with that in mind, in the next episode, I promise, I'm going to show you a tool called Pina.

You can also view the transcript with timestamps here: 0:00-6:16

If you'd like, I can also provide code examples or explanations from this episode!


## Translation

Claro! Aqui está a tradução completa do texto que você forneceu — a transcrição do Episódio 24 da série Learn Vue 3: Step by Step, intitulado “Preocupações com Mutação Direta”:

Muito bem, bem-vindo de volta. Então, em breve — talvez no próximo vídeo — eu vou te apresentar a uma ferramenta chamada Pinia. Mas sabe de uma coisa? Por que não tiramos uns cinco minutos para conversar um pouco mais sobre como você mesmo pode configurar isso? Ok. Vamos fazer o seguinte: vamos criar uma nova página aqui. Quero te mostrar um exemplo incrivelmente simples, e vamos usar o famoso contador. Vamos chamar essa página de CounterView.

Quero te mostrar um exemplo incrivelmente simples, e vamos usar o famoso contador. Vamos chamar essa página de CounterView. E claro, por enquanto, só criar a página não muda nada. Eu preciso registrá-la no roteador e então adicionar o link aqui. Certo. Isso será uma boa recapitulação do roteador. Vamos adicionar uma nova rota aqui. Se o usuário visitar "/counter", essa rota terá o nome counter e irá carregar o componente CounterView. E eu preciso importá-lo no topo do arquivo.

Componente chamado CounterView. Preciso importá-lo no topo. Importar CounterView. Assim. Certo. Agora, se eu for até o App.vue, aqui está a navegação. Vou adicionar um novo link aqui para o contador. Vamos dar uma olhada. Sim, agora se eu clicar, temos uma página dedicada para o nosso contador.

E não se preocupe, isso vai ser bem básico. Vamos ter um `<h1>` aqui onde mostramos o valor atual do contador. Sim, é um exemplo ridiculamente simples, mas vamos partir da ideia de que precisamos acessar esse contador a partir de outras páginas da aplicação. Com isso em mente, vou criar uma store dedicada. Aqui está o diretório stores. Vamos chamá-la de counterStore.js.

Assim como fizemos antes, vamos declarar nosso contador. Ele será reativo. E para começar, terá um campo count iniciado em zero. Por fim, vamos exportar isso. Pronto. Agora em CounterView, posso importar isso e usar assim: counter.count.

Vamos dar uma olhada no navegador. E sim, isso vai funcionar. E quer saber? Isso está OK. Mas na verdade, se você olhar a documentação do Vue, eles desencorajam um pouco essa abordagem — de referenciar e mutar diretamente o estado. Em vez disso, eles recomendam o uso de métodos.

Essa abordagem de referenciar e alterar diretamente o estado... Em vez disso, o recomendado é usar um método. E eu acho isso justo. Mas veja bem: a documentação diz que isso é aceitável para projetos pequenos. Mas uma vez que o projeto cresce um pouco, você não deveria seguir essa abordagem. Só lembre: você tem certeza que não está construindo um projeto pequeno? Todo mundo gosta de imaginar que está construindo o próximo Twitter. E talvez você esteja.

Ou talvez esteja construindo algo bem pequeno. Então mantenha isso em mente. Sempre escolha a abordagem mais simples que resolve o problema. E sim, talvez você chegue a um ponto em que precisa de algo mais robusto. Mas guarde isso, ok?

Agora, voltando à nossa counterStore. Se fôssemos mudar para um método, poderíamos criar algo como increment. Esse método agora será o único responsável por incrementar o contador. E temos o benefício de dar um nome claro à ação que está acontecendo.

Na verdade, você vai começar a ver isso sendo chamado de ação (action). Então você pode imaginar que state é basicamente os dados, e métodos como esse são ações. Mas, novamente: estado, dados, método, ação — são todos conceitos semelhantes. Pode usá-los de forma intercambiável. Certo, legal.

Agora, se eu voltar, em vez de mutar diretamente (counter.count++), posso chamar o método counter.increment(). E teremos o mesmo resultado de antes. Bem legal. E claro, o benefício agora é que isso facilita um pouco o debug. Por exemplo, talvez o contador esteja sendo incrementado em algum lugar da aplicação, mas você não sabe por quê. Agora, você tem um local específico onde pode, por exemplo, adicionar um console.log. Você poderia até adicionar uma lógica condicional.

Como exemplo (ainda que bobo): talvez, se o contador for 10, você não queira ir além disso por algum motivo. Esse contador só é válido de 1 a 9, não 10 ou 11. Nesse caso, podemos retornar. Agora temos um local dedicado para armazenar lógica, comportamento e cláusulas de segurança como essa. Então, agora se clicarmos, podemos incrementar até 10.

Mas se eu continuar clicando, ele não passará de 10. Ok, então esse é um benefício claro dessa abordagem. E de novo: método ou ação são termos intercambiáveis. Eu só menciono isso porque no próximo episódio, quando falarmos da ferramenta Pinia, você verá termos como getters, actions, state. Mas no fundo, eles são só dados, métodos e propriedades computadas — basicamente a mesma coisa.

Agora, pense nisso: se você precisa acessar o valor atual do contador de qualquer página da aplicação, isso é muito fácil de fazer. Já se você tivesse armazenado tudo dentro do CounterView, como algo assim:

```js
<script setup>
const count = ref(0)
</script>
```

Bem, então não seria tão fácil. Porque assim que você troca de página, o componente CounterView é destruído e perdemos o acesso àquele dado.

Vamos fazer um teste: talvez o usuário vá para a página "About". Vamos importar nosso counter. E agora podemos dizer: “O contador atual é counter.count”.

Vamos ver. Atualize a página. Vá até o número 6. Agora vá para "About". Sim! Temos acesso a esse estado. E esse é o grande benefício dessa abordagem.

Espero que você esteja ficando mais confortável com a criação de suas próprias stores. E novamente: talvez isso seja tudo que você precise. Depende do que você está construindo. Mas existem alguns benefícios em usar uma ferramenta dedicada. Então, com isso em mente, no próximo episódio, prometo que vou te mostrar uma ferramenta chamada Pinia.


## Summary