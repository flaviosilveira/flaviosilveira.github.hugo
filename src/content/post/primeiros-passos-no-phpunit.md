+++
title = "Primeiros Passos No PHPUnit"
date = "2012-10-14"
slug = "2012/primeiros-passos-no-phpunit"
Categories = ['desenvolvimento', 'php']
+++

<p>Fala pessoal!</p>

<p>Hoje vamos cobrir os primeiros passos de uma ferramenta super importante para quem quer avançar no desenvolvimento PHP, o PHPUnit. Não vamos passar aqui pela instalação e configuração dele, sendo que já temos vários artigos sobre isso internet a fora seja lá qual for seu sistema operacional. Eu estarei demonstrando os exemplos aqui no Mac OS X mas você pode seguir normalmente no seu sistema.</p>

<p>Para quem não sabe PHPUnit é um framework que nos ajuda a desenvolver testes unitários em PHP. Esse unitário se refere literalmente a unidade, pequenas partes. Logo, testes unitários são testes para pequenas partes de código. No objetivo geral, testando cada unidade vamos saber se toda nossa aplicação está funcionando corretamente, e se não está, qual parte (unidade) está falhando. Pense em um portal onde uma equipe grande trabalha e tem várias alterações de código diariamente para melhorias e correções. Os testes tem que estar sempre ok antes de algo ir para o ar, uma maneira rápida certeira de conferir se nada foi quebrado no código.</p>

<!--more-->


<p>Após instalar e configurar o PHPUnit a primeira coisa a fazer é testar se está tudo ok.<br/>
Para isso vá até o seu console e digite o comando <em>phpunit</em>.<br/>
A saída esperada é um helper como na imagem abaixo:<br/>
<img class="alignleft size-full wp-image-562" title="phpunit 1" src="../../assets/uploads/2012/10/Imagem1.png" alt="testando phpunit" width="487" height="214" /><br style="clear: both;" /></p>

<p>Caso você tenha problemas é hora de checar a sua instalação.<br/>
Se você usa sistema unix e instalou o PHPUnit via PEAR aqui vão algumas dicas para tentar resolver isso:</p>

<ul>
<li>Pode ser que esteja tudo instalado corretamente, mas o console não esteja localizando o comando do PHPUnit. Para resolver isso primeiro verifique se a PEAR está instalada tentando digitar o comando <em>pear</em>. Se sim, entre com o comando <em>pear config-get bin_dir</em> para saber o diretório do bin do PHPUnit. Confira se a saída está no seu PATH de comandos, com o comando <em>echo $PATH</em>. Caso não esteja use o comando <em>export</em> para adicionar esse caminho.</li>
<li>Se você tem certeza que o PEAR está instalado corretamente, execute o seguinte comando para reinstalar o PHPUnit <em>pear install &#8211;alldeps &#8211;force phpunit/PHPUnit</em>.</li>
</ul>


<p>Com tudo ok podemos seguir em frente.<br/>
Daqui em diante conto que você saiba pelo menos um mínimo de Orientação a Objetos para que acompanhe os exemplos abaixo.<br/>
Para que a gente entenda o que esperar do PHPUnit, vamos primeiro criar uma classe com pelo menos um atributo e seus métodos <em>get()</em> e <em>set()</em>.<br/>
Que tal a tradicional classe Carro com uma propiedade de cor?</p>

title = "primeiros passos no phpunit"
 * Classe Carro
 *
 **/
class Carro
{
    private $_cor;

    public function getCor()
    {
        return $this-&gt;_cor;
    }

    public function setCor($cor)
    {
        $this-&gt;_cor = $cor;
    }

}
</pre>


<p>Com a classe principal criada vamos agora preparar nossa classe de testes.<br/>
Vamos chamar nossa classe de testes de CarroTeste.php.</p>

title = "primeiros passos no phpunit"

/**
 * Classe Carro Teste
 **/
class CarroTeste extends PHPUnit_Framework_Testcase
{

}
</pre>


<p>Repare em duas coisas no código acima:</p>

