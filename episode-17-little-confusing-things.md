# Little Confusing Things

###

Here is the full transcript for Episode 17, "Little Confusing Things," from the "Learn Vue 3: Step by Step" series:

All right, so at this point, if you're working along, you should have worked your way through some of the files and, you know, just lightly familiarized yourself with the general codebase. So now for this episode, I've identified a handful of things that I think might be a little confusing to you. So let's clear that up right now. First up, if we go into app.vue, you may notice this import at the top has a squiggly here, almost like my editor can't figure out how to find it. And second, what is this alias here? At symbol, components, hello world. Well, clearly we are pointing to this file here, but what is that at symbol?

At symbol, components, hello world. Well, clearly we are pointing to this file here, but what is that at symbol? Okay, this is referred to as an alias. If we visit our Vite config file, you can see it's setting one up right here. So we're effectively creating an alias called at symbol, and that will resolve to a file path to this source directory, which means effectively what we're doing here is instead of saying, all right, go into the current directory, but then into components and then hello world, and notice the squiggly goes away, instead we can use this alias here. And now, no matter how many nested directories we are in, we can always use this at symbol to point to that source directory.

And now, no matter how many nested directories we are in, we can always use this at symbol to point to that source directory. Okay, but yeah, you can see, at least in my editor, phpStorm, it's a little confused here. So to fix this, we need to give phpStorm a little more information. So unfortunately, this requires a bit of duplication. Create a file called jsconfig.json. And within here, create an object with a compiler options property. So within here, we will declare some paths. And specifically, I want to say, all right, look for that alias symbol followed by a star. That's a regular expression, meaning anything.

And specifically, I want to say, all right, look for that alias symbol followed by a star. That's a regular expression, meaning anything. And I want that to resolve to the source directory, like so. Yeah, so you can see I'm kind of duplicating what we have here. The problem is phpStorm doesn't know about Vite at the time of this recording, but it will know about this jsconfig.json file. So now yeah, we're just setting up an alias, anything at symbol followed by characters, I actually want it to go to that source directory. So now if I go back to app.view, there we go. You can see that squiggly goes away.

So now if I go back to app.view, there we go. You can see that squiggly goes away. And now I can, for example, command click to instantly visit that file. All right, so that's item number one. The next thing is you're now familiar with these router links. And again, this is really important to understand. If I were to replace this with a basic anchor tag, like so, well, think about what would happen here. Let's give it a try in the browser. I will run npm run dev.

Let's give it a try in the browser. I will run npm run dev. And actually on that note, npm run dev, that is being declared in your package.json file. You can see there is an npm script called dev, and all that does is run Vite. Which means if you want, you could just as easily say npx Vite. Okay, so now we have a dev server at localhost 3000. All right, and here we go. Actually real quick, looks like we have a little typo. Let's go back into this, oh I'm sorry, roster view, how did I do that? Okay, so anyways, yeah, notice if I click on the about page, it's instant.

Let's go back into this, oh I'm sorry, roster view, how did I do that? Okay, so anyways, yeah, notice if I click on the about page, it's instant. We're not performing a full page refresh. And you can see that. If I click on contact, yeah, you don't see that loading bar. However, because we switched the home link back to an anchor tag, well yes, it's going to work. But notice that it did perform a full page refresh. So whenever you want to link to a page and have it be dynamic and done through Ajax, you need to use a router link.

So whenever you want to link to a page and have it be dynamic and done through Ajax, you need to use a router link. Okay, and that should do the trick. Home, about, or contact. Perfect. Okay, but next, what about this router view section? This is confusing. Well, let's do this. Let's put these side by side. And now let's see what happens if I remove it entirely.

Let's put these side by side. And now let's see what happens if I remove it entirely. Run it. Oh, and notice we don't show the contact view at all. If I go to home, yep, we don't see it. So bring it back, that works. If I go to about, that works. But if I remove it, it disappears. Okay, so clearly what we can see is this will display the corresponding view component for whatever component matches the current route.

Okay, so clearly what we can see is this will display the corresponding view component for whatever component matches the current route. Say that three times fast. Really what's going on though is if we go into our router here, notice we have these routes set up and we say, well, if the URI is this, then this is the corresponding component we want to display. Or if the URI is this, then this is the corresponding component. So of course, if we go into app.view, I can't just hard code something. I can't just say about view here. So if I were to import that fully and give this a refresh, yeah, that's going to work.

