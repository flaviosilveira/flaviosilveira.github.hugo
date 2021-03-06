+++
title = "Initializr – Comece Seu Projeto HTML5 Em 15 Segundos!"
date = "2011-07-25"
slug = "2011/initializr-comece-seu-projeto-html5-em-15-segundos"
Categories = ['desenvolvimento', 'html', 'css', 'Javascript']
+++

<p>Salve pessoal!</p>

<p>Vocês já ouviram falar sobre o <a href="http://initializr.com/" title="Initializr!">Initializr!</a> ?</p>

<p>Ele é um gerador de código que ajuda você a começar seu projeto em HTML5. Ele é baseado no <a href="http://html5boilerplate.com/" title="oilerplate HTML5">Boilerplate</a> e foi criado por Jonathan Verrecchia (<a href="http://twitter.com/#!/verekia" title="Twitter Jonathan Verrecchia">@verekia</a>) com o objetivo de ampliar o uso do HTML5.</p>

<p>Em contato com o Jonathan, combinei com ele de traduzir a documentação oficial do Initializr do francês para o português, para ajudar a divulgar ainda mais essa tremenda ferramenta e quem sabe com isso ver o uso do HTML5 mais e mais em novos projetos.</p>

<p>Segue a tradução da documentação abaixo.<br/>
Você encontra a versão original em francês no seguinte link: <a href="http://www.html5-css3.fr/html5/initializr-generateur-template-html5-boilerplate" title="Documentação oficial Initializr Francês">http://www.html5-css3.fr/html5/initializr-generateur-template-html5-boilerplate</a>.</p>

<p>Conheça esses projetos e comece já a trabalhar com HTML5!<br/>
Grande Abraço!</p>

<h3>Initializr &#8211; Um gerador baseado nos templates Boilerplate HTML5</h3>

<p><img class="aligncenter size-full wp-image-371" title="logo-initializr" src="../../assets/uploads/2011/07/logo-initializr.png" alt="Initializr!" width="600" height="285" /></p>

<!--more-->


<p>Initializr permite a você gerar um template baseado no Boilerplate, montando um rascunho de um HTML5 funcional em segundos.</p>

<p>Você pode customizar seus templates como precisar, para evitar começar um projeto com um código muito pesado. Todo o processo do projeto de design e as opções disponíveis estão detalhadas neste artigo.</p>

<p>Se você está começando agora com HTML5 e quer ter uma geral do que tem por trás dessa tecnologia, eu recomendo que você leia uma introdução ao HTML5 antes de seguir em frente.</p>

<h3>Boilerplate HTML5</h3>

<p>Boilerplate é uma poderosa e confiável ferramenta de templates criada e mantida por Paul Irish (Google) e Divya Manian.</p>

<p>Boilerplate consiste de um grupo de arquivos HTML, CSS e JavaScript, usados para iniciar com o pé direito em um projeto HTML5.</p>

<p>Ele também inclui ferramentas muito úteis, como o Modernizr, JQuery, e um reset CSS.</p>

<p><img class="aligncenter size-full wp-image-372" title="logo-boilerplate" src="../../assets/uploads/2011/07/logo-boilerplate.png" alt="Boilerplate" width="600" height="75" /></p>

<p>Também inclui outras ferramentas não tão necessárias como um Profiling JQuery, Código Google Analytics, Funções Javascript para loggin,</p>

<p>um arquivo de configuração para Flash cross domain, Configuração IIS server e Nginx, Páginas de teste, scripts ANT… Bem, quando você for iniciar seu projeto com Boilerplate, você vai precisar de algum tempo para selecionar as partes que você quer e não quer no seu projeto.</p>

<h3>Initializr &#8211; Um Boilerplate leve e personalizável</h3>

<p>A proposta com o initializr é ter o Boilerplate sem essas ferramentas raramente usadas com HTML5 para poder começar um projeto rápido e tão confiável quanto o Boilerplate. O código gerado pelo Initializr é totalmente baseado no Boilerplate, que tem uma força inegável. Initializr oferece diferentes opções para customizar seu template. Aqui estão os detalhes:</p>

<h3>HTML / CSS</h3>

<p>Por padrão, o Boilerplate entrega a você uma página em branco. Initializr permite a você gerear um conteúdo inicial como base, para te ajudar a começar rapidamente. A página exemplo trás o tema do site da Initializr, com uma página estruturada com um clássico cabeçalho, um rodapé, um menu para navegação, um bloco lateral, e uma estrutura similar a um blog com alguns posts.</p>

