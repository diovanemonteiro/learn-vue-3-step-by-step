# From Mixins to Composables

### Let's talk about code re-use in this episode. We'll begin by reviewing a basic example using a traditional, mixin-based approach. And then, we'll convert it to the more recommended approach these days: composables.

Here is the full transcript for Episode 19, "From Mixins to Composables," of the "Learn Vue 3: Step by Step" series on Laracasts:

All right, welcome back. So let's do this. I'm going to grab my mind reading helmet here, put it on, Doc Brown style, and I will guess or predict that you're still not sold on the Composition API. And if that's the case, if that's you, you're right. So far in this series, I haven't shown you anything that really demonstrates the benefits. So far, it's mostly, well, here's another way to do the exact same thing. And in fact, you might even think to yourself, you know what? I like the Options API even more. It feels more structured than this kind of loose approach using the Composition API.

I like the Options API even more. It feels more structured than this kind of loose approach using the Composition API. So again, all of this is perfectly normal. We haven't really reviewed many benefits yet. So that's what I want to start doing or begin doing over the next few episodes. Let's begin by talking about code reuse. So here's my Home component. Actually, we don't even need this. Let's get rid of that. And then temporarily, I'm going to switch back to the Options API.

Let's get rid of that. And then temporarily, I'm going to switch back to the Options API. Okay, so imagine here, in response to something, we'll just use a button here. When you click on the button, we want to display some kind of flash message to the user. Okay, so I could say when you click on me, call a method flash, and we'll say it works. All right. So of course, I need to create a method here called flash that accepts a message. And for now, I'm just going to do an alert. Switch to the browser, give it a try, and of course, it works. Basic stuff at this point.

Switch to the browser, give it a try, and of course, it works. Basic stuff at this point. Okay. But now, I want to do the exact same thing from a different page, maybe the About page. So we'll do that here. And you know what? I don't think we even need this class here. So let's keep it super simple. Okay, so we'll say it works on the About page. But of course, if we give it a try, that's not going to work at all.

Okay, so we'll say it works on the About page. But of course, if we give it a try, that's not going to work at all. And the reason is obvious. I don't have access to this method. It was defined in a totally different component over here. Okay, so now, you think, well, I need to call flash, so let's go to the About page, and I'm going to paste in all of that code. And now, it'll work. Yep, About page, Home page, we're up and running. But yeah, clearly, you can see this is not ideal.

Yep, About page, Home page, we're up and running. But yeah, clearly, you can see this is not ideal. I don't want to copy and paste this every single time I want to show a flash message on a new page. And then further, if we change it, there's an opportunity for these things to become out of sync. So for example, maybe we decide to switch to a tool called Suite Alert. So I will pull that in through NPM, and then I will import it up here. I'll call it Swall. There we go.

I'll call it Swall. There we go. And then, it's as simple as replacing Alert with Suite Alert. Okay, so now, if we give it a try, we have our fancy new alert message, but yeah, way back on the Home page, that's still using the traditional alert. So now, things have become out of sync. And it's really easy to do that six months down the line, when you've forgotten that you copied this from one page to another. All right, so let's see how to fix that. So first, real quick, if you're not familiar with Suite Alert, you can always add a title,

All right, so let's see how to fix that. So first, real quick, if you're not familiar with Suite Alert, you can always add a title, you could add a message, and even a level, like success, or warning, or danger, or information. And that will determine what kind of icon is displayed. So let's stick with success. So come back, let's go to About, give it a try. And yeah, that looks pretty good. But yeah, again, we had that big problem where everything is out of sync now. Okay, so a more legacy or traditional way that we would solve this in Vue 2 applications, and actually on that note, it still works in Vue 3, it's just a little frowned upon

Okay, so a more legacy or traditional way that we would solve this in Vue 2 applications, and actually on that note, it still works in Vue 3, it's just a little frowned upon these days. Anyways, that technique is known as mixins. It's sort of like traits in PHP. So let's give it a try. I'm going to add a new directory called mixins. And you can name this anything you want. I'm going to go with Flash. Okay, so when we are creating mixins, one nice thing is the object here will be identical

I'm going to go with Flash. Okay, so when we are creating mixins, one nice thing is the object here will be identical to your Vue components. And whatever you have here will literally be mixed in with the component that pulls it in. So that means if I want a method, then I create one here. If I have a particular hook, then I would declare it here. And again, it all gets mixed up or merged into the single Vue component. Okay, so now you can see where I'm going with this. If I switch back, I could take, well, all of this and move it in here.