<ul>
<li>Sua classe de testes deve conhecer a classe que vai ser testada (use require, include ou autoload).</li>
<li>Sua classe de testes precisa extender o framework PHP_Unit. Para extender o PHPUnit da mesma forma como no código acima, configure corretamente o seu <em>include_path</em> no seu arquivo de configuração do PHP (php.ini). Não sabe onde está seu arquivo php.ini? Utilize o comando <em>php &#8211;ini</em>. Procure por <em>include_path</em> dentro desse arquivo e adicione o caminho para o framework PHPUnit. <em>**A instalação via PEAR constuma adicionar esse caminho para você no php.ini. Confira o arquivo se for caso.</em></li>
</ul>


<p>Finalmente vamos ao nosso teste em si. Vamos testar se nossos métodos <em>get()</em> e <em>set()</em> estão realmente fazendo o que se espera. <em>Get()</em> tem de retornar o mesmo valor passado para <em>set()</em>. Para verificar isso vamos usar o método assertEquals do PHPUnit, veja o exemplo:</p>

title = "primeiros passos no phpunit"

/**
 * Classe Carro Teste
 **/
class CarroTeste extends PHPUnit_Framework_Testcase
{
    public function testeCor()
    {
        $carro = new Carro();
        $carro-&gt;setCor("Azul");

        $this-&gt;assertEquals("Azul", $carro-&gt;getCor());
    }
}
</pre>


<p>Criamos um método testeCor em nossa classe de testes.<br/>
Dentro dele instanciamos a classe carro e atribuímos para a propiedade cor o valor Azul.<br/>
O método AssertEquals do PHPUnit vai comparar se os dois parâmetros passados são iguais.</p>

<p>Vamos rodar nosso teste?<br/>
Em seu console execute o comando phpunit passando para ele o caminho da sua classe de testes. O resultado deve ser similar a esse:<br/>
<img class="alignleft size-full wp-image-563" title="Imagem2" src="../../assets/uploads/2012/10/Imagem2.png" alt="Rodando o primeiro teste" width="442" height="171" /><br style="clear: both;" /></p>

<p>Na imagem você percebe abaixo da linha de descrição da versão do PHPUnit um . (ponto). Em seguida uma descrição do tempo de execução e memória utilizada e abaixo um OK. Isso indica que nosso teste teve sucesso. O ponto que falamos acima indica que um teste teve sucesso, em caso de falha teremos um F no lugar do ponto. Para cada teste irá ser adicionado um <em>. ponto</em>ou um <em>F</em>.</p>

<p>Vamos forçar um erro no teste para ver o que acontece? Vamos trocar os parâmetros do nosso <em>AssertEquals</em> e dizer que estamos esperando o resultado <em>Amarelo</em> invés de <em>Azul</em>.</p>

title = "primeiros passos no phpunit"

/**
 * Classe Carro Teste
 **/
class CarroTeste extends PHPUnit_Framework_Testcase
{
    public function testeCor()
    {
        $carro = new Carro();
        $carro-&gt;setCor("Azul");

        $this-&gt;assertEquals("Amarelo", $carro-&gt;getCor());
    }
}
</pre>


<p>Rodando nosso teste agora temos a seguinte saída:<br/>
<img class="alignleft size-full wp-image-564" title="Imagem3" src="../../assets/uploads/2012/10/Imagem3.png" alt="Falha no PHPUnit" width="427" height="317" /><br style="clear: both;" /><br/>
No lugar do ponto anterior que indicava sucesso, temos agora um <em>F</em> indicando a falha. Junto a isso o PHPUnit nos traz detalhes da falha com o nome do teste que falhou, o que era esperado e o que foi retornado.</p>

<p>A ideia por trás do PHPUnit e suas funções é bem similar ao que foi demonstrado acima, com o detalhe que algumas funções podem ter mais parâmetros ou esperar tipos diferentes de dados. Que tal descobrir mais métodos do PHPUnit e criar novos testes? Visite o capítulo 4 do manual do PHPUnit e teste outras funções do framework. Segue o link para o manual: <a href="http://www.phpunit.de/manual/current/en/writing-tests-for-phpunit.html" title="PHPUnit Manual Cap4">http://www.phpunit.de/manual/current/en/writing-tests-for-phpunit.html</a>.</p>

<p>Grande Abraço!</p>
