+++
title = "Formatando CPF No SQL Com Expressões Regulares – RegexReplace"
date = "2010-05-21"
slug = "2010/formatando-cpf-no-sql-com-expressoes-regulares-regexreplace"
Categories = ['desenvolvimento', 'expressão regular']
+++

<p>Que as expressões regulares são bacanas e divertidas todo mundo já sabe.<br/>
Elas estão presentes em várias linguagens e no SQL Server não poderia ser diferente.</p>

<p>Se você é programador e ainda não sabe sobre as expressões regulares, não perca tempo.<br/>
Você precisa se emocionar com o uso delas em seus códigos.</p>

<p>Consulte os links abaixo para iniciar já esse aprendizado:<br/>
Wikipedia &#8211; <a href="http://pt.wikipedia.org/wiki/Express%C3%A3o_regular">http://pt.wikipedia.org/wiki/Express%C3%A3o_regular</a><br/>
Um excelente tutorial para começar do Rafael Jaques- <a href="http://www.phpit.com.br/artigos/entendendo-as-expressoes-regulares.phpit">http://www.phpit.com.br/artigos/entendendo-as-expressoes-regulares.phpit</a><br/>
Aurélio Marinho Jargas &#8211; O guru das expressões regulares &#8211; <a href="http://aurelio.net/er/">http://aurelio.net/er/</a></p>

<p>Certo mas e o SQL Server ? Vamos voltar para ele..</p>

<p>Em um post antigo eu mostro como fazer a formatação de campos como CPF direto pelo SQL.</p>

<p>Mas digamos que alguns campos do CPF estejam com formatação correta com pontuação e dígitos e outras não.<br/>
E ainda outras mais ou menos. Ex: <em>161.364.708-53, 16136470853, 161364708-53</em>.<br/>
Você tem um problema e nesse caso um SubString não iria funcionar corretamente.</p>

<p>Solução? RegexReplace. Vamos ver como usar isso.</p>

<!--more-->


<p>Primeiro vamos montar a expressão regular.<br/>
Vamos montar ela de maneira clara pensando apenas em como o CPF tem de ser exibido.<br/>
Não vamos pensar no cálculo do dígito verificador nem nada desse tipo.</p>

<p>Bom o que queremos ?</p>

<ul>
<li>3 números seguidos de um ponto. Vamos lembrar que esse ponto pode existir ou não. Não sabemos como o dado foi salvo no banco.</li>
<li>Mais 3 números seguidos de outro ponto. Novamente não sabemos se esse ponto estará presente ou não.</li>
<li>Precisamos agora de 3 números seguidos por um hífen, que também não temos certeza se estará lá ou não.</li>
<li>Para fechar, dois números.</li>
</ul>


<p>Legal! Já sabemos o que queremos vamos agora começar a brincadeira.</p>

<p>Não vou explicar aqui cada operador e caracter. Isso é demorado e também não é meu objetivo aqui.<br/>
Para começar com Expressões Regulares consulte os links que passei logo no início desse post.</p>

<p>Para trazer numerais na expressão regular usamos o seguinte</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
</pre>


<p>Mas isso vai me trazer apenas um numero, mas na verdade queremos 3 então fazemos da seguinte maneira</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
</pre>


<p>Se você quisesse 2 números, bastava substituir o 3 pelo 2.</p>

<p>Legal, para pegar os números já temos todas as armas na mão.<br/>
E agora os caracteres, o ponto e o hífen opcionais ??<br/>
Vamos lá&#8230;</p>

<p>O ponto é um operador em expressão regular e não é o operador que vai trazer o que queremos.<br/>
Nós precisamos de um ponto literalmente.<br/>
Para isso vamos escapar o ponto, assim como escapamos aspas ou caracteres especiais em programação.<br/>
Ficando assim:</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
/*Desconsidere umas das barras, acima
coloquei duas por conta do plugin de sintaxe do wordpress.*/
</pre>


<p>Agora para deixar isso opcional, basta colocar uma interrogação depois disso.</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
</pre>


