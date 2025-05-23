# Vite

### Great job, if you've made it this far. I think you're now ready to move on to part two of this series. Now that you understand many of the fundamentals of Vue, let's now figure out how to actually construct a single-page application using it. To demonstrate this, we'll pull in a first-party tool called 

Here is the full transcript of Episode 16 "Vite" from the "Learn Vue 3: Step by Step" series on Laracasts:

Okay, so if you made it this far, you know what, you go ahead and give yourself a little pat on the back. You deserve it. But I think that also means you're ready to move on to Part 2, and we are going to kick it up a notch. So far, we've reviewed many of the fundamentals, but you're probably still in this position where you're not sure how to put it all together. How do we actually build a website using Vue? Well that's what Part 2 is for. So why don't we get started with Vite.

If you're working along, visit vitejs.dev. And if you're curious about that word, it's simply French for the word quick. Vite is a build tool that takes care of our server, hot reloading, which basically means when I change text within a file, the browser instantly updates to reflect that change. And it also includes a build tool that will bundle up all of our code to make it as performant as possible. All right, let's give this a shot. So I'm going to visit my code directory.

In your case, just go to wherever you store your websites. And I'm going to run npm init vue, and I want the latest version. Now it's going to ask us some questions. The project name, why don't we say my-first-vue-project. All right, do we want TypeScript? No. JSX? No, we're not going to worry about that.

Do we want a router? Yes, we do. And I'll use the arrow keys for this. Next, do we need help with state management? Well, eventually, yes. But for now, let's keep it simple. And then finally, testing, we're going to skip that. Cypress is an amazing end-to-end testing framework, but again, we're going to skip all of that.

But I will pull in ESLint to help out with code quality, as well as prettier for code formatting. All right, so now it's asking us to run these commands. I will select that and paste it in. All right, here we go. So you can see I have Vue version 2.9 installed, and we have a dev server running at localhost 3000. We've now successfully created a project with Vite and Vue 3.

Let's have a look at the code base. In a new tab, I will CD into my first Vue project and open this in my editor of choice. Okay, so immediately I see a bunch of files here. Now, I will warn you, it's always a little overwhelming when you're introduced to a framework. You see a bunch of directories, a bunch of files, and you're not sure what any of them do. And yeah, you immediately kind of feel disheartened, like, here's something else I have to learn. Just stick with it, though.

Many of the things we've already learned are represented here, so you'll feel right at home pretty quickly. Let's first go into index.html, and you can see, yeah, we did something just like this in our project. It imports a main.js file, and it declares it as a module. All right, there's main.js. And yeah, we can recognize some of this. Notice we are importing createApp from Vue.

Before we imported Vue globally, and we just did something like this, where we said Vue.createApp. But it's the same thing. Okay? All right, next you can see it's importing an app file, and it's passing it to createApp. Now you'll remember, when we were first learning, we did everything inline, but then later we extracted it to a file, and the same is true here. Okay? So it's importing this file, and it looks like this is our root component.

So look, we have a header here with the Vue logo, and then a message that says, you did it. All right, let's see if we can find that in the browser. There we go. We have a header with a message that says, you did it. Okay, so check this out. If I tweak this file, it will instantly be represented on the page without requiring a reload.

And this is referred to as hot module replacement. So I delete that, and notice the image is now gone. In fact, let's delete the entire header. I'll save it. It recompiles and updates the browser. But let's bring that back real quick. If I now return to main.js, the only other thing you're not familiar with is this router. So if I showed you just this, I think you'd see, oh yeah, I'm very familiar with this.

We use Vue.createApp to build our app, we pass in our root component, and then we mount it to the page. And if we have a look at index.html, there it is. So all of that is super familiar to you, hopefully. The only thing you're not familiar with is Vue router. So we use Vue router by importing it, and then we say app.use(router). Now Vue router is a first party tool that's going to help us out when it comes to defining our routes, creating our links, history management, scroll position, memory, all of that stuff comes out of the box.

And we can see if I open up this router directory, here it is. Granted, this looks a little confusing, but the bread and butter is right here. This is where we can define an array of all of the routes, or all of the pages, that we want to respond to. So notice for the homepage, and you know what, I always like to keep things as simple as possible when I'm learning. So let's keep it just like this.

Okay, so now our application responds to a single route. If you visit this URI, or the homepage, we are going to load a component called HomeView. And you can see we are loading the HomeView from this path. Okay, so think of it like this. When you're building a traditional server side application, you're always going to have a Vue, some kind of block of HTML that responds to every URI. So for example, if I'm building a static website, if I visit /about in the browser, then there's probably something like an about.html file that returns the HTML.

Or if I'm building a Laravel app, and I visit /contact, well there's probably going to be something like a contact.blade.php file that has all of the data in the form. And the same is going to be true when we're building a single page application. So if the user visits the homepage, we need some kind of HTML to render. And that will be stored in the views directory. And notice real quick this convention where page specific Vue components have the suffix .vue and they are stored in a views directory rather than a general components directory. Very very common.

