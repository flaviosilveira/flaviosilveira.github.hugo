+++
title = "Habilitando Layouts No CodeIgniter (Template Engine) – Parte 2"
date = "2010-02-18"
slug = "2010/habilitando-layouts-no-codeigniter-template-engine-2"
Categories = ['desenvolvimento', 'php']
+++

<div id="atencao">
  <p>
    Atenção!! Este artigo foi escrito em cima da versão 1 do Codeigniter. Para detalhes de como usar com a versão 2 do framework <a href="http://flaviosilveira.com/2011/codeigniter-2-templates-e-layouts">clique aqui</a>.
  </p>
</div>


<p>Continuando a parte 1 deste post.<br/>
Se você perdeu a primeira parte <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-1">clique aqui para ler a primeira parte</a>.</p>

<p><strong>5 &#8211; Construindo sua View</strong></p>

<p>Sua View deve ser feita normalmente, como voce já está acostumado a fazer, com o nome que você colocaria normalmente.<br/>
Apenas com o conteúdo que muda de uma página para outra.</p>

<p>O HTML que você colocar aqui na View irá substituir a variável <em>{content_for_layout}</em> que definimos no layout acima.<br/>
Vou colocar nessa nossa view de exemplo apenas um título e um parágrafo para demonstrar.<br/>
Ficando assim:</p>

title = "habilitando layouts no codeigniter template engine 2"

&lt;p&gt;Paragrafo teste teste teste teste.&lt;/p&gt;

</pre>


<p>Chamei essa view de <em>home.php</em>.</p>

<p><strong>6 &#8211; Desenvolvendo a Classe</strong></p>

<p>Quando definimos nosso Hook no passo 2, setamos que a pasta onde ficaria nossa classe seria a pasta hooks que vem por padrão no projeto do CodeIgniter.</p>

<p>Vamos criar nossa classe dentro dessa pasta, e, com o nome que também especificamos na definição do Hook que foi Layout.php<br/>
Se você não seguiu o exemplo, faça suas devidas adaptações.</p>

<p>A classe é um pouco extensa, leia com atenção.<br/>
Para ajudar ela está com os comentários do próprio <a href="http://www.mozartpetter.com/pt/">Mozart Petter</a>.</p>

<!--more-->




title = "habilitando layouts no codeigniter template engine 2"
&lt;?php if (!defined('BASEPATH')) exit('No direct script access allowed');

/**
 * Layout Class
 *
 * @package hooks
 * @description Implementa as views do tipo layout no framework.
 */

class Layout
{

public $base_url;

/**
* Metodo que executa as implementacoes.
* Este metodo e chamado atraves do arquivo hooks.php
* na pasta config.
*
* @return
*/
public function init()
{
// Instancia do CI.
$CI =& get_instance();

// Definindo o base_url.
$this-&gt;base_url = $CI-&gt;config-&gt;slash_item('base_url');

// Pegando a saida que o CI gera normalmente.
$output = $CI-&gt;output-&gt;get_output();

// Pegando o valor de title, se definido no controller.
$title = (isset($CI-&gt;title)) ? $CI-&gt;title : '';

// Links CSS definidos no controlador.
$css = (isset($CI-&gt;css)) ? $this-&gt;createCSSLinks($CI-&gt;css) : '';

// Links JS definidos no controlador.
$js = (isset($CI-&gt;js)) ? $this-&gt;createJSLinks($CI-&gt;js) : '';

// Se layout estiver definido e a regexp nao bater.
if (isset($CI-&gt;layout) && !preg_match('/(.+).php$/', $CI-&gt;layout))
{
$CI-&gt;layout .= '.php';
}
else
{
$CI-&gt;layout = 'default.php';
}

// Definindo caminho completo do layout.
$layout = LAYOUTPATH . $CI-&gt;layout;

// Se o layout for diferente do default, e o arquivo nao existir.
if ($CI-&gt;layout !== 'default.php' && !file_exists($layout))
{
// Exibe a mensagem, se o layout for diferente de '.php'.
}

// Se o arquivo layout existir.
if (file_exists($layout))
{
// Carrega o conteudo do  arquivo.
$layout = $CI-&gt;load-&gt;file($layout, true);

// Substitui o texto {content_for_layout} pelo valor de output em layout.
$view = str_replace('{content_for_layout}', $output, $layout);

// Substitui o texto {title_for_layout} pelo valor de title em view.
$view = str_replace('{title_for_layout}', $title, $view);

// Links CSS.
$view = str_replace('{css_for_layout}', $css, $view);

// Links JS.
$view = str_replace('{js_for_layout}', $js, $view);
}
else
{
$view = $output;
}

echo $view;
}

/**
* Gera os links CSS utilizados no layout.
*
* @return void
*/
private function createCSSLinks($links)
{
$html = "";

for ($i = 0; $i &lt; count($links); $i++)
{
$html .= "&lt;link rel='stylesheet' type='text/css' href='" . $this-&gt;base_url . CSSPATH . $links[$i] . ".css' media='screen' /&gt;n";
}

return $html;

}

/**
* Gera os links JS utilizados no layout.
*
* @return void
*/
private function createJSLinks($links)
{
$html = "";

for ($i = 0; $i &lt; count($links); $i++)
{
$html .= "&lt;script type='text/javascript' src='" . $this-&gt;base_url . JSPATH . $links[$i] . ".js'&gt;&lt;/script&gt; n";
}

return $html;
}

}
</pre>


<p><strong>7 &#8211; Fazendo as chamadas no Controller</strong></p>

<p>Chegou o momento final!<br/>
É hora de juntar tudo isso que fizemos até agora.</p>