Okay, so now you can see where I'm going with this. If I switch back, I could take, well, all of this and move it in here. And we'll return this. All right, we have our mixin. So now if I want to use it back in the About page, so import Flash from, and we go into our mixins directory, and Flash. Now I can export an object, and I will add this new mixins property where I can provide an array of mixins that should be, again, mixed in with the current component. Okay, so now I once again have access to this Flash method because it was defined in the mixin here.

Okay, so now I once again have access to this Flash method because it was defined in the mixin here. So this should work exactly the way it did before. But now I can also pull it in from the Home Vue. So let's do this. So now I have a single place where we can define how a Flash message or overlay is presented to the user. And we don't have to worry about them becoming out of sync. I don't have to worry about copying and pasting implementations. This is definitely a step up.

I don't have to worry about copying and pasting implementations. This is definitely a step up. But now, like I said, even though this is still supported, it's not being deprecated anytime soon, it's somewhat frowned upon, mostly because now when you have all these mixins you're pulling in, the code base becomes a little less clear. It's not clear where this Flash message is defined. And again, we can figure it out here because we have 10 lines or so. But you can imagine a component that is 400 lines long, and then suddenly you're calling this method, and you don't immediately know where it comes from. And worse, if you have multiple mixins being pulled in, or you're using a library that's

this method, and you don't immediately know where it comes from. And worse, if you have multiple mixins being pulled in, or you're using a library that's pulling in mixins, again, it becomes confusing to determine where this is being defined. Or if you're changing state, maybe you're changing some kind of message property, but you don't see message defined here, so you find yourself having to look into all of your mixins to see where it's defined. And yeah, that's not dissimilar to traits in PHP. Now granted, a good IDE can help you with this. So in fact, I think phpStorm can figure out where this is defined. But yeah, you're not always going to be using that.

So in fact, I think phpStorm can figure out where this is defined. But yeah, you're not always going to be using that. And still, it's a potential concern. So a more recommended approach is to reach for something known as composables. And I'll show you how to do that. Let's create a new directory here called composables. And I'll add a new file here. And the common convention is to name it use, and then the thing it represents. So in our case, we are working with Flash messages, I will call it useFlash. And now I will export a function that has the same name as the file.

So in our case, we are working with Flash messages, I will call it useFlash. And now I will export a function that has the same name as the file. Again, we're following conventions here. Okay, so let's do it. I'm going to take everything we have here, and it looks like it's just a method called Flash, and I will define it like so. I'll paste that in, and then declare Flash as a function. And you do note when I pasted that in, it automatically pulls in the import as well. Okay, finally, I'm going to return whatever I want to expose to the outside world, or whatever I want to share.

Okay, finally, I'm going to return whatever I want to expose to the outside world, or whatever I want to share. In this case, it looks like I just want to share a method called Flash, or a function called Flash. Now what we have here is technically just a module. I'm calling it a composable. But if you think about it, we're not really leveraging the composition API, we're not managing any state. But nonetheless, we will get there. I'm trying to start with the simplest possible example.

But nonetheless, we will get there. I'm trying to start with the simplest possible example. So this is a very basic composable in quotes. Okay, so now let's use it. I'm going to go back to my home component. We're no longer using mixins, so I will replace this with useFlash from composables useFlash. Okay so now, in my setup method, and this is almost always where you will call your composables, I can trigger this method or function. And think about it, that function is going to return to me an object with a key of Flash. And that property is equal to a function that displays a suite alert.

And think about it, that function is going to return to me an object with a key of Flash. And that property is equal to a function that displays a suite alert. All right, let's use it. So I will pull that out, Flash. And now don't forget, when we create this setup method, whatever you've returned from it is exactly like what you would have defined in your data method. Whatever I return here is just like what I would have returned from the data method. Okay, so I will return Flash. Now I can use it in my template. Switch back to Chrome, we're on the home page, and it works.

Now I can use it in my template. Switch back to Chrome, we're on the home page, and it works. Very cool. So yeah, this is an alternative to using mixins. And I think you'll find this is the more recommended approach these days. And don't forget, we can even clean this up further by using script setup. When we do this, just like before, I can take the contents of my setup method and graduate it to the top level like this. And just to prove it to you, of course, it still works. But yeah, now to my eyes, this becomes much more appealing.

And just to prove it to you, of course, it still works. But yeah, now to my eyes, this becomes much more appealing. If I want to reuse code, I create a composable, I import it, and then I use it. Okay, so now in my About page, I'm going to do the same thing here. I'm going to paste it in. And now I have access to a Flash function within this page as well. Give it a try. It works here. And on the About page, it works as well. Okay, so now if I want to change the functionality, I can do so within a single place.

And on the About page, it works as well. Okay, so now if I want to change the functionality, I can do so within a single place. So for example, maybe we're going to change the API. Give us a title, give us a message, and give us a level. But I will set the level to a default of success. Okay, now we can tweak this. I can say test. And then on the About page, I will say hey. And then let's try out an icon of, I don't know, info. All right, let's give it a shot.

