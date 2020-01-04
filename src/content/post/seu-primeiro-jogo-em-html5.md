+++
title = "Seu Primeiro Jogo Em HTML5"
date = "2013-09-19"
slug = "2013/09/19/seu-primeiro-jogo-em-html5"
Categories = ['games']
+++

<p>Hoje quero ajudar você a desenvolver seu primeiro jogo, que talvez não fique aquele delírio de diversão, mas é o primeiro passo para você começar a entrar nesse mundo de desenvolvimento de jogos. E para isso vamos usar tecnologias que você tem em mãos no seu navegador. HTML5 e javascript.</p>

<p>Vou passo a passo, tentando deixar claro o porque de algumas coisas primordiais em desenvolvimento de jogos. Cometendo erros para depois corrigi-los. Isso talvez torne o post um pouco extenso, então busque sua garrafa de água para manter seu cérebro hidratado.</p>

<!--more-->


<p>Para os sem saco, no final do post você tem um link para o código completo.</p>

<p><strong>O Jogo</strong><br/>
Eu havia pensado em desenvolver um <a href="http://en.wikipedia.org/wiki/Arkanoid">Arkanoid</a> para esse post, mas a criação e a lógica subiriam um pouco de nível e a intenção de começar devagar iria se perder. Então temos algo bem mais simples, bolas que caem do topo da tela e que você deve resgatá-las com a plataforma.<br/>
<img src="../../../assets/uploads/2013/09/Imagem1-300x240.png" alt="" title="Imagem1" width="300" height="240" class="alignnone size-medium wp-image-660" /><br style="clear:both;" /></p>

<p><strong>HTML</strong><br/>
Para montar o desenho da tela, o jogador e a bola, vamos usar a tag canvas. Ela está presente há algum tempo nos navegadores, tendo começado no Safari da Apple, mas ganhou mais popularidade recentemente com o HTML5.</p>

<p>Crie um arquivo HTML com qualquer nome e dentro dele crie um Canvas.</p>

title = "seu primeiro jogo em html5"
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;Seu Primeiro Jogo - HTML5&lt;/title&gt;
    &lt;/head&gt;   
    &lt;body&gt;
        &lt;canvas id="canvas" width="600" height="480"&gt;
            Navegador não suporta HTML5
        &lt;/canvas&gt;
    &lt;/body&gt;
&lt;/html&gt;
</pre>


<p>Usamos o Doctype do HTML5 junto com um título.<br/>
Dentro da tag body vemos o canvas, onde definimos uma largura e uma altura.</p>

<p>Carregando isso no navegador, não vemos nada. Mas não se preocupe, você não fez nada de errado. Vamos com ajuda de um CSS definir uma borda para nosso canvas, assim vamos ver ele na tela. Nosso head vai ficar como abaixo.</p>

title = "seu primeiro jogo em html5"
    &lt;title&gt;Seu Primeiro Jogo - HTML5&lt;/title&gt;
     &lt;style type="text/css"&gt;
    canvas {
        border: 1px solid #000000;
    }
     &lt;/style&gt;
&lt;/head&gt;  
</pre>


<p>Fique a vontade para alterar a cor, o tipo da borda ou o que mais quiser nesse CSS.</p>

<p>Nosso trabalho com HTML acaba aqui. Tudo o que vamos usar agora é JavaScript. Para isso vamos então chamar uma função javaScript quando o body estiver totalmente carregado, da seguinte maneira.</p>

title = "seu primeiro jogo em html5"
</pre>


<p><strong>JavaScript</strong><br/>
Vamos criar nosso JavaScript no mesmo arquivo do HTML. Nosso intuito não é discutir arquitetura aqui. Vamos criar uma tag script logo depois de nosso canvas, e já vamos definir nossa função inicializar que chamamos acima.</p>

title = "seu primeiro jogo em html5"
function inicializar()
{
 // Nosso código aqui
}
&lt;/script&gt;
</pre>


<p><strong>Jogador</strong><br/>
Vamos começar desenhando o jogador, que nada mais é do que uma barra.</p>

<p>Vamos iniciar algumas variáveis acima da nossa função. barraAltura e barraLargura.<br/>
Em seguida em nossa função inicializar setamos os valores desejados para elas.</p>

<p>Para desenhar com o canvas, precisamos capturar o elemento com javaScript e usar o contexto que no nosso caso vai ser 2D.</p>

<p>O método para desenhar retângulos com canvas é fillRect. Essa função nos pede a posição do elemento (pontos X e Y), sua largura e sua altura.</p>

