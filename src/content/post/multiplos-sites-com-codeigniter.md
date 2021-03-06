+++
title = "Múltiplos Sites Com Codeigniter"
date = "2008-12-19"
slug = "2008/alterando-configuracao-do-codeigniter"
Categories = ['desenvolvimento', 'php']
+++

<p>Entrei em uma empresa recentemente, e acredito que conquistei a vaga por já ter trabalhado com CodeIgniter antes. Pra quem não sabe o <a href="http://codeigniter.com/">CodeIgniter</a> é um framework PHP com estrutura em <a href="http://pt.wikipedia.org/wiki/MVC">MVC</a>, o que deixa tudo mais organizado. E foi a ferramenta escolhida pela empresa para organizar os seus bagunçados projetos.</p>

<p>Apesar de já ter trabalhado com CodeIgniter antes, nunca havia me envolvido tanto, entrado em suas configurações principais e etc. Me limitava ao superficial para fazer funcionar. Controler, consulta no banco pelo Model, chama a view para mostrar o conteúdo e fechou. No máximo chamar uma library.</p>

<p>Porém pediram para mim e meu amigo <a href="http://twitter.com/RonieNeubauer">Ronie</a>, que já tinhamos experiência com a ferramenta, para deixar ela configurada para múltiplos sites. Já tinhamos visto isso antes. Vamos lá! Pesquisar no segundo cérebro (<a href="http://www.google.com">Google</a>)!</p>

<p>O site oficial propõe duas maneiras para se trabalhar com múltiplos sites em CodeIgniter. A primeira seria criando as pastas principais dos sites dentro de Application (Application é onde fica a estrutura do site). Funciona como se cada pasta dessa, fosse um application. Logo, você deve replicar o conteúdo da pasta application que vem por padrão no CodeIgniter para cada site que for ter, renomeando para um nome de acordo (No exemplo abaixo a pasta site1 e a pasta site2).<br/>
<img class="alignnone size-full wp-image-54" title="ci1" src="../../assets/uploads/2009/01/ci1.jpg" alt="ci1" width="148" height="139" /><br/>
<br style='clear: both' /></p>

<!--more-->


<p>A segunda forma é bem similar. Você tiraria as pastas principais de dentro do Application, trazendo para a mesma raiz do system(system é onde fica o core do codeigniter).<br/>
<img class="alignnone size-full wp-image-55" title="ci2" src="../../assets/uploads/2009/01/ci2.jpg" alt="ci2" width="126" height="119" /><br/>
<br style='clear: both' /></p>

<p>Outro passo que a documentação pede, para as duas formas, é replicar o arquivo &#8220;index.php&#8221; (Nos exemplos acima representados por site1.php e site2.php), que vem por padrão na raiz do codeigniter, junto com a pasta system e a pasta application.<br/>
Deve se fazer essa réplica, para cada site/pasta principal, e editar a variável $application_folder, que devem conter o caminho para sua respectiva pasta principal. Nos exemplos do Wiki ele renomeia cada index para sua pasta do site, para ter como acessar cada site. que ficaria: <strong><em><a href="http://www.seudominio.com/site1***">http://www.seudominio.com/site1***</a> ou </em></strong><a href="http://www.seudominio.com/site2***">http://www.seudominio.com/site2***</a></p>

<p>Porém, precisavamos de outra coisa.<br/>
Foi pedido que separacemos a pasta dos arquivos css&#8217;s para fora da aplicação do CodeIgniter. Para que apenas o pessoal da programação tivesse acesso a isso. O pessoal do Layout (do CSS) não interferiria na Aplicação.</p>

<p>Depois de algumas idéias, rodando o tal arquivo &#8220;index.php&#8221; veio toda a solução. Simples !</p>

<p>Nesse arquivo é setado o endereço da pasta System, e, como já vimos antes, da pasta Application. Putz.. Ai fica tudo muito fácil.</p>

<p>Jogamos uma pasta system na raiz do servidor, e renomeamos para CI.</p>

<p>Para cada site, fizemos uma pasta principal (para onde o domínio é apontado). Dentro dessa pasta principal colocamos a Réplica do Application, com o nome de &#8220;app&#8221;, Uma pasta &#8220;www&#8221;, para os CSS&#8217;s e Imagens de Layout, e por último uma pasta &#8220;includes&#8221;, para Uploads do usuário como fotos de notícias, PDF&#8217;s e etc. Ficou como tento demonstrar abaixo:</p>

<p><img class="alignnone size-full wp-image-56" title="ci3" src="../../assets/uploads/2009/01/ci3.jpg" alt="ci3" width="169" height="210" /><br/>
<br style="clear: both" /></p>

<p>Não queriamos deixar as cópias dos &#8220;index.php&#8221; soltas para fora de tudo, como o Wiki deixa a entender. Colocamos dentro de cada Pasta Principal. O que facilitou no sentido da URL, pois geralmente quando você entra em uma pasta pelo browser, ele procura por um &#8220;index&#8221; não é mesmo ? Então para acessar cada site, é só entrar na pasta principal. Ele pega o index.php, e faz todo o Trabalho <em>Hard Mode.</em>**</p>

<p><em><em>Nossa URL então, ficou apenas com o dominio do site</em>, </em>que é apontado para pasta do site. Como cada pasta tem o index, fechou.*<br/>
*</p>

<p>Na edição dos arquivos &#8220;index.php&#8221;, setamos a variável $system_folder da seguinte maneira:</p>

title = "multiplos sites com codeigniter"

</pre>


<p>Dois pontos para quem não sabe, volta um diretório. e CI, foi o nome que demos para nossa pasta system. Resumindo: <em>Volta um e entra na pasta CI</em></p>

<p>Apontamos a variável $application_folder para nossa réplica da pasta Application, que é a pasta app no exemplo acima.</p>

title = "multiplos sites com codeigniter"

</pre>


<p>E isso resolve tudo. Ou seja, Podemos fazer a organização do nosso projeto para múltiplos sites como achar melhor. É só editar o cara que manda em tudo, que é o arquivo &#8220;index.php&#8221;, da maneira correta.</p>

<p>Confira um exemplo passo a passo, <a href="http://flaviosilveira.com/2009/multiplos-sites-com-codeigniter-exemplo-pratico/">clicando aqui.</a></p>

<p>Em breve mais posts sobre CodeIgniter. Valeu !!!</p>