And then let's try out an icon of, I don't know, info. All right, let's give it a shot. There we go. Here's our information icon. Go to the other page. And now we have our success icon. Okay, so now you've learned two different very common approaches for basic code reuse, mixins and now composables. And in fact, we still have a good bit more to discuss. So let's keep digging into composables in the next episode.

You can also view the transcript with timestamps here: 0:00-11:12

Let me know if you want me to extract any specific part or code examples from this episode!

## Translation

Muito bem, bem-vindo de volta. Vamos lá. Vou pegar meu capacete de leitura de mentes aqui, colocá-lo no estilo Doc Brown, e vou adivinhar ou prever que você ainda não está convencido com a Composition API. E se esse for o caso, se esse é o seu sentimento, você está certo. Até agora nessa série, eu não te mostrei nada que realmente demonstre os benefícios. Até agora, é basicamente só: "aqui está outra forma de fazer a mesma coisa". E, de fato, você pode até pensar: "Sabe de uma coisa? Eu gosto ainda mais da Options API. Ela parece mais estruturada do que essa abordagem solta usando a Composition API."

Eu gosto ainda mais da Options API. Ela parece mais estruturada do que essa abordagem solta usando a Composition API. E tudo bem, isso é totalmente normal. A gente ainda não revisou muitos benefícios. E é isso que eu quero começar a fazer nos próximos episódios. Vamos começar falando sobre reutilização de código. Aqui está meu componente Home. Na verdade, nem precisamos disso. Vamos remover. E, temporariamente, vou voltar para a Options API.

Ok, imagine aqui que, em resposta a alguma ação – vamos usar um botão. Quando você clicar nesse botão, queremos exibir uma mensagem de notificação ao usuário. Então posso dizer: ao clicar, chame o método flash, e diremos “funciona!”. Claro, preciso criar um método flash que aceite uma mensagem. E, por enquanto, vou só usar um alert. Voltando ao navegador, testamos, e claro, funciona. Coisa básica por enquanto.

Mas agora, quero fazer exatamente a mesma coisa em outra página, talvez a página About. Vamos fazer isso aqui. E, na real, acho que nem precisamos dessa class. Vamos manter super simples. Ok, então vamos dizer: “funciona na página About”. Mas claro, se tentarmos, isso não vai funcionar.

E o motivo é óbvio: não tenho acesso a esse método. Ele foi definido em um componente totalmente diferente. Então, agora você pensa: “Preciso chamar flash”, então vamos à página About, e colamos todo aquele código. E agora vai funcionar. Sim, página About, página Home, tudo funcionando. Mas, claramente, dá pra ver que isso não é o ideal.

Não quero copiar e colar isso toda vez que quiser exibir uma mensagem em uma nova página. E, além disso, se eu alterar o método, há chance de as versões ficarem fora de sincronia. Por exemplo, talvez decidamos mudar para uma ferramenta chamada SweetAlert. Então instalo com NPM e importo lá em cima. Vou chamar de Swal.

E então é tão simples quanto substituir alert por Swal. Testamos e temos nossa nova mensagem bonita. Mas, veja só: lá na página Home ainda está usando o alert tradicional. Então as coisas ficaram fora de sincronia. E é muito fácil isso acontecer depois de 6 meses, quando você esqueceu que copiou esse código de uma página para outra.

Ok, como resolver isso? Primeiro, se você não conhece o SweetAlert, você pode adicionar um título, uma mensagem e até um nível, como success, warning, danger ou info. Isso define o ícone que será exibido. Vamos manter como success. Voltamos à página About, testamos – e sim, está bonito. Mas, de novo, o grande problema é que está tudo fora de sincronia.

Uma maneira mais tradicional que usávamos para resolver isso em aplicações Vue 2 – e na real, ainda funciona no Vue 3, embora seja um pouco desencorajada – é usar mixins. É como traits no PHP. Vamos tentar. Vou criar um diretório chamado mixins. E você pode nomear como quiser. Vou chamar de Flash.

Ao criar mixins, uma vantagem é que o objeto aqui será idêntico ao de um componente Vue. E o que você colocar aqui será literalmente mesclado com o componente que o importar. Então, se quero um método, crio aqui. Se tiver um hook, declaro aqui. Tudo será mesclado no componente. Então você já imagina onde quero chegar. Posso pegar tudo isso e mover para cá.

E então retornamos isso. Pronto, temos nosso mixin. Agora, se eu quiser usá-lo na página About, importo Flash do diretório mixins. Agora posso exportar um objeto e adicionar a propriedade mixins, que recebe um array com os mixins que devem ser incluídos neste componente.

