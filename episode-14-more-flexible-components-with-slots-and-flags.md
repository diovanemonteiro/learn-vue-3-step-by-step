# More Flexible Components With Slots and Flags

### There are many ways to allow for more flexible and configurable components. Let's begin with two simple and obvious techniques: slots and flags.

Here is the full transcript for Episode 14, "More Flexible Components With Slots and Flags," from the "Learn Vue 3: Step by Step" series on Laracasts:

Alright, next up we should talk about component configurability or component flexibility, something like that, fill in the blank. It's really cool that we can reuse components, but there will absolutely be cases where we need to tweak them or modify them in some way. So let's figure out what we can do there. To begin, well, let me show you something. If I boot up our server using npx serve, and we open this in the browser, but notice I don't see any assignments here like we did before. And that's because, well look, we haven't booted up that fake API server. So I'd have to open a new tab and say npx json server on port 3001.

And that's because, well look, we haven't booted up that fake API server. So I'd have to open a new tab and say npx json server on port 3001. And now I can switch back and refresh the page. And you know what, that's a little annoying. So usually my rule is when I have to run multiple commands to run my tests or start my server, I will always put those within a npm script. Here's how. Let's go into package.json and we'll add a new script section. Let's create a new script called start. And I want it to run these two commands, npx serve and also npx json server.

Let's create a new script called start. And I want it to run these two commands, npx serve and also npx json server. Okay, so I want our serve command and then also our json server. And real quick, notice that I'm using one and symbol. That means I want these commands to run simultaneously. If I used two ands, that would mean let this command complete and then run this, but that's not quite right. I want them to run at the same time. Okay, so let's try it out. npm run and then the name of the script, start.

Okay, so let's try it out. npm run and then the name of the script, start. Okay, so now notice it boots up the server and then it runs npx serve. So now if I switch back and refresh, everything's working and I can now get up and running with a single command. Very cool. Okay, next up, I'd like these to be columns. So if I go back to my assignment section, why don't we set a class of flex on the wrapper here? Give it a refresh.

Yeah, but now this is awkwardly placed. So I'm going to show you how to fix that. But just for now, let's comment it out. Okay, next I'd like a little space between each of these columns and I can use the gap. Maybe we'll do eight and then we'll set a gap of two rims. Perfect. But next, notice that the width of our assignment list is contingent upon the number of characters in the assignment.

So for example, if I were to tweak this, finish Leracasts's video for work or whatever, suddenly it gets wider. So why don't we set a hard-coded width on each of the assignments? We'll go into assignment list and maybe on this section here, I'll set a width of 60 and that is 15 rims. So if my base font size is 16 pixels, then we're looking at a width of about 240 pixels. All right, we switch back, we give it a refresh and now I think that looks better. So let's figure out a place for this to live because yeah, if I come back and refresh,

it's being added to a third column, which I don't want. I still want it to be placed at the bottom here. So we have a couple of choices, right? One option would be, well, let's put it within assignment list. But let's just see. I could put it right down here at the bottom and I could import it. So import assignment creates like so, but yet the issue here, if I come back and give it a refresh, is that of course, well, the layout is off.

So import assignment creates like so, but yet the issue here, if I come back and give it a refresh, is that of course, well, the layout is off. But the main issue is that we're now adding a new assignment input to every single list. And maybe that's what you want, but in our case, actually no. We only want to show it below the in progress assignment list and nowhere else. Now we could make something like this configurable or what if we did this? Let me undo this, scroll down to the bottom. And now instead of forcing this component here, why don't we just add a slot? This is our way of saying, okay, if you want to add anything here from the outside, we'll slot it in right below the UL.

This is our way of saying, okay, if you want to add anything here from the outside, we'll slot it in right below the UL. Otherwise we won't do anything. Okay, so let's see. I come back and refresh. That's back to how it was. And now in our assignments component, I can say for this top one here, I'm going to slot in anything we want. Let's do hello. And now you'll see on this component only, we've added hello.

Let's do hello. And now you'll see on this component only, we've added hello. Okay, so now I can swap this out with our assignment create component. And now we have a way to sort of selectively extend the components when and if we need to. So I come back and give it a refresh. And there we go. It's at the bottom. Okay, so now I can fix the layout here. And that should be pretty easy.

Okay, so now I can fix the layout here. And that should be pretty easy. In our assignment create component, let's set a class of flex or display a flex. Give it a refresh. And there we go. Looking pretty good. So yeah, slots provide one option for extending your components. And you can create as many named slots as you want. Another option would be to provide toggles of sorts. So for example, maybe some assignment list can be effectively closed or toggled, but