<p>Como a posição X (horizontal) do jogador vai ficar mudando, vamos criar uma variável para isso também. Já a posição Y (vertical) como não vai mudar, podemos deixá-la fixa usando a altura do canvas menos o tamanho da barra.</p>

<p>Confira o código abaixo com as explicações acima:</p>

title = "seu primeiro jogo em html5"
        
function inicializar()
{
    barraAltura = 15;
    barraLargura = 90;

    jogadorPosicaoX = 0;

    canvas = document.getElementById("canvas");
    context = canvas.getContext("2d");

    context.fillRect(jogadorPosicaoX, canvas.height - barraAltura, barraLargura, barraAltura);
}
</pre>


<p>Resultado na tela:<br/>
<img src="../../../assets/uploads/2013/09/imagem2-300x240.png" alt="" title="imagem2" width="300" height="240" class="alignnone size-medium wp-image-659" /><br style="clear: both;" /></p>

<p>Nosso jogador não ficou centralizado, porque definimos sua posição X como 0, ou seja, o canto esquerdo do canvas.<br/>
Altere os valores de pouco em pouco para você perceber como o jogador irá se mover, isso também irá ajudar na lógica de colisão mais para frente. Entendido isso, vamos deixar nosso jogador centralizado, pegando o tamanho do canvas e dividindo por 2.</p>

<p>Ao atualizar seu browser e conferir o resultado nesse ponto não se preocupe, você não está com problema na vista. É necessário diminuir o tamanho da barra para que o jogador fique exatamente no centro do canvas. Ficando então da seguinte maneira.</p>

title = "seu primeiro jogo em html5"
</pre>


<p>Use os parênteses para fazer a subtração primeiro.</p>

<p><strong>Comandos do jogador</strong><br/>
É hora de dar vida ao jogador.<br/>
O que queremos é que quando for pressionado para a direita, para esquerda, a nossa barra obedeça isso.</p>

<p>Vamos deixar nosso javaScript de olho quando o jogador apertar alguma tecla com os Event Listeners do javaScript.</p>

<p>Então definimos a função desse listener. Aqui no meu notebook, o código das teclas para esquerda e para direita são respectivamente 37 e 39. Isso pode variar se você tem um tipo diferente de teclado ou ainda se quiser outras teclas de comando.</p>

<p>Vamos agora reposicionar o jogador de acordo com as teclas pressionadas.<br/>
Se apertar a tecla código 37, esquerda, diminuimos a posição do jogador. Se apertar a tecla código 39 vamos somar.</p>

<p>Mas vamos somar/diminuir quanto? Vamos definir uma variável para a velocidade do jogador, essa velocidade será a quantidade de pixels que o jogador se movimenta a cada vez que é pressionado as teclas. Voltando então, se pressionar para a direita somamos a velocidade do jogador, se pressionar para a esquerda diminuimos a velocidade do jogador.</p>

<p>Não esqueça de desenhar a barra novamente com a posição nova do jogador.</p>

<p>Confira o código abaixo:</p>

title = "seu primeiro jogo em html5"
        
function inicializar() ...
    velocidadeJogador = 20;
    ...
    document.addEventListener('keydown', keyDown);
}
            
function keyDown(e) 
{
    if(e.keyCode == 37)
    {
        jogadorPosicaoX -= velocidadeJogador;
    }
                
    if(e.keyCode == 39)
    {
        jogadorPosicaoX += velocidadeJogador;
    }

    context.fillRect(jogadorPosicaoX, canvas.height - barraAltura, barraLargura, barraAltura);
}
</pre>


<p>Atualizando nossa tela e apertando as teclas você vê o resultado.<br/>
<img src="../../../assets/uploads/2013/09/Imagem3-300x241.png" alt="" title="Imagem3" width="300" height="241" class="alignnone size-medium wp-image-658" /><br style="clear: both;" /></p>

<p>Percebe um problema? Temos dois na verdade, mas vamos um de cada vez.<br/>
O primeiro é que não estamos apagando a posição anterior do jogador. Estamos então tendo a sensação de que a barra está aumentando de tamanho.</p>

<p>Para resolver isso temos que entender um conceito no desenvolvimento de jogos que é o GameLoop.<br/>
Não vou entrar em detalhes á fundo, mas acompanhe.</p>

<p><strong>Game Loop &#8211; Explicação ultra simples</strong><br/>
Um jogo não passa de um loop infinito. Se você perde, você volta ao começo.<br/>
Então pense em um loop que contêm algumas verificações dentro dele que serão os comandos do jogador, pontuação e etc.</p>

<p>Durante esse loop, os inimigos, o jogador e outras coisas na tela irão mudar de posição o tempo todo.<br/>
Mas você deve apagar a posição anterior caso contrário vai ficar um efeito como o que estamos tendo.</p>

