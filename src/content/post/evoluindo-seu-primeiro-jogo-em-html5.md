+++
title = "Evoluindo Seu Primeiro Jogo Em HTML5"
date = "2014-02-17"
slug = "2014/evoluindo-seu-primeiro-jogo-em-html5"
Categories = ['games']
+++

<p>O post de hoje é uma continuação do anteriormente escrito Seu primeiro jogo em HTML5. O objetivo dessa continuação é aprender mais alguns conceitos de desenvolvimento de jogos e animar um pouco o nosso game que não estava lá essas coisas de divertido. Você acompanha a primeira parte no seguinte link <a href="http://flaviosilveira.com/2013/seu-primeiro-jogo-em-html5/" title="Seu primeiro jogo em HTML5 - Parte 1">http://flaviosilveira.com/2013/seu-primeiro-jogo-em-html5/</a>.</p>

<!--more-->


<p>Nessa continuação vamos adicionar um pouco de jogabilidade, variando a velocidade das bolas que caem e também seu tamanho e a sua pontuação.</p>

<p><strong>Objeto</strong><br/>
Estamos querendo tipos diferentes de bolas. Tamanhos diferente, velocidades diferentes, pontos diferentes. Ainda são bolas, mas cada uma de um jeito, certo?<br/>
Estamos falando então de uma mesma coisa, mas com características e comportamentos diferentes, concorda?</p>

<p>Vamos entrar aqui então com o conceito de programação orientada a objetos para resolver o problema.<br/>
Dependendo do seu nível em programação, esse pode ser um conceito novo e, se esse é o caso, você vai precisar fazer algumas pesquisas caso queira entender melhor alguns pontos. Se você não conhece Orientação a Objetos recomendo que pare a leitura aqui e pesquise á respeito e também como é aplicado na linguagem javaScript. Não é necessário um conhecimento profundo neste momento, dê aquela lida no conceito, faça um exemplos simples em um papel e volte a leitura do post. Caso você já entenda o suficiente desse conceito é seguir em frente.</p>

<p>Precisamos então programar algo que crie as bolas para a gente, uma fôrma das bolas, que é equivalente a uma classe em orientação a objetos. Em javaScript não temos classes propriamente ditas, tudo que precisamos fazer é uma função.</p>

<p>Pegue então o código que desenvolvemos no post anterior.<br/>
Antes da nossa função inicializar, vamos criar uma função chamada bola e dentro dela vamos colocar todas as variáveis iniciais referente a bola que estão hoje na função inicializar.<br/>
Veja como fica:</p>

title = "evoluindo seu primeiro jogo em html5"
    {
                bolaDiametro = 10;
                bolaPosX = canvas.width / 2;
                bolaPosY = -10;
        velocidadeBola = 10;
        colisao = false;
    }
        
    function inicializar()
    {
        barraAltura = 15;
        barraLargura = 90;

        pontosJogador = 0;
        jogadorPosicaoX = (canvas.width - barraLargura) / 2;
        velocidadeJogador = 20;
                
        canvas = document.getElementById("canvas");
        context = canvas.getContext("2d");              
                
        document.addEventListener('keydown', keyDown);
                
        setInterval(gameLoop, 30);
    }
</pre>


<p>Dentro da função inicializar vamos criar a primeira bola e adicionar ela dentro de um array. Esse array vai guardar todas as bolas que estiverem em cena. Dessa maneira teremos controle sobre elas.</p>

title = "evoluindo seu primeiro jogo em html5"
    {
        …     
        var primeira = new bola()
        bolas = new Array(primeira);
        …
    }
</pre>


<p>Rodando o seu código nesse momento verá que está tudo como antes. A questão é que nesse ponto não estamos utilizando nenhum conceito novo. Tudo que foi feito foi adicionar o código de antes para uma função, e chamar ela. Nem estamos trabalhando com o array criado não é mesmo?</p>

<p>Vamos trocar a nossa função para ela realmente virar um objeto, com propriedades. Para isso adicione a palavra chave this a frente de todas as variáveis.<br/>
Essa palavra chave fará referência para aquela instância de objeto e apenas ela. Caso não entenda isso aqui, talvez você entenda melhor quando trabalharmos com o array das bolas que estão em cena.</p>

title = "evoluindo seu primeiro jogo em html5"
{
    this.bolaDiametro = 10;
    this.bolaPosX = canvas.width / 2;
    this.bolaPosY = -10;
    this.velocidadeBola = 10;
    this.colisao = false;
}
</pre>