<p>A construção do seu controller é normal, como você está acostumado, mas temos que inserir algumas variáveis globais nele.</p>

<ul>
<li>Uma para o Layout default do controller, para que você não precise fazer a mesma definição várias vezes.</li>
<li>Uma para o título, onde você pode definir um default para todos as páginas que vão surgir desse controller mas, o interessante é estar um título por página.</li>
<li>Outra para guardar um Array dos CSS&#8217;s que você vai usar na página.</li>
<li>E por último, outro Array para guardar os JavaScripts que você vai usar na página.</li>
</ul>


<p>Vejamos como fica.<br/>
Acompanhe pelos comentários.</p>

title = "habilitando layouts no codeigniter template engine 2"

/**
 *
 */
class Principal extends Controller
{

/**
* Layout default utilizado pelo controlador.
*/
public $layout = 'default';

/**
* Titulo default.
*/
public $title = '::: Titulo default :::';

/**
* Definindo os css default.
*/
public $css = array('default');

/**
* Carregando os js default.
*/
public $js = array('home');

/**
* Construtora.
* @return
*/
function Principal()
{

parent::Controller();

}

// Metodoo index
function index()
{
// Carregando a view.
$this-&gt;load-&gt;view('home');
}

// Metodo teste
function teste()
{
//Title
$this-&gt;title = '::: TESTE Título :::';

//CSS
$this-&gt;css = array('test');

//JS
$this-&gt;js = array('jquery');

// Carregando a View
$this-&gt;load-&gt;view('teste');
}

}

?&gt;

</pre>


<p>Vamos reparar no seguinte.<br/>
Há dois métodos nesse controller que vão chamar páginas diferentes, o index e o teste.</p>

<p>Para o index não definimos nada de Layout, Titulo, CSS ou JS.<br/>
Ou seja, vai vir tudo do valor default que usamos quando definimos as variáveis globais.</p>

<p>Já no método teste, por algum motivo precisamos de um CSS, um JS e um Título diferente.<br/>
Então redefinimos esses valores no nosso método com o que precisamos.</p>

<p>A gente poderia ter definido um outro Layout caso tivesse a necessidade, da mesma forma com que fiz com esses valores.<br/>
Aí, claro, teria que criar um outro Layout na pasta layouts.</p>

<hr />

<p><span id="explicacao"> </span><br/>
<strong>UPDATE 20 DE NOVEMBRO DE 2010</strong><br/>
Detalhe importante observado pelo <a href="http://diegofelix.com.br/">Diego Felix</a> (<a href="http://twitter.com/diegofelix">@diegofelix</a>), que comentou esse detalhe abaixo nos comentários, no dia 16 de setembro desse mesmo ano.</p>

<p>&nbsp;</p>

<p>Eu tenho como costume em meus projetos com CI, retirar a pasta system no qual ele vem por padrão.<br/>
Faço então a alteração da variável <em>$system_folder</em> no arquivo de configuração e tudo segue sem problemas.</p>

<p>Exceto esse tutorial, que não leva em consideração essa pasta system.<br/>
Você tem duas opções para consertar isso:</p>

<p><strong>Primeiro:</strong><br/>
No local onde são definidas as variáveis contantes, adicionar sua pasta system antes de <em>$application_folder</em>.<br/>
Exemplo: <em>define(&#8216;LAYOUTPATH&#8217;, &#8216;system/&#8217; . $application_folder.&#8217;/layouts/&#8217;);</em></p>

<p>Particularmente acho essa solução acima atrasada, por deixar o projeto estático.<br/>
Se ocorrer de você alterar a pasta system, terá que alterar nesse local também. Chato.</p>

<p><strong>Segundo:</strong><br/>
Seguindo essa linha de raciocínio, de não deixar o projeto estático, prefiro fazer o seguinte:<br/>
No local onde são definidas as variáveis constantes, adicionar a variável <em>$system_folder</em>.<br/>
Exemplo: <em>define(&#8216;LAYOUTPATH&#8217;, $system_folder . &#8216;/&#8217; . $application_folder.&#8217;/layouts/&#8217;);</em></p>

<p>Mas há um detalhe.<br/>
No arquivo <em>index.php</em>, em torno da linha 53, é adicionado a variável <em>$system_folder</em> o seu caminho completo do servidor. Isso, claro, vai gerar problemas para o projeto.<br/>
O que eu faço então é pegar as variáveis constantes que usam a pasta system, e jogar antes desse bloco.<br/>
Se você seguir pelo projeto exemplo, verá que as coloquei logo depois do comentário <em>&#8220;END OF USER CONFIGURABLE SETTINGS&#8221;</em>.</p>

<p>Feito isso, caso você altera sua pasta system, basta alterar no local de sempre para o projeto continuar funcionando.</p>

<hr />

<p>Pessoal é isso!<br/>
Fazia tempo que queria escrever sobre isso, espero que ajude a galera por aí.<br/>
Dúvidas podem mandar sem problemas, vou responder no que estiver a meu alcance.</p>

<p>Se você teve dificuldades, <a href="../../assets/uploads/2010/02/projetoExemplo.zip" title="Baixar projeto Exemplo">baixe o projeto pronto aqui</a> e dê uma olhada mais de perto.</p>

<p>Agradeço novamente ao <a href="http://www.mozartpetter.com/pt/" title="Mozart Petter Developer">Mozart Petter</a>, grande Brother, que implementou essa solução que uso até hoje em meus projetos. E, como sempre, também ao pessoal que garante minhas 30 visitas diárias, Valeu!</p>

<p>É isso pessoal.<br/>
Até a próxima!!!</p>