Now, if we have a look at this, it does feel a little foreign. This isn't quite what we've been reviewing in previous episodes. In previous episodes we had things like this where we exported an object where we declared the template, right? But now we have multiple tags here. I have a script tag, I have a template tag, I can even have a style tag. And also on that note, notice that the file extension is .vue rather than .js. Okay, .vue is a file type that we refer to as single file component.

It is a single file that contains your script, its respective template, and any optional styling that should go along with it. It's really cool, I think you're going to love it, and in fact I exclusively use single file components. All you really need to know though is whereas in the past you would export an object where you create the template, well now that template can be stored outside of the script tag. So if we just had something like this, hello world, like that, this would still work. We come back, give it a refresh, and now you have your component.

And of course you can inspect it like usual. So if we have a look here, I'm going to click on this little icon, and this lets me hover over the browser to select any Vue components it finds. So here's our app component, and there is our home view.

Okay, so let's do this to wrap up. I'm going to bring it back to what we had before. I fully expect this to be somewhat confusing. We're introducing a bunch of new concepts here, even things like this where we're using camel casing instead of things like the welcome. Well you can actually do both, but nonetheless these are all little changes that can be a bit overwhelming. So I think you should fully expect that. And don't worry, you're going to figure it out, I promise.

But why don't we finish up the episode by just figuring out how we can add another page. And hopefully that'll get you a little excited. Right now we have a home page and an about page, but notice that's blank. That's because I cleared out the router. So let's bring it back. Alright, a home page and about page. Let's do one more.

So let's do this. I will take about view, I'll duplicate it, and I'm going to call it contact view. And this will be the contact page. And we'll update this as well.

Alright, so I have my component here, but it's not like we can visit that page yet. So for example, if I go to /contact, yeah, that's not going to work. And in fact, notice if I open up the console, no match found for location with path contact. Alright, let's set up a route. So we go into our router, and we'll do another one right here. If you visit /contact, we'll give it a name of contact, and that should load a component called contact view. Alright, let's import that up here, like so.

Now if I come back, there we go. It works. Okay, so now the only remaining step is to create a link to that contact page. Let's do that now. We'll go into app.vue, and here's our navigation for the entire site. And notice we have these router links, and that's pulled in right here. And again, think of this sort of like an anchor tag on steroids. Of course, ultimately, it's going to render an anchor tag, but yes, of course, it has extra behavior to respond, to deal with history, to deal with potential scroll management, a bunch of things like that.

So I'm going to add a new one here, and that will link us to /contact. Alright, so let's switch back, and there we go. We have the contact page, contact, about, home, and it's blazing fast.

Okay, so admittedly, you should feel a little overwhelmed at this point. So if you do, trust me, that's par for the course. Just work along and play around with it. Work through the editor, see what each file does, tweak things, see how that affects what's loaded in the browser. And when you're ready, let's move on to the next episode.

Oh, and don't forget, if you have any questions along the way, please do ask in the comments below, and one of us will try to help out. Okay, onward to the next episode.

You can also view the transcript in segments with timestamps here: 0:00-10:00, 10:00-20:00, etc.

If you want me to extract or explain any specific part of this episode, just ask!


## Translation

Aqui está a transcrição completa do Episódio 16 "Vite" da série "Learn Vue 3: Step by Step" do Laracasts:

Certo, então se você chegou até aqui, sabe de uma coisa? Pode se dar um tapinha nas costas. Você merece. Mas acho que isso também significa que está pronto para passar para a Parte 2, e agora vamos elevar o nível. Até agora, revisamos muitos dos fundamentos, mas você provavelmente ainda está naquela fase em que não sabe como juntar tudo. Como realmente construímos um site usando Vue? Bem, é para isso que serve a Parte 2. Então, por que não começamos com o Vite?

Se estiver acompanhando, visite vitejs.dev. E se estiver curioso com essa palavra, ela significa simplesmente "rápido" em francês. __Vite é uma ferramenta de build que cuida do nosso servidor, recarregamento automático — o que basicamente significa que, quando eu altero um texto em um arquivo, o navegador atualiza instantaneamente para refletir essa mudança. E também inclui uma ferramenta de build que empacota todo o nosso código para torná-lo o mais performático possível__. Certo, vamos tentar. Vou visitar meu diretório de código.

No seu caso, vá para onde você armazena seus sites. E vou executar npm init vue, e quero a versão mais recente. Agora ele vai nos fazer algumas perguntas. Nome do projeto? Vamos dizer "meu-primeiro-projeto-vue". Certo, queremos TypeScript? Não. JSX? Não, não vamos nos preocupar com isso.

Queremos um roteador? Sim, queremos. E vou usar as setas para isso. A seguir, precisamos de ajuda com gerenciamento de estado? Bem, eventualmente sim. Mas por enquanto, vamos manter simples. E finalmente, testes — vamos pular isso. __Cypress é uma estrutura de testes de ponta a ponta incrível, mas novamente, vamos pular tudo isso__.

__Mas eu vou adicionar o ESLint para ajudar com a qualidade do código, e o Prettier para formatação__. Certo, agora ele pede para rodarmos esses comandos. Vou copiar e colar. Pronto. Você pode ver que tenho o Vue versão 2.9 instalado, e um servidor de desenvolvimento rodando em localhost:3000. Agora criamos com sucesso um projeto com Vite e Vue 3.