<p><img class="aligncenter size-full wp-image-373" title="initializr-html5-template" src="../../assets/uploads/2011/07/initializr-html5-template.jpg" alt="Site Initializr" width="510" height="391" /></p>

<h3>Javascript</h3>

<p>O Boilerplate inclui a excelente biblioteca de Javascript jQuery. E no Initializr nós também encontramos essa biblioteca, disponível em forma minimizada ou não. Ou também o direito de não incluir ela, ou não incluir nenhum Javascript. Vamos atentar para um ponto: Estamos falando do seu Javascript. Nada no Modernizr ou no HTML5shiv vai garantir uma compatibilidade 100% com todos os navegadores. Então não esqueça de testar isso posteriormente.</p>

<p><img class="aligncenter size-full wp-image-374" title="jquery-logo" src="../../assets/uploads/2011/07/jquery-logo.png" alt="JQuery" width="366" height="90" /></p>

<h3>Compatibilidade</h3>

<h3>Html5Shiv</h3>

<p>Navegadores modernos suportam totalmente as novas tags do HTML5. Mas versões do Internet Explorer 8, e anteriores a ele, precisam de uma ajudinha para exibir essas novas tags, que por padrão não são reconhecidas. Esta pequena ajuda é chamada HTML5shiv. Ele é um pequeno arquivo javascript que vai permitir ao Internet Explorer reconhecer essas tags graças a uma função createElement():</p>

title = "initializr comece seu projeto html5 em 15 segundos"
</pre>


<p>Todos os novos itens são automaticamente criados antes do conteúdo da página ser completamente exibido. Isso torna obrigatório colocar o HTML5shiv no <em>Head</em> da sua página ao invés de colocar no rodapé, que é o recomendado para todos os outros javascripts.</p>

<h3>Modernizr</h3>

<p><img class="aligncenter size-full wp-image-375" title="modernizr-logo" src="../../assets/uploads/2011/07/modernizr-logo.png" alt="Modernizr" width="222" height="50" /></p>

<p>O Modernizr, é um sensor de suporte das funcionalidades HTML5 e CSS3, que inclui o HTML5shiv. Ele é um arquivo javascript que irá criar um objeto contendo propriedades modernizr para cada funcionalidade, indicando se ela funciona ou não no seu navegador.</p>

title = "initializr comece seu projeto html5 em 15 segundos"
  // A geolocalização é suportada
}
else {
  // A geolocalização não é suportada
}
</pre>


<p>Modernizr também adiciona classes CSS para o HTML, para que você possa facilmente indicar um estilo alternativo se certas propiedades CSS3 não forem suportadas.</p>

title = "initializr comece seu projeto html5 em 15 segundos"
  /* Backgrounds múltiplos são suportados */
}
.no-multiplebgs header {
  /* Backgrounds múltiplos não são suportados */
}
</pre>


<p>Modernizr é bem abrangente na detecção de suporte a HTML5 e CSS3, mas é importante entender que ele não adiciona nenhuma característica faltante (como faz o HTML5shiv em relação as tags). Ele é a ferramenta selecionada por padrão para compatibilidade do Initializr.</p>

<h3>A configuração do servidor</h3>

<p>O Initializr traz um arquivo de configuração para o servidor, também gerado pelo Boilerplate. Portanto é possível selecionar um arquivo .htaccess para servidores Apache, web.config para Microsoft IIS, ou nginx.conf para Servidores NGinx. É importante notar que por padrão, esses arquivos vão re-escrever a URL da página, removendo o &#8220;www&#8221; para montar URLs curtas.</p>

<p>Se você preferir manter o seu &#8220;www&#8221;, você pode remover as seguintes linhas no caso do .htaccess:</p>

title = "initializr comece seu projeto html5 em 15 segundos"
  RewriteEngine On
  RewriteCond %{HTTPS} !=on
  RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
  RewriteRule ^(.*)$ http://%1/$1 [R=301,L]
&lt;/IfModule&gt;
</pre>


<p><img class="aligncenter size-full wp-image-376" title="server" src="../../assets/uploads/2011/07/server.png" alt="" width="256" height="256" /></p>

<h3>É apenas um clique no botão!</h3>

<p>Após fazer suas escolhas com relação a configuração, um simples clique no botão Download! fará o download de seus arquivos.</p>