<p>Então vamos apagar tudo da tela e fazer aparecer novamente. Ok!<br/>
Mas isso não pode ser visível ao jogador, a tela não pode parecer que está piscando.<br/>
Então vamos definir um tempo, um certo número de frames que não permita que o jogador perceba isso.</p>

<p>Então vamos re-estruturar nosso código, pensando nesse conceito.</p>

<p>No topo temos a definição das variáveis.</p>

<p>Em seguida na função inicializar, vamos deixar apenas o valor inicial das variável e o listener, e de dentro dela chamar o gameLoop.<br/>
Para o loop, vamos usar setInterval e chamar nossa função a cada 30 milisegundos.<br/>
Ficando assim:</p>

title = "seu primeiro jogo em html5"
        
function inicializar()
{
    barraAltura = 15;
    barraLargura = 90;

    jogadorPosicaoX = (canvas.width - barraLargura) / 2;
    velocidadeJogador = 20;

    canvas = document.getElementById("canvas");
    context = canvas.getContext("2d");              

    document.addEventListener('keydown', keyDown);

    setInterval(gameLoop, 30);
}
</pre>


<p>Seguimos o código com a função keyDown que fizemos acima, mas já vamos resolver nosso segundo problema que não comentei anteriormente. O jogador não pode continuar indo para a direita ou para esquerda se ele chegar aos limites do canvas. Então adicionamos algumas verificações para isso. Repare também que não vamos mais redesenhar a tela a partir dessa função.</p>

title = "seu primeiro jogo em html5"
{
    if(e.keyCode == 37)
    {
        if(jogadorPosicaoX &gt; 0)
        {
            jogadorPosicaoX -= velocidadeJogador;
        }
    }

    if(e.keyCode == 39)
    {
        if(jogadorPosicaoX &lt; (canvas.width - barraLargura))
        {
            jogadorPosicaoX += velocidadeJogador;
        }
    }
}
</pre>


<p>Por último nosso gameLoop. Ele contém uma função que desenha um retângulo em branco em cima de toda a área do canvas.<br/>
Isso limpa a nossa tela. E em seguida redesenhamos nosso jogador.</p>

title = "seu primeiro jogo em html5"
{
    context.clearRect(0, 0, canvas.width, canvas.height);

    context.fillRect(jogadorPosicaoX, canvas.height - barraAltura, barraLargura, barraAltura);
}
Recarregue sua tela e se divirta movimentando a barra.

&lt;strong&gt;Bola&lt;/strong&gt;
Vamos primeiro desenhar uma bola parada no topo da tela.
Vamos definir algumas configurações para ela. Diâmetro, posição X, posição Y e sua velocidade.
1
var barraAltura, barraLargura, jogadorPosicaoX, velocidadeJogador, bolaDiametro, bolaPosX, bolaPosY, velocidadeBola;
        
function inicializar()
{
    ...
    bolaDiametro = 10;
    bolaPosX = canvas.width / 2;
    bolaPosY = 0;
    velocidadeBola = 10;
    ...
}
</pre>


<p>Para desenhar a bola, adicione as seguintes linhas dentro de gameLoop.</p>

title = "seu primeiro jogo em html5"
{
    ...
    context.beginPath();
    context.arc(bolaPosX, bolaPosY, bolaDiametro, 0, Math.PI * 2, true);
    context.fill();
    ...
}
</pre>


<p>Procure pesquisar some a função de desenho do arco que usamos acima. Foge do mérito desse artigo explicá-la.</p>

<p>Como resultado você deve ver metade da bola desenhada no topo do canvas. Como abaixo:<br/>
<img src="../../../assets/uploads/2013/09/Imagem4-300x240.png" alt="" title="Imagem4" width="300" height="240" class="alignnone size-medium wp-image-657" /><br style="clear: both;" /></p>

<p>Vemos metade dela pois ela é desenhada a partir do centro, como setamos Y para 0, a outra metade está acima do canvas.<br/>
Sendo desenhada do centro, não precisamos diminuir seu diâmetro para centralizar ela na tela, bastou dividir por 2 o eixo X.</p>

<p><strong>Movimentando a bola</strong><br/>
Bom, não queremos que a bola inicia com metade aparecendo, melhor que isso queremos que ela venha antes do canvas.<br/>
Você pode setar o valor de bolaPosY para -10 para que isso aconteça.</p>

title = "seu primeiro jogo em html5"
    bolaPosY = -10;
    ...
</pre>


<p>Agora vamos movimentar ela como se estivesse caindo, no eixo Y.<br/>
Simples não? Basta a cada gameLoop diminuir a velocidade da bola.</p>