<p>Para o hífen, não é obrigatório escapar pois ele não é um operador em expressões regulares.<br/>
Entretanto eu gosto de escapar ele. Para mim facilita a leitura.</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
</pre>


<p>Certo. Temos como pegar os numerais, como pegar hífen e pontos. Agora é juntar tudo.<br/>
Vamos usar parênteses para deixar tudo organizado e também para facilitar a nossa formatação mais para frente.</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
</pre>


<p>Repare que coloquei um circunflexo(<em>^</em>) no início da expressão e um cifrão(<em>$</em>) no final.<br/>
Isso indica que a String tem que ter um começo e um fim.<br/>
Caso não tivesse isso poderia haver qualquer caractere antes ou depois do CPF.</p>

<p>Vejamos por partes então:</p>

<ul>
<li>^ &#8211; Inicia a string</li>
<li>([0-9]{3}) &#8211; 3 números</li>
<li>.? &#8211; Um ponto, que pode ter ou não, por isso a interrogação.</li>
<li>([0-9]{3}) &#8211; Novamente 3 números</li>
<li>.? &#8211; Mais um ponto, que pode ter ou não.</li>
<li>([0-9]{3}) &#8211; Mais 3 números</li>
<li>-? &#8211; Um hífen, que pode ter ou não. Não é obrigatório o escape nele.</li>
<li>([0-9]{2}) &#8211; Dois números.</li>
<li>$ &#8211; Finaliza a String.</li>
</ul>


<p>Agora vamos para a segunda parte, o RegexReplace do Sql Server.</p>

<p>A função RegexReplace tem 3 parâmetros obrigatórios.<br/>
O primeiro é o seu campo, CPF nesse caso. O Segundo a expressão regular, e o terceiro o como queremos exibir.</p>

<p>Os dois primeiros parâmetros já temos.<br/>
Para o modo de exibição funciona da seguinte forma.<br/>
Quando usamos os parênteses em nossa expressão regular, elas se tornam variáveis que resgatamos com um cifrão e a ordem em que ela aparece na expressão. Então o primeiro parênteses seria o $1, o segundo o $2 e assim por diante.</p>

<p>Agora é só montar a função no Select.<br/>
Ficando assim.</p>

title = "formatando cpf no sql com expressoes regulares regexreplace"
'^([0-9]{3}).?([0-9]{3}).?([0-9]{3})-?([0-9]{2})',
'$1.$2.$3-$4')
</pre>


<p>Entre as variáveis você pode colocar os caracteres para exibição como pontos, hífens, underline e qualquer coisa que queira.</p>

<p>Reparem que coloquei o CPF no primeiro parâmetro da função formatado de maneira errada propositalmente.<br/>
Experimente modificar essa formatação, deixar só os números, só os pontos, enfim&#8230;<br/>
Modifique também a exibição da formatação para ver o funcionamento.</p>

<p>É isso galera.</p>

<p>Agradeço ao meu grande brother Anderson Orso por me mostrar possível aprender expressões regulares facilmente.</p>

<p>Espero que tenham curtido.<br/>
Qualquer dúvida só mandar.</p>

<p>Abraços!!</p>

<p><strong>UPDATE &#8211; 22 de maio</strong></p>

<p>Fala pessoal,<br/>
não me dei conta ontem que esqueci um detalhe importantíssimo de todo essa papo aqui.</p>

<p>O RegexReplace e outras funções similares não são nativas no SQL Server ao contrário de outros bancos de dados. Para ter isso disponível nos seus Selects, Updates e etc, você deve compilar um assembly .NET e subir para o banco.</p>

<p>O código para compilar você pode <a href="../../assets/UserDefinedFunctions.cs.rar" title="User Defined Functions">baixar aqui</a>.<br/>
Mais detalhes de como fazer e usar tudo isso você encontra <a href="http://justgeeks.blogspot.com/2008/08/adding-regular-expressions-regex-to-sql.html">nesse link</a>.</p>

<p>Abraço!</p>