Agora, mais uma vez, tenho acesso ao método flash, pois ele foi definido no mixin. Isso deve funcionar exatamente como antes. E agora posso usá-lo também na página Home. Com isso, tenho um lugar único onde defino como a mensagem é exibida para o usuário, e não preciso mais me preocupar com cópias ou versões divergentes. É um avanço.

Mas, como eu disse, embora ainda seja suportado, mixins são um pouco mal vistos hoje. Isso porque, quando você começa a importar muitos mixins, o código fica menos claro. Não é evidente onde o método flash está definido. E aqui conseguimos ver porque o componente é pequeno. Mas imagine um componente com 400 linhas, e você chama um método sem saber de onde ele veio. E pior, se tiver múltiplos mixins sendo importados, ou bibliotecas usando mixins, fica confuso saber onde tudo está definido.

Ou então, se você está mudando um state, como uma propriedade message, mas ela não está visível ali, você vai ter que procurar em todos os mixins. Isso lembra bastante os traits do PHP. Um bom IDE pode ajudar. O PhpStorm, por exemplo, consegue apontar de onde vem. Mas nem sempre você estará usando ele. E ainda assim, é um problema potencial.

__Então a abordagem mais recomendada hoje é usar algo chamado composables__. E eu vou te mostrar como fazer isso. Vamos criar um novo diretório chamado composables. E vou adicionar um novo arquivo. A convenção comum é nomear como use + o nome do recurso. Como estamos lidando com mensagens flash, vou chamar de useFlash. E agora exportamos uma função com o mesmo nome.

Vamos lá. Vou pegar tudo que temos aqui – basicamente um método flash – e vou defini-lo na função. Colei o conteúdo e ele até já importou o SweetAlert. E por fim, retorno o que quero expor ao mundo externo. No caso, é só a função flash.

O que temos aqui é, tecnicamente, apenas um módulo. Estou chamando de composable. Mas, se pensar bem, ainda não estamos usando de fato a Composition API, nem lidando com estado. Mas vamos chegar lá. Estou começando com o exemplo mais simples possível.

Esse é um composable bem básico, entre aspas. Agora vamos usá-lo. Volto para o componente Home. Não estamos mais usando mixins, então importo useFlash de composables/useFlash.

Agora, dentro do método setup, que é quase sempre onde você chama seus composables, eu posso usar essa função. Ela me retorna um objeto com a chave flash, que é uma função que exibe o SweetAlert.

Vamos usar. Extraí flash. __E não se esqueça: tudo o que você retornar do setup é como se tivesse definido em data__. Então retorno flash. Agora posso usá-lo no template. Volto ao Chrome, estamos na página Home – e funciona.

Muito legal. Essa é uma alternativa ao uso de mixins. E essa abordagem é mais recomendada hoje em dia. E mais: podemos refinar isso usando script setup. Quando usamos, pegamos o conteúdo do setup e colocamos no topo, diretamente. E para provar: claro, ainda funciona. Mas agora, visualmente, está mais agradável.

__Se quero reutilizar código, crio um composable, importo, e uso__. Agora, na página About, vou fazer o mesmo. Colei o código. Agora tenho acesso ao método flash nessa página também. Testo – funciona aqui. E na página Home – também funciona.

Agora, se eu quiser mudar a funcionalidade, posso fazer isso num único lugar. Por exemplo, posso alterar a API para receber um título, uma mensagem e um nível. Mas vou definir um nível padrão como success. Agora ajustamos: posso dizer “teste”. Na página About, digo “hey”. E tento um ícone, digamos, info.

Vamos testar. Pronto, aqui está nosso ícone de informação. Vamos para a outra página...

## Summary

In Episode 19, __Jeffrey explains the practical benefits of the Composition API by focusing on code reuse__. He starts by showing a common problem: duplicating a flash message method across multiple components using the Options API, which leads to maintenance issues and code getting out of sync.

He then revisits the older Vue 2 solution of mixins, which allows sharing methods and hooks by mixing in an object into components. While mixins solve the duplication problem, they can make the codebase harder to understand because it becomes unclear where methods or state come from, especially with multiple mixins.

Jeffrey introduces composables as the modern, recommended alternative. A composable is a simple function (usually named with a use prefix) that encapsulates reusable logic and returns the pieces you want to expose. This approach is clearer and more explicit than mixins. He demonstrates creating a useFlash composable that provides a flash message function, which can be imported and used in any component's setup function. This keeps the code DRY and easier to maintain.

He also shows how composables fit naturally with the <script setup> syntax, making the code even cleaner and more appealing.

Overall, the key takeaway is that composables provide a more transparent and maintainable way to share reusable logic across components compared to mixins, aligning well with Vue 3's Composition API style.