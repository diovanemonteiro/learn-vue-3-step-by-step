# Component Props

### If we want our Vue components to be as flexible as possible, we should figure out a way to pass in data from the outside. This way, each "instance" of a component can be configurable. Props allow for this!

Here is the full transcript for Episode 6, "Component Props," from the "Learn Vue 3: Step by Step" series on Laracasts:

Okay, so, if we want our Vue components to be as flexible as possible, we need to figure out a way to pass in data from the outside. And that way, each instance of the component could have its own set of props. Let's figure out how in this episode. But before we dig in, a quick bit of housekeeping. In the last episode, we set up our first Vue component, which is great. But if we come back here, I also noted that what you see here also is a Vue component. So could we extract that to its own file? The answer, of course, is yes. So let's do that now.

The answer, of course, is yes. So let's do that now. I'll create a new file. And this will be our app component. And I'll paste that in. And instead of saving it to a variable, we will export it. Okay, but now don't forget, we need to import app button here. Import app button. And I'll add the extension. Great.

And I'll add the extension. Great. So now if I switch back to index.html, we can get rid of all of this and replace it with an import of our app. Just like that. And again, don't forget to include the extension. So now we will update this. And this should work just like it did before. We switch to the browser. And yes, we see our button.

We switch to the browser. And yes, we see our button. So it's working. Quite a bit of work just for a single button. But of course, we are setting up the framework for how you will structure your applications. And yeah, what we're doing here, this is all starting to look quite a bit more real life. What you will see in the real world when browsing a Vue-based application. All right. Housekeeping complete. Let's move on to props.

Housekeeping complete. Let's move on to props. So yeah, right now we just have a standard button that is gray. But in real life, as you know, you'll have different styles of buttons. You might have your primary button. You might have a secondary one. You might have a muted button. And it would be cool if we could specify that when we instantiate it, so to speak. So for example, maybe I could have a primary button. And that would be, say, blue.

So for example, maybe I could have a primary button. And that would be, say, blue. All right. Let's see how we can do that. The first step is to visit our component. And we can declare which props can be passed in by using the props object. We call that prop type. And it should be a string. So this is where we specify the data type. Because remember, if you want, we could accept an object or an array or a Boolean.

So this is where we specify the data type. Because remember, if you want, we could accept an object or an array or a Boolean. In this case, though, what we want is a string. OK. So let's leave it like this. Switch back to the browser. Give it a refresh. And now we're going to leverage Vue DevTools. Have a look. Here's our button.

Have a look. Here's our button. And now we can see it does accept a type prop. And currently, it's set to primary. Perfect. But what about the situations where, well, how about the primary type should be the default type? OK. That means if we don't pass one in at all, it should still be set to primary. But right now, it's undefined. OK.

But right now, it's undefined. OK. If we switch back, I can say just like this. Type will be now an object where the type is string. Don't get confused that we have two types. This is the name of the prop. And this is the type of the prop. So it's just a coincidence that we're doubling up there. But they are different things. OK.

But they are different things. OK. So the type is string. And the default value for it is primary. That's how we can handle this. So if I come back and refresh, now the type is primary. But if I switch back, and this time we set a type of, how about secondary? Well, it should override the default. And it does, as you see there. Cool.

And it does, as you see there. Cool. So now our component is accepting data from the outside world. That's how I think of it. Now, let's use it. And it's very simple. And I'll show you a little trick. When you're setting class bindings, you can use a string, you could use an array, or you could use an object. Let's take the object approach.

could use an object. Let's take the object approach. So I will cut all of this out, replace it with an object. And now the key of the object will be the class names. So I could paste all of those in there. And then the value would be a Boolean. And if that Boolean is true, we add the classes to the element. If the Boolean is false, we do not. So for example, if I set true here, have a look. If I come back and refresh, I should still see my gray button.

So for example, if I set true here, have a look. If I come back and refresh, I should still see my gray button. But if we instead change it to false, that means do not apply these classes, as you see there. Cool. So what we could do is set a base set of classes. And let's hide the sidebar, which would be a border, rounded, some padding. But then the colors, those will be unique to the style or the type, like this. Apply a gray background if the type is, how about, muted. All right, let's do a couple more.