Vamos dar uma olhada na base de código. Em uma nova aba, vou entrar no diretório do projeto Vue e abrir no meu editor favorito. Imediatamente vejo vários arquivos. Agora, vou avisar: sempre é um pouco assustador quando você é apresentado a um framework. Você vê vários diretórios, arquivos, e não sabe o que cada um faz. E sim, você se sente desanimado, tipo "lá vem mais coisa pra aprender". Mas continue firme.

Muitas das coisas que já aprendemos estão aqui, então você vai se sentir em casa rapidamente. Vamos primeiro abrir o index.html, e você verá, sim, fizemos algo assim no nosso projeto. Ele importa o arquivo main.js e declara como um módulo. Certo, aqui está o main.js. E sim, reconhecemos algumas coisas. Veja que estamos importando createApp do Vue.

Antes importávamos o Vue globalmente e fazíamos algo assim: Vue.createApp. Mas é a mesma coisa, ok? Agora, veja que está importando um arquivo App e passando para o createApp. Você deve se lembrar que, no início, fazíamos tudo inline, mas depois extraímos para um arquivo, e aqui é a mesma coisa. Estamos importando esse arquivo, que parece ser nosso componente raiz.

Veja, temos um cabeçalho com o logo do Vue e uma mensagem "Você conseguiu!". Vamos ver isso no navegador. Aqui está, cabeçalho com a mensagem "Você conseguiu!". Agora veja isso: se eu modificar esse arquivo, a mudança aparece instantaneamente na página, sem recarregar.

Isso é o chamado __Hot Module Replacement__. Se eu deletar a imagem, ela some. Se eu deletar o cabeçalho todo e salvar, ele recompila e atualiza o navegador. Mas vamos trazer isso de volta. No main.js, o único item novo é o router. Se eu mostrasse só isso, você diria “ah, já conheço isso”.

Usamos Vue.createApp para construir o app, passamos o componente raiz e montamos na página. E se olharmos o index.html, está lá. Tudo isso deve parecer bem familiar. O único item novo é o Vue Router. Usamos o Vue Router importando e dizendo app.use(router). É uma ferramenta oficial que nos ajuda a definir rotas, criar links, gerenciar histórico, rolagem e mais.

Se abrirmos o diretório router, lá está. Pode parecer confuso, mas o essencial está aqui: definimos um array com todas as rotas (ou páginas) que queremos responder. Para a home, por exemplo — __e gosto de manter simples ao aprender__ — mantemos assim.

Nosso app responde a uma única rota. Se visitar a URI / (homepage), ele carrega o componente HomeView, que vem de um determinado caminho. Pense assim: num app tradicional, cada URI tem uma view com HTML. Em um site estático, visitar /sobre carrega sobre.html. Em um app Laravel, visitar /contato carrega um contato.blade.php com os dados e o formulário.

Com single-page apps é o mesmo: se o usuário visita a homepage, precisamos de um HTML. Ele fica no diretório views. E veja esse padrão: __componentes específicos de página têm sufixo .vue e ficam em views, não em components. Isso é muito comum__.

O arquivo pode parecer estranho. Antes, exportávamos um objeto com template, __agora temos múltiplas tags: `<script>`, `<template>`, e até `<style>`. E o arquivo agora termina com .vue, o que chamamos de Single File Component (SFC)__.

__É um único arquivo com script, template e estilos__. Muito legal — eu uso exclusivamente SFCs. Tudo que você precisa saber é que, enquanto antes o template ficava dentro do script, agora ele pode estar separado. Por exemplo, <template>Hello world</template> já funciona.

Podemos inspecionar como sempre. Clico no ícone de inspeção, passo o mouse e vejo os componentes Vue. Aqui está o App e o HomeView.

Para encerrar, vamos ver como adicionar uma nova página. Temos uma home e uma about. Mas a about está vazia — porque limpei o router. Vamos restaurar.

Ok, temos home e about. Vamos criar mais uma: duplico a AboutView, chamo de ContactView.vue e atualizo para ser a página de contato.

Mas não adianta só criar o componente. Se eu visitar /contact, não funciona. No console, erro: "nenhuma rota corresponde ao caminho contact". Vamos criar a rota.

No router, adiciono uma nova rota: path /contact, nome contact, e carrega ContactView. Importamos no topo, e agora funciona.

Só falta criar um link para essa página. __No App.vue, temos a navegação do site com router-link. Ele é como uma `<a>` com superpoderes: renderiza um link normal, mas com comportamento extra (histórico, rolagem, etc.)__.

Adiciono um link para /contact, e pronto. Temos navegação entre contato, about e home — super rápido.

__Admito: é normal se sentir sobrecarregado neste ponto. Mas continue. Mexa no editor, explore os arquivos, veja o que fazem, altere e veja o resultado no navegador. Quando estiver pronto, vamos para o próximo episódio.__

Ah, e se tiver dúvidas, pergunte nos comentários. Alguém vai tentar ajudar. Vamos para o próximo episódio.