I can't just say about view here. So if I were to import that fully and give this a refresh, yeah, that's going to work. But now we're going to see about view for every single page. And of course, the point is we want this to be dynamic. And that's what router view does. It will display the appropriate view component that corresponds to the current URI. And our router is telling us that, for example, this URI corresponds to home view. So if we click through there, sure enough, it's showing a welcome page. So if I were to change this and say, hello, I'm home and give this a save, sure enough, that updates on the fly.

So if I were to change this and say, hello, I'm home and give this a save, sure enough, that updates on the fly. All right, next up, item number three. If we bring this back, up until the installation of this project, we would reference our components using a dash like this. So notice if I save this, everything still works. So there's no problem there. It just turns out that it's a pretty common convention to use this syntax here. And in fact, for the layer cast code base, as an example, this is exactly what I do. The only reason why we use dashes is because sometimes when we're referencing it globally

And in fact, for the layer cast code base, as an example, this is exactly what I do. The only reason why we use dashes is because sometimes when we're referencing it globally or we're using templates, we still need to use a syntax that the browser can understand. However, in this case where we're compiling, there's no problem whatsoever. So we can stick to this syntax from now on. All right, next up. What about this word the in the name of the file? It's kind of weird. If we go everywhere else, hello world, welcome item, contact view, why does this one alone contain the word the?

If we go everywhere else, hello world, welcome item, contact view, why does this one alone contain the word the? Okay, well, once again, as you'll find with many things, this just comes down to a basic convention. So the general idea is whenever you have a component that's really just sort of like a partial, it's only ever going to be used exactly one time throughout the entire project. It's a common convention to proceed it with the word the. And again, that's just a hint to anyone who looks at this file six months from now that hey, this is sort of a one-time thing, and that's why we call it the welcome. There's no situation where we're going to have, for example, five different instances of this component.

There's no situation where we're going to have, for example, five different instances of this component. It's a one-time thing. So in those cases, yeah, you don't have to, but it's a common convention to proceed it with the word the. Okay, so let's open up this welcome section. And yeah, you can see it's divided into all of these welcome item. So here's one, here's another one, here's another one. And of course, that corresponds to each one of these as well. So this is a common thing, we even worked on this a few episodes ago, to reduce code

And of course, that corresponds to each one of these as well. So this is a common thing, we even worked on this a few episodes ago, to reduce code and style duplication. Think about it. In this case, every one of these welcome item sections contains an icon, a heading, and then a description. So let's see what we have here. All right, a section to define the icon. And notice we have that hash, and we learned about it a few episodes ago, so that should be pretty familiar.

And notice we have that hash, and we learned about it a few episodes ago, so that should be pretty familiar. Next we have a section for the heading itself, and that's called documentation. And then finally, it looks like the default slot goes right here. So if I remove that, it goes away. If we want to change the heading to docs, that updates. If we want to use a totally different icon, of course we can. Okay, let's dig into a welcome item. And yeah, oftentimes the components you create will be almost like basic skins, where you can deposit HTML or text wherever it needs to go.

And yeah, oftentimes the components you create will be almost like basic skins, where you can deposit HTML or text wherever it needs to go. Now, no matter how many welcome items you have, you don't have to repeat yourself over and over. Instead, we just say, okay, let's create a new welcome item, and here's the icon I want to use, and here's the heading I want to use, and here's where my default content should go. But what's cool about View Components is we can define the template outside of the script, which makes it a little more flexible. And then also notice that we can create styles within the same file.

which makes it a little more flexible. And then also notice that we can create styles within the same file. So a View Component allows you to declare the HTML, the script behavior, and the styling all within a single file, which is really neat. But of course, don't forget, these things are all optional. So if, in your case, you don't like doing your styles here, you want it to be in a traditional app.css file, well, of course, you could always, using a bundler, you could extract all of this into an app.css file. But otherwise, if you just want everything contained in the same place, you could select everything and extract it manually.

But otherwise, if you just want everything contained in the same place, you could select everything and extract it manually. So there's nothing that says you have to create styles within a .ViewComponent. It's just an option if you want to. Next, notice in this particular file, there's no script section. So notice there's nothing like this, where we export an empty object. In the case of welcome items, there really is no special logic or behavior. So in those cases, we can omit the script section entirely. And yeah, I think you'll find that components like this can be incredibly useful. Okay, so now let's say, I don't know, let's pick one of these random ones for ecosystem.

And yeah, I think you'll find that components like this can be incredibly useful. Okay, so now let's say, I don't know, let's pick one of these random ones for ecosystem. So that corresponds to this. Right at the bottom, why don't we say, now visit the about page. And as you learned, we can't just use an anchor tag. So if I created an anchor tag to about, well, actually, of course, you can do that. Just remember, once again, that's going to perform a full page refresh. So even when you're outside of your main route section, if you ever want to link to a different page, I just want to make this crystal clear, and that's why I'm circling back. Make sure that you import router link from ViewRouter.

