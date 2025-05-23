# A Deeper Look at V-Model

### We reviewed the basics of the `v-model`  directive at the beginning of the series, but I think it's time that we take a deeper look. What exactly happens when we apply `v-model`  to an input? And can we also use it on custom Vue components?

Here's the full transcript for Episode 12, "A Deeper Look at V-Model," from the "Learn Vue 3: Step 
by Step" series on Laracasts:

Okay, before we continue, I think we need to take a step back and have another look at the vmodel directive. At the beginning of the series, we learned the basics, and for example, we know that we can apply it to a form input, and then magically it keeps everything in sync. But what exactly happens when we apply it? It's really important. Let's have a look. Now here's index.html, but just for a minute, let's bring it back to a fresh boilerplate. So get rid of the text color, and then within here, I will add an input, where we will use vmodel, and how about name?

So get rid of the text color, and then within here, I will add an input, where we will use vmodel, and how about name? Okay, let's declare it. Return name, like so. Okay, let's view this in the browser. So I give it a refresh, and if I bring up Vue DevTools, right now, of course, name is an empty string, but if I were to change it to Joe, of course, we then see that the name data property is updated as well. And the same, of course, works in reverse. So if we change this to Jane, then Vue picks up on the change, and it re-renders the value

And the same, of course, works in reverse. So if we change this to Jane, then Vue picks up on the change, and it re-renders the value of the input. Okay, so if we were to take a step back and think, what exactly is vmodel doing? Well, at the very least, at some point, it is setting the value of the input. So we know, if I were to remove this, at some point, we are setting the value equal to name. Alright, so let's just play around with this for a minute. If I give it a refresh, and bring back Vue DevTools, let's set the name to Jane again, and it works. We set the value.

and it works. We set the value. But because we removed vmodel, it's not going to work the other way around. So if I change this to Jeffrey, notice at no point does the underlying name property get updated. Okay, so it sounds like that's the other piece of the puzzle. If we were to manually reproduce what vmodel does, we would set the value of the input, and then we would listen for when you type into the input, using the input event, and we would then update the name to be equal to the input's current value. Alright, let's give that one a shot.

we would then update the name to be equal to the input's current value. Alright, let's give that one a shot. So once again, I set the name from this end. That works. But if I update it to, how about, my own name? Aha! It worked! So we can see that vmodel is basically doing two things. First, it binds the value, and second, it listens for when the value changes. And as it turns out, what you see here is basically the long form of vmodel.

First, it binds the value, and second, it listens for when the value changes. And as it turns out, what you see here is basically the long form of vmodel. Vmodel name. It's the same thing. Okay, so now that you understand this important piece of the puzzle, let's bring back our existing app, like so. So we come back, give it a refresh, there's our app. And now, yeah, let's apply this knowledge. So here we set up our assignment tags, and you'll remember in the last episode, we ran into this awkward situation where we need to pass the current tag to the assignment

So here we set up our assignment tags, and you'll remember in the last episode, we ran into this awkward situation where we need to pass the current tag to the assignment tags component, but then we also need to listen for when that assignment tags component changes the current tag by emitting this change event. And when it does, we also need to update the current tag here as well. So you can see what I'm basically doing is I'm desperately trying to keep everything in sync. I'm trying to pass the current tag to this component, but then if that component changes what the current tag should be, we need to listen for that and then update it on this end as well.

what the current tag should be, we need to listen for that and then update it on this end as well. Okay, well, if you take a look at this, though, it's kind of like vModel, isn't it? We're passing a value, we're binding a value, and then we're listening for some kind of input event so that we can update the data property on this end. Okay, so yeah, it does seem like it would be neat if I could use vModel on things other than basic form inputs. And as it turns out, we actually can. So let me show you how this works. I want to set vModel to the current tag, so I'm going to pass it in like this.

So let me show you how this works. I want to set vModel to the current tag, so I'm going to pass it in like this. That would then allow me to get rid of this here. And if I switch to assignment tags, let's remove that as a prop. And instead, I will replace it with this model value prop name. This is the default prop name when we are using vModel on a custom component. Okay, so now model value should be equal to whatever the current tag is, which means I can replace that current tag prop with model value. All right, but that's only half of the puzzle. We are now passing in the value.

All right, but that's only half of the puzzle. We are now passing in the value. The next step, as we discussed, is to listen for when that value changes and then emit an event. And we've done that partially. We emit this custom event called change. I'm going to change this to update colon, and then the property that we're updating, in this case, model value. And keep in mind, this event name is not arbitrary. It needs to be this exact shape in order for things to work.

And keep in mind, this event name is not arbitrary. It needs to be this exact shape in order for things to work. Okay, so now I can remove the change event, and with any luck, this should all just work. Let's have a look. Return to the browser. Let's open up Vue DevTools. Here's our assignment list. And yeah, right now the current tag defaults to all. But if we did everything correctly, when I change it to math or science, notice that it updates.

