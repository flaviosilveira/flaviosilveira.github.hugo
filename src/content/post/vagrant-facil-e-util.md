+++
title = "Vagrant: Fácil E útil"
date = "2012-11-07"
slug = "2012/vagrant-facil-e-util"
Categories = ['desenvolvimento']
+++

<p>Salve pessoal!</p>

<p>Hoje eu quero passar uma dica para fazer você parar com aquela desculpa &#8220;Na minha máquina tá funcionando&#8221;. Para isso vou apresentar para vocês o Vagrant <a href="http://vagrantup.com/">http://vagrantup.com/</a>.</p>

<p>O Vagrant é uma ferramenta que te ajuda na criação da infraestrutura para o seu projeto, usando para isso uma máquina virtual. Mas aí você pensa: &#8220;Uma máquina virtual para cada projeto?? Isso vai dar trabalho&#8221;. A grande jogada é que o Vagrant deixa muita coisa invísivel, deixando com que você se preocupe apenas com seu código. É uma máquina virtual reduzida e portável facilmente. Para cada projeto você pode deixar um ambiente diferente rodando, um com PHP 4, outro com PHP 5, um em Debian outro em CentOS, você escolhe.</p>

<!--more-->


<p><strong><br/>
Instalação</strong></p>

<p>Para criar suas máquinas vituais o Vagrant precisa do Virtual Box, um cliente de máquinas virtuais da Oracle bastante conhecido. Basta instalar! Você não precisa deixar o programa aberto para usar o Vagrant. Você pode fazer o download do Virtual box no seguinte link <a href="https://www.virtualbox.org/wiki/Downloads">https://www.virtualbox.org/wiki/Downloads</a>.</p>

<p>Instalado o Virtual Box, faça o download do Vagrant e o instale. Procure pela versão do seu sistema operacional no seguinte link <a href="http://downloads.vagrantup.com/">http://downloads.vagrantup.com/</a>.</p>

<p><strong><br/>
Configurando e rodando</strong></p>

<p>Outra coisa que o Vagrant utiliza para criar suas máquinas virtuais são Boxes, ou no singular uma Box. Essa Box funciona como uma imagem, uma iso do sistema operacional que você quer instalar. Então antes de qualquer coisa vamos adicionar uma box, para que você a tenha disponível para criar seu primeiro teste com vagrant.</p>

<p>Abra o console do seu sistema operacional, seja o cmd no windows ou o terminal no linux ou mac e entre com o comando</p>

title = "vagrant facil e util"
</pre>


<p>Essa é a box de exemplo que o Quick Start do Vagrant traz para a gente, onde o primeiro parâmetro que vem após add é o nome que estamos dando a nossa box e o segundo o caminho da onde faremos o download. Esse comando vai trazer uma Box do Ubuntu Lucid. Aqui eu recomendo que caso esteja começando com o Vagrant faça um teste usando essa box, mas caso queira avançar um pouco mais, aqui está uma lista de algumas boxes disponíveis por aí <a href="http://www.vagrantbox.es/">http://www.vagrantbox.es/</a>.</p>

<p>Box preparada, que tal colocar nosso ambiente para rodar?</p>

<p>Crie uma pasta para o seu projeto no seu ambiente de trabalho e acesse ela via console.<br/>
Entre com o seguinte comando:</p>

title = "vagrant facil e util"
</pre>


<p>Caso tenha usado outro nome para a sua box no passo anterior, substitua no lugar de lucid32 no comando acima.</p>

<p>Como o próprio comando se explica, ele prepara uma configuração inicial para você usando um arquivo que ele cria em seu diretório chamada Vagrantfile. Dentro desse arquivo existe algumas configurações como a box a ser usada entre outros.</p>

<p>Agora é só subir o ambiente.</p>

title = "vagrant facil e util"
</pre>


<p>Ao subir o ambiente o vagrant irá realmente criar sua máquina virtual e configurar as coisas para você. Acompanhe as saídas dos comandos para detalhes.</p>