page, I just want to make this crystal clear, and that's why I'm circling back. Make sure that you import router link from ViewRouter. And you'll see that, I guess I have to do it right here. Import router link. Import router link from ViewRouter. Okay, and now this is an easy one to miss. Don't forget to update your href or your heref to a to property. Okay, so now we try it again, and this time it instantly visits the page without performing a full page refresh. So yeah, what was that?

Four or five, just little things that might have tripped you up. So again, hopefully you're starting to get a little more comfortable. In the next episode, though, I'm going to push you even further.

You can also watch the episode directly here: 0:34-10:52

Let me know if you want me to extract or explain any specific part!


## Translation

Aqui está a tradução completa do texto que você enviou sobre o Episódio 17 - "Little Confusing Things" da série "Learn Vue 3: Step by Step":

Muito bem, então neste ponto, se você está acompanhando, já deve ter explorado alguns dos arquivos e, sabe, se familiarizado levemente com a base de código em geral. Agora, para este episódio, eu identifiquei algumas coisas que podem ser um pouco confusas para você. Então, vamos esclarecer isso agora.

Primeiro: se abrirmos o App.vue, você pode notar que este import no topo tem uma linha ondulada, como se meu editor não conseguisse encontrar esse caminho. E segundo: o que é esse alias aqui? Arroba, componentes, HelloWorld? Bom, claramente estamos apontando para este arquivo aqui, mas o que é esse símbolo de arroba?

Esse símbolo de arroba é chamado de alias. Se formos ao nosso arquivo de configuração do Vite (vite.config.js), podemos ver que está sendo configurado aqui. Então, estamos basicamente criando um alias chamado @, e ele irá resolver para o caminho da pasta src. Isso significa que, em vez de dizer algo como "vá para o diretório atual, depois para components, e depois para HelloWorld", podemos usar esse alias @. Assim, não importa quantos diretórios aninhados estejamos, sempre podemos usar @ para apontar para a pasta src.

Mas você pode ver que, pelo menos no meu editor (PhpStorm), ele ainda fica um pouco confuso. Para corrigir isso, precisamos dar mais informações ao PhpStorm. Infelizmente, isso exige um pouco de duplicação. Crie um arquivo chamado jsconfig.json. E dentro dele, crie um objeto com a propriedade compilerOptions. Dentro disso, vamos declarar alguns caminhos. Especificamente, queremos dizer: procure pelo alias @ seguido de qualquer coisa (usamos * como coringa).

E queremos que isso resolva para o diretório src. Então, basicamente estamos duplicando o que já temos no Vite. O problema é que o PhpStorm, no momento desta gravação, não entende o Vite, mas ele entende o arquivo jsconfig.json. Então agora, qualquer coisa que comece com @, o editor sabe que deve resolver para a pasta src. Se voltarmos ao App.vue, pronto — a linha ondulada desaparece. E agora eu posso, por exemplo, dar um comando + clique e ir direto para aquele arquivo.

Beleza, isso foi o item 1.

Agora, item 2: você já deve estar familiarizado com os router-link. Isso é muito importante de entender. Se eu trocasse por uma tag <a> básica, pense no que aconteceria. Vamos testar no navegador. Eu vou rodar npm run dev.

Na verdade, esse comando está sendo declarado no seu package.json, como um script dev que executa o Vite. Então, se quiser, você pode usar npx vite diretamente. Agora temos o servidor de desenvolvimento rodando no localhost:3000.

Se eu clicar na página "about", a transição é instantânea — sem recarregar a página inteira. Mas, como trocamos o link da página "home" para uma tag <a>, sim, ainda funciona, mas faz um reload completo da página. Ou seja: sempre que você quiser fazer uma navegação dinâmica via Ajax (sem recarregar), use o <router-link>.

Item 3: e essa <router-view>? Isso pode confundir. Vamos colocar lado a lado. E veja o que acontece se eu remover o <router-view>. Rodando... Perceba que a view de contato não aparece. Se eu for para "home", também não aparece. Voltando a <router-view>, funciona novamente. Ou seja, essa tag serve para exibir o componente da rota atual.