But if we did everything correctly, when I change it to math or science, notice that it updates. Okay, let's see the other end. So if I open up assignment tags, notice model value is science. We change it, and that part is working as well. So this is actually a relatively easy way that we can use vModel on things other than basic form inputs. So just to reiterate and make this crystal clear, if you want to use vModel on custom components, then your component needs to offer a model value prop, and this will accept whatever the value of current tag is in this case.

components, then your component needs to offer a model value prop, and this will accept whatever the value of current tag is in this case. So we can then use it, we can bind it, however is necessary for the component. That's the first piece. The second piece is then to notify the parent when that value changes. And we do that by emitting an event, update, colon, and then the name of the prop, which is model value. Okay, so the last little piece of the puzzle is if you don't like using model value, it's kind of vague and arbitrary, you can be explicit about what it should be called. So if you want it to be the exact same thing, you can do this shape here, vModel current

kind of vague and arbitrary, you can be explicit about what it should be called. So if you want it to be the exact same thing, you can do this shape here, vModel current tag. So that's saying, okay, I don't want it to be model value, I want it to be current tag. So now if we add that, we can update the prop like so, and now we can update that here and here. Yeah, and now we effectively have what we started with, but now we don't have to do that awkward thing where we listen for a change event and then manually update it on the parent. And don't get me wrong, we're still effectively doing that behind the scenes, but we're able to mask it behind the very useful vModel directive.

And don't get me wrong, we're still effectively doing that behind the scenes, but we're able to mask it behind the very useful vModel directive. Okay, so I'll let you take one last look at this component. We've now extracted an assignment tags component. Now of course, the parent still needs to know what tag are we working with, what is the current tag. So we use vModel to track that. Then assignment tags can be responsible for all the markup and basic behavior for how to display and update those tags. And like I said, down the line, if we want to add an option to create a new tag, that

to display and update those tags. And like I said, down the line, if we want to add an option to create a new tag, that can all be done right here within this component that is specifically tailored to working with tags. And the benefit is, if I now switch back to assignment list, we can see that everything is fairly clean once again. I don't have a bunch of logic related to working with tags. I have a single place to track what the current tag is, and then we can filter against it. And yeah, I think this ends up being pretty clean. All right, let's move on to the next episode.

And yeah, I think this ends up being pretty clean. All right, let's move on to the next episode.

You can also view the transcript with timestamps here: 0:00-7:53

Let me know if you want me to extract or explain any specific part!

## Translation

Aqui está a transcrição completa do Episódio 12, "Um Olhar Mais Profundo sobre o V-Model", da série "Aprenda Vue 3: Passo a Passo", do Laracasts:

Certo, antes de continuarmos, acho que precisamos dar um passo atrás e olhar novamente para a diretiva `v-model`. No início da série, aprendemos o básico e, por exemplo, sabemos que podemos aplicá-la a um campo de formulário, e então, magicamente, ela mantém tudo sincronizado. Mas o que exatamente acontece quando a aplicamos? Isso é muito importante. Vamos dar uma olhada.

Aqui está o arquivo `index.html`, mas por um momento, vamos voltar a um boilerplate limpo. Então, vou remover a cor do texto e, aqui dentro, adicionarei um campo de input, onde usaremos `v-model`, e que tal usarmos o nome?

Então, removo a cor do texto, e aqui dentro adiciono um campo de input com v-model, e vamos usar o nome? Certo, vamos declará-lo. Retornamos name, assim. Ok, vamos visualizar isso no navegador. Então, dou um refresh e, se eu abrir o Vue DevTools, agora, claro, name é uma string vazia. Mas se eu mudar para "Joe", é claro que vemos que a propriedade name nos dados também é atualizada. E o mesmo, claro, funciona ao contrário. Se mudarmos para "Jane", o Vue percebe a alteração e renderiza novamente o valor do input.

E o mesmo funciona ao contrário. Se mudarmos para "Jane", o Vue detecta a alteração e re-renderiza o valor do input. Ok, então, se voltarmos um passo e pensarmos: o que exatamente o `v-model` está fazendo? Bem, no mínimo, em algum momento, ele está atribuindo um valor ao input. Sabemos que, se eu remover isso, em algum momento estamos atribuindo value = name.

Certo, vamos brincar com isso por um minuto. Dou um refresh, abro o Vue DevTools, defino name como "Jane" de novo, e funciona. Definimos o valor. Mas como removemos o v-model, não funcionará no sentido inverso. Se eu mudar para "Jeffrey", repare que em nenhum momento a propriedade name é atualizada. Ok, então parece que essa é a outra parte do quebra-cabeça. Se fôssemos reproduzir manualmente o que v-model faz, definiríamos o valor do input e, em seguida, ouviríamos quando alguém digita, usando o evento input, e atualizaríamos o name para ser igual ao valor atual do input.