<p>Neste momento o game para de funcionar. Isso porque as variáveis que temos dentro de nosso gameLoop já não existem mais. Temos agora um objeto bola e esse objeto adicionado a um array que é responsável por todas as bolas em cena. Precisamos trabalhar com esse array para as coisas voltarem a funcionar.</p>

<p>Para questão de organização, já que as variáveis que definiam as características da bola não nos servem mais, podemos limpar elas da nossa definição inicial na primeira linha de javaScript. Mas não esqueça de adicionar a variável para o nosso array de bolas, para que fique acessível para todo o resto do código. Ficando assim:</p>

title = "evoluindo seu primeiro jogo em html5"
</pre>


<p>Agora vá até a função de gameLoop, e repare onde está a lógica da bola. Começa onde iniciamos com o desenho dela e termina com a verificação da colisão.<br/>
O que vamos fazer aqui é tirar tudo isso, e aplicar para cada objeto dentro do array bolas usando um foreach. Fica dessa forma:</p>

title = "evoluindo seu primeiro jogo em html5"
bolas.forEach(function(bola, indice){
    context.beginPath();
    context.arc(b.bolaPosX, b.bolaPosY, b.bolaDiametro, 0, Math.PI * 2, true);
    context.fill();
                
    if(bola.bolaPosY &lt;= canvas.height)
    {
        bola.bolaPosY += bola.velocidadeBola;
    }
    else
    {
        bola.bolaPosX = Math.random() * 600;
        bola.bolaPosY = -10;
        bola.colisao = false;
    }
                
    // Checar Colisão
    if((bola.bolaPosX &gt; jogadorPosicaoX && bola.bolaPosX &lt; jogadorPosicaoX + barraLargura) && bola.bolaPosY &gt;= canvas.height - barraAltura && bola.colisao == false)
    {
        pontosJogador++;
        bola.colisao = true;
    }
});
</pre>


<p>Na função de forEach do javaScript o primeiro parâmetro é o elemento em si e o segundo o indíce.<br/>
Para cada objeto dentro do array, ele vai executar uma vez.<br/>
Note que agora nas variáveis com as características da bola de antes, adicionamos “b.”. É dessa maneira que acessamos as propriedades do objeto.<br/>
Tome cuidado para não adicionar isso nas variáveis do jogador nem do canvas.<br/>
Neste ponto se jogo volta a funcionar como antes, mas dessa vez usando bola com o conceito de orientação a objetos.</p>

<p><strong>Cada bola um Objeto</strong><br/>
Olhe o código e verá que quando a bola chega ao final do canvas ou quando ela colide com o jogador, não criamos uma nova, apenas editamos novamente as propriedades do mesmo objeto que foi criado da primeira vez. Vamos mudar isso alterando o if que checa se a bola já passou do canvas. Agora quando ela passar do canvas, vamos retirar ela do nosso array usando a função splice do javaScript.</p>

title = "evoluindo seu primeiro jogo em html5"
    {
        bola.bolaPosY += bola.velocidadeBola;
    }
    else
    {
        bolas.splice(indice, 1);
    }
</pre>


<p>Tudo que estava dentro do else, que era usado para criar uma nova bola, não é mais necessário. Trocamos tudo isso pela função splice.<br/>
Splice irá retirar um item do array baseado em seu índice. O primeiro parâmetro é o índice que queremos tirar e o segundo é a quantidade de índices a partir dele, que para nós será sempre 1.</p>

<p>Rodando seu game agora, quando a bola passa pelo canvas, não é criado nenhuma nova.</p>

<p><strong>Criando uma nova bola</strong><br/>
Nosso foreach só é executado se tivermos bolas dentro dele. Como nossa primeira bola passou pelo canvas e foi destruída, vamos adicionar uma verificação antes do foreach para caso nosso array estiver vazio, criar uma nova bola dentro dele. Para isso vamos usar um push. Veja como fica:</p>

title = "evoluindo seu primeiro jogo em html5"
{
    bolas.push(new bola());
}
</pre>


<p>Certo, mas todas as bolas estão saindo no mesmo lugar. Dá para ganhar o jogo parado!<br/>
Isso está acontecendo por conta da posição X e Y estarem fixas dentro da criação do nosso objeto.<br/>
Vamos alterar isso com a ajuda da classe Math de javaScript.</p>