<p>Tudo pronto!</p>

<p><strong><br/>
Testando</strong></p>

<p>Chegou a hora da verdade. Crie um arquivo html com qualquer conteúdo dentro da pasta do seu projeto.</p>

<p>Por exemplo vamos criar um arquivo chamado teste.html com o seguinte conteúdo</p>

title = "vagrant facil e util"
</pre>


<p>Agora acesse via browser a pasta do seu projeto e o arquivo que criou.<br/>
<a href="../../assets/uploads/2012/11/imagem1.png"><img class="alignleft size-full wp-image-587" title="Vagrant - Rodando" src="../../assets/uploads/2012/11/imagem1.png" alt="Vagrant - Rodando" width="394" height="101" /></a><br/>
<br style="clear: both;" /><br/>
Esse HTML está dentro da sua máquina virtual e você está rodando a partir do seu localhost. Muito bom não?</p>

<p>Alguns pontos:</p>

<ul>
<li>Note que você nem abriu essa máquina virtual para trabalhar dentro dela. Você está trabalhando como se ela fosse uma pasta local em sua máquina, essa é a beleza da coisa. Você pode deixar isso melhor organizado usando a opção share_folder do arquivo de configuração Vagrantfile</li>
<li>Mostrei aqui um teste com HTML como também é mostrado no Quick Start do Vagrant, mas você pode instalar o que quiser dentro da sua máquina virtual seja PHP, Java, Python e rodar o que bem entender. Apenas atente para fazer direcionamento das portas para que isso funcione de acordo. Veja a opção forward_port do arquivo de configuração Vagrantfile</li>
<li>Detalhes com todas as opções disponíveis para o Vagrantfile você encontra na documentação oficial <a href="http://vagrantup.com/v1/docs/vagrantfile.html">http://vagrantup.com/v1/docs/vagrantfile.html</a></li>
</ul>


<p><strong><br/>
SSH</strong></p>

<p>E que tal um acesso SSH na sua máquina virtual?<br/>
Sim, o Vagrant te traz isso!<br/>
Se você está no Mac ou Unix apenas entre com o comando abaixo e você está dentro.</p>

title = "vagrant facil e util"
</pre>


<p>Para usuários do windows será necessário o uso do puttygen, putty e algumas configurações em cima deles. Nada muito complicado para quem já trabalha com SSH no seu dia a dia.</p>

<p>Após acesar o ssh via vagrant, você sai no seu home <em>/home/vagrant</em>.<br/>
Os arquivos que você criou dentro da pasta do seu projeto podem ser encontrados em <em>/vagrant</em>.</p>

<p><strong><br/>
Distribuindo seu ambiente</strong></p>

<p>Está trabalhando com alguém em um projeto? Que tal enviar esse ambiente que você criou no Vagrant para essa pessoa, para que vocês trabalhem em cima do mesmo ambiente?</p>

<p>Para isso basta criar um pacote da sua máquina virtual com o seguinte comando</p>

title = "vagrant facil e util"
</pre>


<p>Ao final do processo você terá um arquivo chamado package.box.<br/>
Para que alguém ou você mesmo o utilize, basta seguir os passos apresentados aqui como se esse arquivo fosse uma box que você vai fazer o download. Sem mais.</p>

<p><strong><br/>
Resumo</strong></p>

<p>Apresentei aqui uma geral sobre o Vagrant, porque ele é útil, porque é interessante usá-lo e etc. Fizemos um exemplo e vimos como distribuir esse ambiente com mais pessoas. Cobri aqui o básico dessa sensacional ferramenta para você configurar o ambiente de seus projetos individualmente.</p>

<p>Você pode ir mais além e criar várias máquinas virtuais que se comunicam entre si e outros. Para isso leia a documentação <a href="http://vagrantup.com/v1/docs/index.html">http://vagrantup.com/v1/docs/index.html</a> e se intere do que mais o Vagrant pode fazer por você.</p>

<p>É isso pessoal.<br/>
Abraços.</p>