Vamos tentar isso. Novamente, defino o name daqui. Isso funciona. Mas se eu atualizar para, digamos, meu próprio nome? Aha! Funcionou! __Então podemos ver que v-model basicamente faz duas coisas: primeiro, vincula o valor; segundo, escuta quando o valor muda.__ E, ao que parece, o que você está vendo aqui é basicamente a forma "longa" do v-model.

__Primeiro ele vincula o valor, depois escuta quando o valor muda__. E, como resultado, o que vemos aqui é basicamente a forma extensa do v-model: v-model="name". É a mesma coisa. Agora que você entende essa parte importante do quebra-cabeça, vamos voltar ao nosso app original. Então voltamos, damos um refresh — aqui está nosso app. E agora, sim, vamos aplicar esse conhecimento.

Aqui configuramos nossas tags de atribuição, e você deve se lembrar que, no último episódio, enfrentamos uma situação estranha onde precisávamos passar a tag atual para o componente de tags, mas também escutar quando esse componente altera a tag atual ao emitir um evento de mudança. E quando isso acontece, também precisamos atualizar a tag atual aqui. Então, basicamente, estou tentando manter tudo sincronizado: passando a tag atual para o componente, e então, se o componente a altera, ouvimos isso e atualizamos aqui também.

__Se observarmos bem, isso é meio que o que v-model faz, não é? Passamos um valor, vinculamos um valor, e então ouvimos algum tipo de evento para atualizar a propriedade de dados do outro lado. Então sim, parece que seria ótimo se eu pudesse usar v-model em coisas além de inputs de formulários. E acontece que podemos, sim__. Deixe-me mostrar como isso funciona. Quero definir v-model para a tag atual, então vou passá-la assim:

```html
<assignment-tags v-model="currentTag" />
```

Isso me permite remover isso aqui. E se eu mudar para o componente AssignmentTags, vamos remover isso como uma prop. E em vez disso, substituirei por modelValue. Esse é o nome padrão da prop quando usamos v-model em um componente personalizado.

Agora, modelValue deve ser igual à tag atual, o que significa que posso substituir a prop currentTag por modelValue. Certo, mas isso é só metade do processo. Agora estamos passando o valor. O próximo passo, como discutido, é escutar quando esse valor muda e emitir um evento. Já fizemos isso parcialmente. Emitimos um evento chamado change. Mas agora vou mudar para update:modelValue.

Lembre-se: esse nome de evento não é arbitrário. Ele precisa ser exatamente nesse formato para que funcione com v-model. Agora posso remover o evento change, e com sorte, tudo deve funcionar. Vamos ver. Voltando ao navegador, abrimos o Vue DevTools. Aqui está a lista de atribuições. E sim, agora a tag atual é "all". Mas se fizermos tudo corretamente, ao mudar para "math" ou "science", repare que ela é atualizada.

Agora vamos olhar do outro lado. Se eu abrir o componente AssignmentTags, repare que modelValue é "science". Mudamos e essa parte também está funcionando. _Então, essa é uma maneira relativamente simples de usar v-model em coisas além de inputs básicos._

Só para reforçar e deixar isso bem claro: se você quiser usar v-model em componentes personalizados, então seu componente precisa ter uma prop chamada modelValue, que aceitará o valor, como neste caso, a currentTag.

Depois, podemos usá-la e vinculá-la da forma necessária dentro do componente. Essa é a primeira parte. A segunda parte é notificar o componente pai quando o valor mudar. E fazemos isso emitindo um evento update:[nome-da-prop], que neste caso é modelValue.

A última parte do quebra-cabeça: se você não gosta de usar modelValue, pois é meio genérico, pode ser mais explícito quanto ao nome que quer usar. Por exemplo:

```html
<assignment-tags v-model:currentTag="currentTag" />
```

Isso diz: ok, não quero que seja modelValue, quero que seja currentTag. Então agora, atualizamos a prop com esse nome, aqui e aqui. E agora temos exatamente o que tínhamos antes, mas sem aquele jeito estranho de escutar eventos e atualizar manualmente no componente pai. E não me entenda mal — ainda estamos efetivamente fazendo isso por trás dos panos — mas conseguimos esconder isso por trás da diretiva super útil v-model.

Então, vou deixar você dar uma última olhada nesse componente. Agora extraímos um componente AssignmentTags. Claro, o componente pai ainda precisa saber qual tag estamos usando, qual é a tag atual. Então usamos v-model para acompanhar isso. O AssignmentTags pode ser responsável por toda a marcação e comportamento básico de como exibir e atualizar essas tags.

E como eu disse, mais adiante, se quisermos adicionar uma opção para criar uma nova tag, isso pode ser feito aqui mesmo, dentro desse componente, que é especificamente voltado para trabalhar com tags. E o benefício é que, se eu voltar para o AssignmentList, vemos que tudo está limpo de novo. Não tenho um monte de lógica relacionada a tags aqui. Tenho um único local onde acompanho qual é a tag atual, e então filtramos com base nela.

E sim, acho que isso ficou bem limpo. Certo, vamos para o próximo episódio.