O que está acontecendo é: no nosso router, definimos rotas, tipo: se a URL for /, então exibe HomeView.vue. Se for /about, exibe AboutView.vue. Logo, se eu removo <router-view> de App.vue, não há onde injetar essas views. Eu até poderia importar diretamente o AboutView e colocar ali — e ele apareceria, mas apareceria em todas as páginas. Não é isso que queremos. Queremos algo dinâmico, e é isso que o <router-view> faz.

Item 4: antes de instalar este projeto, referíamos componentes com hífen (ex: <welcome-item>). Isso ainda funciona, mas uma convenção comum, usada inclusive na Laracasts, é usar PascalCase: <WelcomeItem />. Usamos hífen quando queremos que o navegador entenda sem precisar compilar. Mas como estamos compilando com o Vite, não tem problema usar PascalCase.

Item 5: por que o nome de um componente é "TheWelcome.vue"? Todos os outros são HelloWorld.vue, ContactView.vue... Por que este tem "The"? Isso também é convenção. Quando você tem um componente que é mais "parcial", ou seja, só será usado uma única vez no projeto, é comum nomeá-lo com "The" (tipo TheHeader, TheFooter, TheSidebar). Isso ajuda quem estiver lendo o código a entender que é algo único e não reutilizável.

Abrindo o TheWelcome.vue, vemos vários WelcomeItems. Cada um tem um ícone, um título e uma descrição. Tudo bem organizado. Vimos isso nos episódios anteriores — é uma forma de reduzir repetição de código e estilos. E cada WelcomeItem funciona como um componente "skin", onde você injeta HTML ou texto conforme precisar.

Você define o componente WelcomeItem com espaços para ícone (slot #icon), título (slot #title) e um slot padrão para o conteúdo. Você pode mudar o título, o ícone, ou o conteúdo facilmente, sem precisar duplicar a estrutura HTML várias vezes.

E o mais legal: com componentes Vue, você pode definir template, script e estilo no mesmo arquivo .vue, o que torna tudo mais organizado. Mas isso é opcional. Se preferir, você pode extrair os estilos para um arquivo CSS separado, como app.css.

Inclusive, WelcomeItem.vue nem tem a seção <script>, porque não precisa de lógica específica. E isso é ótimo — você pode omitir essa parte quando não for necessária.

Por fim, vamos pegar um item qualquer (como "Ecosystem") e adicionar um link para a página "About". Mas lembre-se: se usar <a href="/about">, isso recarrega a página. Para evitar isso, use <router-link>, mesmo fora da <router-view>. É só importar RouterLink do Vue Router e usar no seu template.

Certo, e agora essa é fácil de deixar passar. Não se esqueça de atualizar seu href — ou seu heref — para a propriedade to. Certo, então agora tentamos de novo, e desta vez ele visita a página instantaneamente, sem fazer um refresh completo da página.

Então é isso, né? Quatro ou cinco coisinhas que talvez tenham te atrapalhado. Então, mais uma vez, espero que você esteja começando a se sentir um pouco mais confortável.

No próximo episódio, no entanto, vou te desafiar ainda mais.

## Summary

In Episode 17, "Little Confusing Things," Jeffrey clears up several small but important points that often confuse beginners working with Vue 3 and Vite.

He starts by explaining the use of the @ alias in import statements. This alias points to the src directory, set up in the Vite config, allowing imports to be cleaner and independent of the current file's nesting level. To fix editor warnings (like in PhpStorm), you need to create a jsconfig.json file that duplicates this alias mapping so the editor understands it. 0:34-2:20

Next, he clarifies the difference between using <router-link> and a plain <a> tag for navigation. Using <router-link> enables Vue Router to handle navigation dynamically without a full page refresh, making transitions instant and smooth. Using a plain anchor tag causes a full page reload, which is not desired in SPA navigation. 2:10-3:30

Jeffrey then explains the purpose of <router-view>. This component dynamically renders the matched view component based on the current route. Removing <router-view> means no route components will display, so it’s essential for dynamic routing. Hardcoding a view component instead would show the same component for all routes, defeating the purpose. 3:50-5:20

He also touches on component naming conventions, specifically why some components have names starting with "The" (e.g., TheWelcome). This is a convention to indicate that the component is a one-off partial used only once in the entire project, helping future developers understand its intended usage. 6:10-7:10

Finally, Jeffrey discusses the flexibility of Vue single-file components (SFCs), highlighting that you can include template, script, and styles all in one file, but none are strictly required. For example, a simple presentational component might omit the script section entirely. He also reminds to always use <router-link> with the to attribute (not href) for internal navigation to avoid full page reloads. 7:40-9:00

Overall, this episode is about clearing up small confusions around aliases, routing, component naming, and Vue SFC structure to make your development smoother.