<p>Mas veja que isso só pode acontecer se a posição Y da bola for menor que a altura do canvas, caso contrário a bola vai descer até o infinito.</p>

<p>E já que a bola chegou ao fim do canvas, que tal iniciar outra lá no topo?</p>

<p>Acompanhe isso no trecho abaixo:</p>

title = "seu primeiro jogo em html5"
if(bolaPosY &lt;= canvas.height)
{
    bolaPosY += velocidadeBola;
}
else
{
    bolaPosY = -10;
}
...
</pre>


<p>Legal! Mas o jogo já não é muito divertido, se a bola ficar caindo sempre no mesmo lugar então.<br/>
Vamos adicionar um cálculo para fazer a posição X da bola variar cada vez que é criada uma nova.<br/>
Basta reformular o nosso else acima.</p>

title = "seu primeiro jogo em html5"
else
{
    bolaPosX = Math.random() * 600;
    bolaPosY = -10;
}
...
</pre>


<p>Você já pode ir treinando para o game final agora.</p>

<p><strong>Colisão</strong><br/>
Chegou a hora de checar se a bola colide com a barra e com isso marcar pontos para você.</p>

<p>Vamos definir uma variável pontosJogador. Não esqueça de iniciá-la como zero dentro da função inicializar.</p>

title = "seu primeiro jogo em html5"

function inicializar()
{
    ...
    pontosJogador = 0;
    ...
}
</pre>


<p>Em seguida vamos pensar na matemática da colisão.<br/>
Temos que fazer um cálculo que coloque a bola em cima da barra.<br/>
Então primeiramente, a posição X da bola tem de ser maior que a posição X da barra.<br/>
Mas também essa posição X da bola tem de ser menor que a posição X da barra + o tamanho dela.<br/>
Lembrando que na barra, sua posição X é o início dela, no canto esquerdo, por isso somamos a sua largura.</p>

<p>Não podemos bater apenas o ponto X. O eixo Y da bola tem de ser maior ou igual que a altura do canvas menos a altura da barra.</p>

<p>Dentro do IF da colisão incrementamos os pontos do jogador.</p>

<p>Em seguida temos um código para escrever a pontuação na tela.</p>

<p>Confira o código abaixo com a explicação acima:</p>

title = "seu primeiro jogo em html5"
{
    pontosJogador++;
}

context.font = "32pt Tahoma";
context.fillText(pontosJogador, canvas.width - 70, 50);
</pre>


<p>Hora de rodar o seu jogo!<br/>
<img src="../../../assets/uploads/2013/09/Imagem5-300x241.png" alt="" title="Imagem5" width="300" height="241" class="alignnone size-medium wp-image-656" /><br style="clear: both;" /></p>

<p>Mas espere! Isso não é basquete e a cada bola que pegamos estamos fazendo 3 pontos ou mais.<br/>
Porque isso está acontecendo?</p>

<p>Ah, simples! Como refazemos a tela a cada 30 milesegundos, a bola leva muito mais tempo que isso para passar pela barra. Então ela está caindo no IF de colisão mais de uma vez.</p>

<p>Para resolver isso vamos adicionar uma flag dizendo se colidiu ou não.<br/>
Vamos primeiro definir essa variável, em seguida inicializar ela como false.</p>

title = "seu primeiro jogo em html5"

function inicializar()
{
    ...
    colisao = false;
    ...
}
</pre>


<p>Agora no IF onde checamos a colisão, mudamos o valor para true quando colidir, e antes de checar se colidiu verificamos se esse status ainda é false.</p>

title = "seu primeiro jogo em html5"
{
    pontosJogador++;
    colisao = true;
}
</pre>


<p>Por último, se uma bola nova começa a cair ela tem de vir com esse status como falso.<br/>
Lembra do nosso else que cria uma nova bola no eixo X?</p>

title = "seu primeiro jogo em html5"
else
{
    bolaPosX = Math.random() * 600;
    bolaPosY = -10;
    colisao = false;
}
...
</pre>


<p>Feito! Hora de chamar os amigos e iniciar um campeonato.</p>

<p><strong>Conclusão</strong><br/>
Estude alterando as variáveis como velocidade do jogador, velocidade da bola e etc.<br/>
A partir daqui pode surgir muita coisa. Quem sabe não continuamos desenvolvendo esse jogo em um próximo post?</p>

<p>Código completo aqui: <a href="https://github.com/flaviosilveira/primeiro-jogo-html5">https://github.com/flaviosilveira/primeiro-jogo-html5</a></p>

<p>Abraço!</p>