title = "evoluindo seu primeiro jogo em html5"
{
    this.bolaDiametro = 10;
    this.bolaPosX = Math.random() * 600;
    this.bolaPosY = -10;
    this.velocidadeBola = 10;
    this.colisao = false;
}
</pre>


<p>A posição Y da bola pode continuar sendo -10 para aparecer antes do canvas. Mas para deixar a posição X randômica, use Math.random multiplicando pela largura do seu canvas.</p>

<p>Use um pouco da matemática aqui para alterar também a velocidade de sua bola.</p>

title = "evoluindo seu primeiro jogo em html5"
{
    this.bolaDiametro = 10;
    this.bolaPosX = Math.random() * 600;
    this.bolaPosY = -10;
    this.velocidadeBola = Math.random() * (10 - 6) + 6;
    this.colisao = false;
}
</pre>


<p>No exemplo acima temos velocidades entre 10 e 6.<br/>
Acima você vê como obter um número randômico entre um mínimo e um máximo. Math.random multiplicado pelo máximo diminuindo o mínimo e somado ao mínimo.<br/>
Caso queira tentar entender o “truque” acima lembre-se que Math.random retorna um número entre 0 e 1.</p>

<p><strong>Diâmetros e pontos variados</strong><br/>
Para termos diâmetros variados e pontos baseados nesse diâmetro, vamos primeiro definir isso em um array, antes do nosso objeto bola.<br/>
Nesse array, criamos um objeto que tem um dâimetro e uma pontuação.</p>

title = "evoluindo seu primeiro jogo em html5"
        
var diametros = new Array(
    {'diametro' : 7, 'pontos' : 1},
    {'diametro' : 10, 'pontos' : 2},
    {'diametro' : 15, 'pontos' : 3}
);
</pre>


<p>Com isso definido, vamos agora usar a mesma fórmula que usamos acima para pegar um número randômico que esteja dentro dos valores desse array. Lembrando que o array começa em 0, então vamos diminuir um ao final. Vamos armazenar esse número, e usar ele para o tamanho da bola e consequentemente sua pontuação. Veja como fica:</p>

title = "evoluindo seu primeiro jogo em html5"
{
    var indice = Math.round(Math.random() * (3 - 1) + 1) - 1;
    this.bolaDiametro = diametros[indice]['diametro'];
    this.pontos = diametros[indice]['pontos'];
                
    this.bolaPosX = Math.random() * 600;
    this.bolaPosY = -10;
    this.velocidadeBola = Math.random() * (10 - 6) + 6;
    this.colisao = false;
}
</pre>


<p>Neste momento os tamanhos de bolas já aparecem diferentes na tela. Mas a pontuação continua somando 1 sempre.<br/>
Precisamos alterar nosso gameLoop para pegar os pontos do objeto em questão. Veja como:</p>

title = "evoluindo seu primeiro jogo em html5"
{
    pontosJogador += bola.pontos;
    bola.colisao = true;
}
</pre>


<p>Trocamos o incrementar que tinha antes para um += que vai pegar o valor que já tinha na variável e somar o valor dos pontos daquela bola que colidiu.</p>

<p>Mais de uma ao mesmo tempo e tudo junto<br/>
Para finalizar, que tal deixar cair mais de uma bola ao mesmo tempo?</p>

<p>Para fazer isso de forma bem simples, adicione dentro do foreach um verificação para caso aquela bola já tenha passado da posição 50 em Y, criar uma nova.</p>

title = "evoluindo seu primeiro jogo em html5"
if(bola.bolaPosY &gt;= 50 && bolas.length &lt;= 2)
{
    bolas.push(new bola());
}
</pre>


<p>Cuidado! Veja no código acima que eu também verifiquei quantas bolas estão em cena antes de adicionar uma nova. Caso contrário você vai ter um efeito matrix em sua tela e travar seu navegador. Tente por sua conta e risco :).</p>

<p><strong>Conclusão</strong><br/>
Você pode aplicar o conceito de orientação a objetos para tudo o que for objeto na tela. Dessa maneira você vai ter um melhor controle das coisas e é a maneira correta de trabalhar em jogos.</p>

<p>Acompanhe o repositório gitHub dessa série em <a href="https://github.com/flaviosilveira/primeiro-jogo-html5" title="Git Hub - Seu primeiro jogo em HTML5">https://github.com/flaviosilveira/primeiro-jogo-html5</a>.</p>

<p>Aguarde o próximo post da série. Abraços!</p>