Another option would be to provide toggles of sorts. So for example, maybe some assignment list can be effectively closed or toggled, but not all of them. So let me show you what I mean. Let's go into assignment list and we'll say, let's wrap this within a div. And then I'll add a button here to close it. Let's see what that looks like. And yeah, but really I want it to be aligned up here on the far right. So on the div, let's set a class of flex and justify between. That'll push this to the far left and this to the far right.

So on the div, let's set a class of flex and justify between. That'll push this to the far left and this to the far right. There we go. And then let's align everything to the start. So I'll say item start and that'll push the top edges of each side to the top. So now the problem is I want to be able to close this list, but maybe the in progress list can never be closed, at least for our use case. And you can imagine maybe later we'll add an archived list. Well maybe you can close that one and this one, but again, you can never close in progress. So what do we do here?

Well maybe you can close that one and this one, but again, you can never close in progress. So what do we do here? Some assignment lists need to show an X while other assignment lists should not. Well yes, we could use slots for this, but it might get a little tricky. Instead, this is a good use case for simple flags. I'll show you what I mean. Why don't we say, look, only show this button if this component has been marked as, I don't know, can, can hide or toggle level, whatever you want. Let's keep it simple. If this component has been marked that it can be hidden, then we should show a hide

Let's keep it simple. If this component has been marked that it can be hidden, then we should show a hide button. Okay. Let's scroll down and we're going to create a new prop called can hide, and that's going to be a Boolean. And why don't we say by default, you cannot hide it. Okay. So if I come back and refresh, I should no longer see the close buttons, but if we now turn that on like this right here, can hide, that reads pretty well.

So if I come back and refresh, I should no longer see the close buttons, but if we now turn that on like this right here, can hide, that reads pretty well. Come back, refresh. Now I conditionally display that button if it's turned on. And yeah, that's a basic use of what we call flags. Now in terms of the name, I think can hide is kind of fun. But if it would be something where you would turn it on and off, then that's probably not right. Let's see if we can switch to something like toggle, toggleable or can toggle. Why don't we do can toggle actually, to be a little more future-proof.

Let's see if we can switch to something like toggle, toggleable or can toggle. Why don't we do can toggle actually, to be a little more future-proof. Assignment list, can toggle, and then we'll do it right up here as well. So now we want to say when you click on this button, so we'll go ahead and set that up. When you click on me, yeah, we have a couple options. We could track it locally. So for example, I could have a show property that's set to true. And then when you click on it, we set show to false. And then we can make this entire block contingent upon that property. So only show this section if show is truthy and we have assignments.

And then we can make this entire block contingent upon that property. So only show this section if show is truthy and we have assignments. So I think that would work. That would be one option. I click on it and now I don't display it at all. That would be fine. Another option, if you don't want to do that for some reason, would be to again, emit an event. So let me undo what we had before, which again, I think is fine, but yeah, we might want to instead emit an event that says hide or toggle, something like that.

So let me undo what we had before, which again, I think is fine, but yeah, we might want to instead emit an event that says hide or toggle, something like that. Now the button doesn't do anything. It just makes an announcement. And in fact, if I open up view dev tools, we go into our events and let's take care of it. I click on it and sure enough, we fire an event called toggle. Okay. So now the parent can decide how it wants to deal with that like this. Let's reformat and then say when you toggle, maybe we track it at this level, like show

So now the parent can decide how it wants to deal with that like this. Let's reformat and then say when you toggle, maybe we track it at this level, like show completed equals true. Then we can handle it at the parent level, something like maybe we have a show completed property and we make that equal to the opposite of what it currently is. All right. I'm just showing you different options you can consider. Okay. So now, yeah, we could do something like the show is probably appropriate, but we'll do the if like that.

So now, yeah, we could do something like the show is probably appropriate, but we'll do the if like that. Only show this component if show completed is true. Come back, refresh. And now we are handling that at the parent level. And that might be useful if there is more to show. Like maybe if you have a div here and yes, it shows the assignment list, but it also shows other things. So if you handle the toggle at this component level, yeah, again, you might end up in a weird situation where there's other things that also need to be toggled, but aren't.

So if you handle the toggle at this component level, yeah, again, you might end up in a weird situation where there's other things that also need to be toggled, but aren't. So yeah, that would be one way to do this and you just elevate it like so. And yeah, again, probably V show is more appropriate here. Yeah. So that would be an option as well. If I had down here, blah, blah, just to show you. Now if I click on the X, it will toggle the assignment list, but also anything else that happens to be wrapped in that parent div. So that would be the use case there.

Okay. So now we've reviewed two different ways that we can extend our components or at least make them a little more flexible. The first option is through the use of slots. And the second option is to add flags to your components. Pretty cool.

You can watch this segment with timestamps here: 0:00-10:46

If you want me to extract or explain any specific part or code example from this episode, just ask!


## Translation

Aqui está a transcrição completa do Episódio 14, "Componentes Mais Flexíveis com Slots e Flags", da série "Learn Vue 3: Step by Step" no Laracasts:

Certo, a seguir deveríamos falar sobre configurabilidade de componentes ou flexibilidade de componentes, algo assim, preencha a lacuna. É muito legal podermos reutilizar componentes, mas com certeza haverá casos em que precisamos ajustá-los ou modificá-los de alguma forma. Então, vamos descobrir o que podemos fazer nesse sentido. Para começar, bom, deixa eu te mostrar uma coisa. Se eu iniciar nosso servidor com npx serve e abrirmos isso no navegador, perceba que não vejo nenhuma tarefa aqui como antes. E isso porque, veja só, ainda não iniciamos aquele servidor de API falso. Então eu teria que abrir uma nova aba e digitar npx json-server --port 3001.

E isso porque, veja só, ainda não iniciamos aquele servidor de API falso. Então eu teria que abrir uma nova aba e digitar npx json-server --port 3001. E agora posso voltar e atualizar a página. E sabe, isso é meio chato. Então, normalmente minha regra é: quando eu preciso executar múltiplos comandos para rodar meus testes ou iniciar meu servidor, sempre coloco esses comandos dentro de um script no package.json. Veja como: vamos até o package.json e adicionamos uma nova seção de scripts. Vamos criar um novo script chamado start. E quero que ele execute esses dois comandos: npx serve e também npx json-server.

Vamos criar um novo script chamado start. E quero que ele execute esses dois comandos: npx serve e também npx json-server. Ok, então quero o comando serve e também o json-server. E perceba que estou usando um único símbolo &. Isso significa que quero que esses comandos rodem simultaneamente. Se usasse dois &, isso significaria “deixe esse comando terminar e depois execute o outro”, mas isso não é o que queremos. Quero que rodem ao mesmo tempo. Ok, vamos testar. npm run e depois o nome do script, start.

Ok, vamos testar. npm run start. Agora veja, ele inicia o servidor e executa npx serve. Então, se eu voltar e atualizar, tudo está funcionando e agora posso colocar tudo para rodar com um único comando. Muito legal. Ok, agora quero que isso fique em colunas. Então, se eu voltar para minha seção de tarefas, por que não colocamos uma classe flex no wrapper? Damos um refresh.

É, mas agora isso está posicionado de forma estranha. Vou te mostrar como corrigir isso. Mas por enquanto, vamos comentar. Ok, agora quero um pouco de espaço entre essas colunas e posso usar gap. Talvez façamos gap-8, o que significa um espaçamento de 2 rem. Perfeito. Mas veja que a largura da nossa lista de tarefas depende do número de caracteres da tarefa.

Por exemplo, se eu alterar para algo como “finalizar o vídeo do Laracasts para o trabalho” ou algo assim, de repente fica mais largo. Então, por que não definimos uma largura fixa para cada tarefa? Vamos no AssignmentList.vue e talvez nessa seção aqui eu defina w-60, que são 15 rems. Se o tamanho base da fonte é 16 pixels, então estamos falando de uma largura de cerca de 240 pixels. Certo, voltamos, atualizamos e agora acho que ficou melhor. Então, vamos decidir onde isso vai viver, porque sim, se eu voltar e atualizar,

isso está sendo adicionado a uma terceira coluna, o que não quero. Ainda quero que isso fique posicionado na parte inferior. Temos algumas opções, certo? Uma opção seria colocar dentro de AssignmentList. Mas vamos ver. Eu poderia colocá-lo aqui embaixo e importar, assim: import AssignmentCreate. Mas o problema é que, se eu atualizar, o layout fica errado.

Mas o problema principal é que agora estamos adicionando um campo de criação de tarefas para todas as listas. E talvez seja isso que você queira, mas no nosso caso, na verdade não. Só queremos mostrar isso abaixo da lista de tarefas em andamento e em nenhum outro lugar. Agora poderíamos tornar isso configurável, ou, e se fizermos o seguinte? Vou desfazer isso, rolar até o fim. E agora, em vez de forçar esse componente aqui, por que não adicionamos um slot? Essa é a nossa maneira de dizer: “ok, se você quiser adicionar algo aqui de fora, vamos inserir isso logo abaixo do ul.”

Essa é a nossa forma de dizer: se quiser adicionar algo de fora, será inserido logo abaixo do ul. Caso contrário, não faremos nada. Ok, vamos ver. Volto e atualizo. Tudo voltou ao normal. E agora, no nosso componente Assignments, posso dizer que, para esse primeiro aqui, vou inserir qualquer coisa no slot. Vamos testar com um "hello". E agora, só nesse componente, vemos o “hello” adicionado.