<p><img class="aligncenter size-full wp-image-377" title="initializr-download" src="../../assets/uploads/2011/07/initializr-download.png" alt="" width="400" height="157" /></p>

<p>Se você manter as configurações padrão, você terá uma estrutura de projeto completa e pronta para uso, como a mostrada abaixo:</p>

<p><img class="aligncenter size-full wp-image-378" title="html5-initializr-structure" src="../../assets/uploads/2011/07/html5-initializr-structure.png" alt="" width="224" height="250" /></p>

<p>Uma rápida olhada no arquivo index.html e você pode ver que o código traz muita coisa do Boilerplate:</p>

title = "initializr comece seu projeto html5 em 15 segundos"
&lt;!--[if lt IE 7 ]&gt; &lt;html lang="en" class="no-js ie6"&gt; &lt;![endif]--&gt;
&lt;!--[if IE 7 ]&gt;    &lt;html lang="en" class="no-js ie7"&gt; &lt;![endif]--&gt;
&lt;!--[if IE 8 ]&gt;    &lt;html lang="en" class="no-js ie8"&gt; &lt;![endif]--&gt;
&lt;!--[if IE 9 ]&gt;    &lt;html lang="en" class="no-js ie9"&gt; &lt;![endif]--&gt;
&lt;!--[if (gt IE 9)|!(IE)]&gt;&lt;!--&gt; &lt;html lang="en" class="no-js"&gt; &lt;!--&lt;![endif]--&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;

  &lt;title&gt;Your website name&lt;/title&gt;

  &lt;meta name="description" content=""&gt;
  &lt;meta name="author" content=""&gt;

  &lt;meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;

  &lt;link rel="shortcut icon" href="favicon.ico"&gt;
  &lt;link rel="apple-touch-icon" href="apple-touch-icon.png"&gt;

  &lt;link rel="stylesheet" href="css/style.css?v=2"&gt;

  &lt;script src="js/libs/modernizr-1.6.min.js"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;!-- Código da página exemplo do Initializr --&gt;

  &lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"&gt;&lt;/script&gt;
  &lt;script&gt;!window.jQuery && document.write(unescape('%3Cscript src="js/libs/jquery-1.4.4.min.js"%3E%3C/script%3E'))&lt;/script&gt;
  &lt;script src="js/script.js"&gt;&lt;/script&gt;
  &lt;!--[if lt IE 7 ]&gt;
  &lt;script src="js/libs/dd_belatedpng.js"&gt;&lt;/script&gt;
  &lt;script&gt; DD_belatedPNG.fix('img, .png_bg');&lt;/script&gt;
  &lt;![endif]--&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


<p>O arquivo style.css traz em torno de 200 linhas, os primeiros 3 quartos disso um CSS Reset. Se você estiver procurando onde colocar os seus estilos no meio desse código CSS, role o arquivo para baixo até você encontrar o seguinte comentário:</p>

title = "initializr comece seu projeto html5 em 15 segundos"
    // ========================================== \\
   ||                                              ||
   ||               Your styles !                  ||
   ||                                              ||
    \\ ========================================== //
*/
</pre>


<p>Por último, o arquivo script.js contém um simples teste para ver se a biblioteca JQuery está sendo carregada. Nesse arquivo você pode escrever seu código JavaScript.</p>

<h3>TODO.txt</h3>

<p>Um arquivo todo.txt também é incluído para te mostrar que tarefas você tem de fazer para começar seu projeto e como usar alguns truques de HTML5 presentes no Boilerplate. Por exemplo, você e lembrado para não esquecer de substituir a linguagem se sua página não estiver em inglês, ou para criar uma  página 404.html no seu arquivo se configuração do servidor para fazer um redirecionamento em erros 404.</p>

<p><img class="aligncenter size-full wp-image-379" title="initializr-todo" src="../../assets/uploads/2011/07/initializr-todo.png" alt="" width="463" height="110" /></p>

<h3>Indo mais longe</h3>

<p>A versão do Boilerplate que vem no Initializr é mais leve que a original. Se você precisa de um entendimento mais profundo do template ou de informações mais detalhadas de todos os arquivos, você pode ver a explicação oficial do Boilerplate em um vídeo feito por Paul Irish em inglês:</p>

<p>Eu também lhe convido a visitar o <a href="http://html5boilerplate.com/" title="Boilerplate">site oficial do Boilerplate</a>, onde você vai encontrar algumas dicas para melhorar seu site , dicas de compatibilidade e performance.</p>