Apply a gray background if the type is, how about, muted. All right, let's do a couple more. We'll do primary, secondary, and muted. So we'll do primary, secondary. For primary, we'll say maybe if it's blue, something like that. Secondary, you know, whatever you want. Purple, maybe? All right, let's have a look. And yeah, it's pastel purple. Maybe we're building a My Little Pony site.

And yeah, it's pastel purple. Maybe we're building a My Little Pony site. But you get the idea. We can now configure the style of the button based upon an incoming prop value. So let's try out all variations. We have secondary. We have muted, which should be the default gray. And we have primary, which is, again, a My Little Pony shade of blue. Or, of course, if we don't pass in any type, it will still default to blue. Okay, so now if you want, you could set the state of the button from the outside world.

Or, of course, if we don't pass in any type, it will still default to blue. Okay, so now if you want, you could set the state of the button from the outside world. Right now, we had processing as a simple data prop. But in real life, you might pass that in like this. I will now make processing a Boolean. So we'll say type of Boolean, default of false. By default, it's not processing. But what I do want you to notice is that in your template, nothing changes here. If you need to access a prop, reference the name. Or if you need to instead access a data property, again, just reference the name.

If you need to access a prop, reference the name. Or if you need to instead access a data property, again, just reference the name. It's the exact same system. So let's do this. Let's add a class of isLoading if the button is currently processing. Okay, so now we'll switch back to our template here. And I will set processing to true. And again, you can imagine binding this to the result of some kind of Ajax call. Okay, so if I switch back and give this a refresh, we should see a class of isLoading. And we do.

Okay, so if I switch back and give this a refresh, we should see a class of isLoading. And we do. But if I set this to false, then we will not see that class. And just to drive this home, let's see if we can quickly find a CSS loading spinner. So I will Google that. How about this one from Steven Wagner? Okay, yeah, something like that. So let's grab all of that. And I'll just put it in line here. And it looks like we need a class of, well, let's change this to isLoading.

And I'll just put it in line here. And it looks like we need a class of, well, let's change this to isLoading. Okay, so now let's set it in a state of processing. Cross our fingers and give it a refresh. And there we go. Okay, cool. So now the only remaining step is to hide the text when it's processing. So I could say up here isLoading. Let's just set the color to transparent. That would be one way to deal with it.

Let's just set the color to transparent. That would be one way to deal with it. Give it a refresh. And there we go. Okay, so now if I switch back, this blue is killing me. Let's turn it up to, how about 600 to 700? Okay, it works. It's not the prettiest button in the world, but yeah, it works. We have a loading spinner to provide some feedback for the user. We disallow clicking it more than once, which means you can't spam that button to send a bunch

We have a loading spinner to provide some feedback for the user. We disallow clicking it more than once, which means you can't spam that button to send a bunch of AJAX requests to the server, which, trust me, people will try to do. That's good. And we allow for this through the use of props. Very cool.

You can also review the transcript directly at the start of the episode here: 0:00-8:22

Let me know if you want me to extract specific code examples or explain any part!


## Translation

Aqui está a transcrição completa do Episódio 6, "Component Props", da série "Learn Vue 3: Step by Step" da Laracasts:

Beleza, então, se quisermos que nossos componentes Vue sejam os mais flexíveis possível, precisamos descobrir uma forma de passar dados de fora para dentro. E assim, cada instância do componente poderia ter seu próprio conjunto de props. Vamos descobrir como fazer isso neste episódio.

Mas antes de começarmos, um breve recado. No episódio anterior, criamos nosso primeiro componente Vue, o que é ótimo. Mas se voltarmos aqui, também notei que o que você vê aqui também é um componente Vue. Então, será que poderíamos extrair isso para um arquivo próprio? A resposta, é claro, é sim. Então, vamos fazer isso agora.

A resposta, é claro, é sim. Então, vamos fazer isso agora. Vou criar um novo arquivo. E este será o nosso componente App. Vou colar o conteúdo lá. E em vez de salvar isso numa variável, vamos exportá-lo. Ok, mas agora não se esqueça, precisamos importar o AppButton aqui. Importar AppButton. E vou adicionar a extensão. Ótimo.