Vamos testar com um "hello". E agora, só nesse componente, vemos o “hello” adicionado. Agora posso substituir isso pelo nosso componente AssignmentCreate. E agora temos uma maneira de estender os componentes de forma seletiva, quando necessário. Volto e atualizo. Pronto, está lá embaixo. Agora posso corrigir o layout, e isso deve ser bem fácil.

Agora posso corrigir o layout, e isso deve ser bem fácil. No nosso componente AssignmentCreate, vamos definir class="flex". Atualizamos. Pronto. Está com uma aparência ótima. Então sim, slots oferecem uma maneira de estender seus componentes. E você pode criar quantos slots nomeados quiser. Outra opção seria fornecer "alternadores", ou seja, flags. Por exemplo, talvez algumas listas de tarefas possam ser fechadas ou ocultadas, mas

outras não. Deixe-me te mostrar o que quero dizer. Vamos em AssignmentList.vue e vamos envolver isso com uma div. Então adiciono um botão aqui para fechar. Vamos ver como fica. Mas na verdade quero que fique alinhado à direita. Então, na div, coloco a classe flex justify-between. Isso empurra um conteúdo para a esquerda e outro para a direita.

Coloco a classe flex justify-between. Isso empurra um conteúdo para a esquerda e outro para a direita. Pronto. Depois vamos alinhar tudo ao topo com items-start. Agora o problema é que quero poder fechar essa lista, mas talvez a lista de tarefas “em andamento” nunca possa ser fechada — pelo menos no nosso caso de uso. E imagine que no futuro adicionamos uma lista de tarefas arquivadas — talvez essa sim possa ser fechada. Mas, de novo, não queremos que a lista “em andamento” seja escondida. O que fazer?

Algumas listas precisam mostrar um "X", enquanto outras não. Sim, poderíamos usar slots para isso, mas talvez fique complicado. Em vez disso, esse é um bom caso para usar flags simples. Vou te mostrar o que quero dizer. Vamos dizer que só mostramos esse botão se o componente tiver sido marcado com algo como canHide, ou canToggle, o que você quiser. Vamos manter simples: se esse componente foi marcado como podendo ser escondido, então mostramos o botão de esconder.

Vamos manter simples: se esse componente foi marcado como podendo ser escondido, então mostramos o botão. Vamos criar uma nova prop chamada canHide, e ela será um booleano. E, por padrão, vamos dizer que não pode ser escondido. Se eu atualizar agora, o botão de fechar desaparece. Mas se ativarmos essa opção, assim: can-hide, fica bem claro.

Atualizamos, e agora mostramos esse botão somente se a flag estiver ativada. Isso é o uso básico do que chamamos de flags. Em termos de nome, canHide é legal. Mas se for algo que você possa alternar (ligar e desligar), então talvez o nome não seja ideal. Vamos usar algo como toggleable, ou melhor ainda: canToggle, para ser mais à prova de futuro.

Usamos canToggle, colocamos no componente AssignmentList, e também lá em cima. Agora, queremos que, ao clicar no botão, ele alterne a visibilidade. Então vamos configurar isso. Temos algumas opções: podemos controlar isso localmente. Por exemplo, podemos ter uma propriedade show, que começa como true, e quando clicamos, definimos como false. E então tornamos esse bloco visível apenas se show for verdadeiro e houver tarefas.

Essa seria uma opção: clico e ele não exibe mais nada. Está tudo bem. Outra opção, se você não quiser controlar isso localmente, seria emitir um evento. Então desfazemos a lógica anterior — que funciona bem, aliás —, e agora emitimos um evento como toggle.

O botão não faz nada além de emitir um aviso. E se abrirmos o Vue Devtools, vamos para os eventos e verificamos: clicamos, e sim, um evento toggle é disparado. Agora o componente pai pode decidir o que fazer com isso. Por exemplo: dizemos que ao escutar @toggle, vamos mudar uma variável chamada showCompleted para o oposto do valor atual.

Assim, o controle fica no componente pai. Isso pode ser útil se houver mais coisas a mostrar. Como, por exemplo, se você tiver uma div que, além da lista, mostra outras informações. Se o toggle for feito no nível do componente filho, você pode acabar em uma situação estranha, onde outras partes do layout não são escondidas como deveriam.

Então, esse seria um jeito de fazer isso: eleva o controle. E sim, talvez o v-show seja mais apropriado aqui. Se eu colocar um "blá blá" dentro da div, agora, ao clicar no X, escondemos a lista e qualquer outra coisa que esteja dentro da div do componente pai. Esse é o uso ideal aqui.

Concluindo: vimos duas maneiras diferentes de estender ou tornar nossos componentes mais flexíveis.
A primeira é usando slots.
A segunda é adicionando flags aos seus componentes. Muito legal.

Você pode assistir a esse episódio com marcações de tempo aqui: 0:00–10:46.

Se quiser que eu extraia ou explique alguma parte específica ou código mencionado nesse episódio, é só me avisar!