E vou adicionar a extensão. Ótimo. Agora, se eu voltar para o index.html, podemos remover todo aquele conteúdo e substituí-lo pela importação do nosso App. Assim mesmo. E novamente, não se esqueça de incluir a extensão. Agora vamos atualizar isso. E isso deve funcionar como antes. Mudamos para o navegador. E sim, vemos nosso botão.

Mudamos para o navegador. E sim, vemos nosso botão. Então, está funcionando. Bastante trabalho só para um único botão. Mas, claro, estamos configurando a estrutura de como você organizará suas aplicações. E sim, o que estamos fazendo aqui começa a se parecer bastante com o mundo real. Como as coisas funcionam em aplicações reais feitas com Vue. Certo. Recados concluídos. Vamos em frente para falar sobre props.

Recados concluídos. Vamos em frente para falar sobre props. Agora, temos apenas um botão padrão que é cinza. Mas na vida real, como você sabe, teremos diferentes estilos de botões. Pode haver o botão primário, o botão secundário, o botão desativado (muted). E seria legal se pudéssemos especificar isso ao instanciá-lo, por assim dizer.

Por exemplo, talvez eu queira um botão primário. E esse botão poderia ser azul.

Certo. Vamos ver como fazer isso. O primeiro passo é visitar nosso componente. E podemos declarar quais props podem ser passadas usando o objeto props. Chamamos isso de tipo da prop (prop type). E ela deve ser uma string. Aqui é onde especificamos o tipo de dado. Porque lembre-se, se quisermos, poderíamos aceitar um objeto, um array ou um booleano.

Aqui é onde especificamos o tipo de dado. Porque lembre-se, se quisermos, poderíamos aceitar um objeto, um array ou um booleano. Mas neste caso, o que queremos é uma string. Ok. Vamos deixar assim. Voltar ao navegador. Atualizar a página. Agora vamos usar o Vue DevTools. Veja só. Aqui está nosso botão.

Veja só. Aqui está nosso botão. E agora podemos ver que ele aceita uma prop chamada type. E atualmente está definida como primary. Perfeito. Mas e se quisermos que o tipo primary seja o valor padrão? Ok. Isso significa que, se não passarmos nenhum valor, ainda assim ele deve ser primary. Mas, neste momento, está como undefined. Ok.

Mas, neste momento, está como undefined. Ok. Se voltarmos, posso dizer o seguinte: type será agora um objeto onde type é String. Não se confunda com os dois “type” — esse é o nome da prop, e esse é o tipo da prop. É só coincidência estarem repetidos. Mas são coisas diferentes. Ok.

Mas são coisas diferentes. Ok. Então o tipo é String. E o valor padrão será primary. É assim que lidamos com isso. Se eu voltar e atualizar, agora o tipo será primary. Mas se eu voltar e, desta vez, definirmos o tipo como secondary, ele deve sobrescrever o padrão. E faz isso, como você pode ver. Legal.

E faz isso, como você pode ver. Legal. Agora nosso componente está aceitando dados do “mundo externo”. É assim que penso nisso. Agora, vamos usar isso. E é bem simples. Vou mostrar uma dica. Quando você estiver usando bindings de classe, pode usar uma string, um array ou um objeto. Vamos usar o modo com objeto.

Vamos usar o modo com objeto. Vou cortar todo o conteúdo atual e substituí-lo por um objeto. Agora a chave do objeto será o nome da classe. Então posso colar todos esses nomes de classe ali. E o valor será um booleano. Se esse booleano for true, as classes serão aplicadas ao elemento. Se for false, não serão.

Por exemplo, se eu colocar true aqui, veja só. Se eu voltar e atualizar, ainda devo ver meu botão cinza.

Por exemplo, se eu colocar true aqui, veja só. Se eu voltar e atualizar, ainda devo ver meu botão cinza. Mas se mudarmos para false, isso significa que essas classes não serão aplicadas, como você vê. Legal. Então, o que podemos fazer é definir um conjunto base de classes. E vamos esconder a sidebar. Seriam coisas como borda, cantos arredondados, algum padding. Mas as cores, essas serão únicas por tipo, como assim: aplicar fundo cinza se o tipo for muted. Beleza, vamos fazer mais alguns.

Aplicar fundo cinza se o tipo for muted. Beleza, vamos fazer mais alguns. Vamos fazer primary, secondary e muted. Então faremos primary e secondary. Para primary, diremos talvez azul, algo assim. Secondary, qualquer cor que você quiser. Roxo, talvez? Beleza, vamos ver. E sim, é um roxo pastel. Talvez estejamos construindo um site do My Little Pony.

E sim, é um roxo pastel. Talvez estejamos construindo um site do My Little Pony. Mas você entendeu a ideia. Agora podemos configurar o estilo do botão com base no valor recebido pela prop. Vamos testar todas as variações. Temos secondary, muted (que deve ser cinza por padrão) e primary, que novamente é um azul estilo My Little Pony. E claro, se não passarmos nenhum tipo, ainda será azul por padrão.

Ok, agora, se quiser, você pode definir o estado do botão a partir do mundo externo.

Ok, agora, se quiser, você pode definir o estado do botão a partir do mundo externo. Agora mesmo, tínhamos processing como uma data prop simples. Mas na prática, você pode passar isso como uma prop, assim. Agora farei de processing um booleano. Então diremos que o tipo é Boolean, com valor padrão false. Por padrão, ele não estará processando. Mas quero que você perceba que, no seu template, nada muda aqui. Se precisar acessar uma prop, basta referenciar o nome dela. Se quiser acessar uma data property, mesma coisa: apenas referencie o nome.

Se quiser acessar uma prop, basta referenciar o nome dela. Se quiser acessar uma data property, mesma coisa: apenas referencie o nome. É o mesmo sistema. Vamos fazer isso: adicionar uma classe isLoading se o botão estiver processando. Beleza, agora voltamos ao template. E vamos definir processing como true. E você pode imaginar que isso seria o resultado de uma chamada AJAX, por exemplo.

Se eu voltar e atualizar, deveremos ver a classe isLoading. E vemos.

Se eu voltar e atualizar, deveremos ver a classe isLoading. E vemos. Mas se eu definir isso como false, então não veremos essa classe. E só para reforçar, vamos procurar rapidamente um spinner de carregamento em CSS. Vou pesquisar no Google. Que tal esse do Steven Wagner? Ok, sim, algo assim. Vamos copiar tudo. E colocarei aqui direto no HTML. Parece que precisamos de uma classe chamada, bem, vamos mudar isso para isLoading.

E colocarei aqui direto no HTML. Parece que precisamos de uma classe chamada, bem, vamos mudar isso para isLoading. Agora vamos colocar o botão no estado de processamento. Cruzar os dedos e atualizar. E lá está. Legal. Agora, o único passo que falta é esconder o texto enquanto estiver carregando. Podemos dizer aqui em cima: se isLoading, então vamos definir a cor como transparent. Seria uma forma de lidar com isso.

Vamos definir a cor como transparent. Seria uma forma de lidar com isso. Atualizar. E lá está. Agora, se eu voltar, esse azul está me matando. Vamos mudar de 600 para 700? Ok, funciona. Não é o botão mais bonito do mundo, mas funciona. Temos um spinner de carregamento para dar feedback ao usuário. Impedimos que ele clique várias vezes, o que evita que a pessoa envie várias requisições AJAX para o servidor, o que, acredite, as pessoas tentam fazer. Isso é ótimo. E conseguimos isso através do uso de props. Muito legal.

## Summary

In Episode 6, "Component Props," Jeffrey explains how to make Vue components flexible by passing data from the outside through props. He starts by organizing components into separate files, which is a common real-world practice.

The core concept is declaring props in a component using the props option, specifying the expected data type (like string or Boolean) and optionally setting default values. This allows each component instance to receive different data, such as button types like "primary," "secondary," or "muted," which then control the styling dynamically.

Jeffrey demonstrates using an object syntax for class bindings to conditionally apply CSS classes based on prop values. For example, the button's background color changes depending on the type prop.

He also shows how to handle Boolean props (like a processing state) to add classes such as isLoading for showing a loading spinner and disabling repeated clicks. The template accesses props just like data properties, making the component reactive to external state.

Overall, this episode teaches how to pass and use props to customize component behavior and appearance, enabling reusable and configurable Vue components.