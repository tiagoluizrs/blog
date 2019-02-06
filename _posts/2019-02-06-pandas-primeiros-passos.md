---
title: "Seus primeiros passos como Data Scientist: Introdução ao Pandas!"
excerpt_separator: "<!--more-->"
categories:
  - Programação
tags:
  - Pandas
  - Python
  - Report
  - Relatório
---


<p id="1f73" class="graf graf--p graf--hasDropCapModel graf--hasDropCap graf-after--figure"><span class="graf-dropCap">A</span><em class="markup--em markup--p-em">lém desses animaizinhos simpáticos</em>,&nbsp;<a class="markup--anchor markup--p-anchor" href="https://pandas.pydata.org/" target="_blank" rel="noopener nofollow" data-href="https://pandas.pydata.org/"><strong class="markup--strong markup--p-strong">Pandas</strong></a><strong class="markup--strong markup--p-strong">&nbsp;</strong>também é uma biblioteca&nbsp;<strong class="markup--strong markup--p-strong">Python.&nbsp;</strong>Ela fornece ferramentas de análise de dados e estruturas de dados de alta performance e&nbsp;<strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">fáceis&nbsp;</em></strong><em class="markup--em markup--p-em">de usar</em>.</p>
<p id="76fb" class="graf graf--p graf-after--p"><em class="markup--em markup--p-em">Por ser a principal e mais completa biblioteca para estes objetivos,&nbsp;</em><strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">Pandas&nbsp;</em></strong><em class="markup--em markup--p-em">é fundamental para Análise de Dados.</em></p>

<figure id="4ffb" class="graf graf--figure graf-after--p">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*71Typ4wtCLNeetb81EgZ7Q.png" data-width="582" data-height="140" data-scroll="native"><canvas class="progressiveMedia-canvas js-progressiveMedia-canvas" width="75" height="17"><img class="alignnone size-full wp-image-2402 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/1_71Typ4wtCLNeetb81EgZ7Q-min.png" alt="" width="582" height="140"></canvas><img class="size-full wp-image-2402 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/1_71Typ4wtCLNeetb81EgZ7Q-min.png" alt="" width="582" height="140"></div>
</div></figure>
<h3 id="e700" class="graf graf--h3 graf-after--figure">Disclaimer</h3>
<p id="40d9" class="graf graf--p graf-after--h3">Esse guia foi escrito como uma alternativa em português às introduções já existentes e à&nbsp;<a class="markup--anchor markup--p-anchor" href="http://pandas.pydata.org/pandas-docs/stable/10min.html" target="_blank" rel="noopener nofollow" data-href="http://pandas.pydata.org/pandas-docs/stable/10min.html">introdução de 10 minutos apresentada na documentação oficial</a>, e tem por objetivo fornecer de forma&nbsp;<strong class="markup--strong markup--p-strong">enxuta e simplificada</strong>&nbsp;uma apresentação básica às principais ferramentas fornecidas pelo&nbsp;<strong class="markup--strong markup--p-strong">pandas</strong>, cobrindo:</p>

<ul class="postList">
 	<li id="6542" class="graf graf--li graf-after--p"><strong class="markup--strong markup--li-strong">Manipulação,</strong></li>
 	<li id="e827" class="graf graf--li graf-after--li"><strong class="markup--strong markup--li-strong">Leitura,</strong></li>
 	<li id="0245" class="graf graf--li graf-after--li"><strong class="markup--strong markup--li-strong">Visualização</strong>&nbsp;<strong class="markup--strong markup--li-strong">de dados</strong>.</li>
</ul>
<p id="2c41" class="graf graf--p graf-after--li">A introdução pressupõe apenas conhecimento básico em&nbsp;<strong class="markup--strong markup--p-strong">Python</strong>.</p>
<p id="209f" class="graf graf--p graf-after--p">Há&nbsp;<strong class="markup--strong markup--p-strong">duas</strong>outras excelentes opções de acessar esta introdução:</p>

<ol class="postList">
 	<li id="b8c0" class="graf graf--li graf-after--p">Você pode acessar o&nbsp;<a class="markup--anchor markup--li-anchor" href="https://mybinder.org/v2/gh/mvinoba/notebooks-for-binder/master?filepath=postagem.ipynb" target="_blank" rel="nofollow noopener" data-href="https://mybinder.org/v2/gh/mvinoba/notebooks-for-binder/master?filepath=postagem.ipynb">MyBinder deste arquivo</a>, que cria um ambiente interativo Jupyter rodando Python com todas as dependências necessárias automaticamente, onde você pode testar e executar por si mesmo as linhas de código deste tutorial direto do seu navegador sem precisar configurar nada.</li>
 	<li id="bab0" class="graf graf--li graf-after--li">Você pode acessar o&nbsp;<a class="markup--anchor markup--li-anchor" href="http://nbviewer.jupyter.org/github/mvinoba/notebooks-for-binder/blob/master/postagem.ipynb" target="_blank" rel="nofollow noopener" data-href="http://nbviewer.jupyter.org/github/mvinoba/notebooks-for-binder/blob/master/postagem.ipynb">notebook viewer</a>&nbsp;deste arquivo, que fornece syntax highlighting e formatação mais padronizada com o que se está acostumado num notebook Jupyter.</li>
</ol>
<h3 id="3bb3" class="graf graf--h3 graf-after--li"><strong class="markup--strong markup--h3-strong">Mãos à&nbsp;obra!</strong></h3>
<p id="acfa" class="graf graf--p graf-after--h3">Vamos começar com as importações, usaremos além do pandas, o&nbsp;<a class="markup--anchor markup--p-anchor" href="http://www.numpy.org/" target="_blank" rel="nofollow noopener" data-href="http://www.numpy.org/"><strong class="markup--strong markup--p-strong">numpy</strong></a>, biblioteca para&nbsp;<strong class="markup--strong markup--p-strong">computação científica</strong>&nbsp;e o&nbsp;<a class="markup--anchor markup--p-anchor" href="https://matplotlib.org/index.html" target="_blank" rel="nofollow noopener" data-href="https://matplotlib.org/index.html"><strong class="markup--strong markup--p-strong">matplotlib</strong></a>, biblioteca principal para&nbsp;<strong class="markup--strong markup--p-strong">visualização de dados</strong>, entretanto, como veremos mais adiante, o próprio pandas nos fornece facilidades em relação à visualização de dados, com métodos construídos com base no matplotlib, também importamos esta biblioteca para, além de poder modificar esteticamente nossos gráficos, facilitar a exibição dos gráficos. A linha&nbsp;<code class="markup--code markup--p-code">%matplotlib inline</code>&nbsp;faz parte da mágica do Jupyter e você não deve rodá-la caso esteja em outra IDE/Ambiente.</p>

<pre id="acc7" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">import</strong> <strong class="markup--strong markup--pre-strong">pandas</strong> <strong class="markup--strong markup--pre-strong">as</strong> <strong class="markup--strong markup--pre-strong">pd</strong><strong class="markup--strong markup--pre-strong">import</strong> <strong class="markup--strong markup--pre-strong">numpy</strong> <strong class="markup--strong markup--pre-strong">as</strong> <strong class="markup--strong markup--pre-strong">np</strong><strong class="markup--strong markup--pre-strong">import</strong> <strong class="markup--strong markup--pre-strong">matplotlib.pyplot</strong> <strong class="markup--strong markup--pre-strong">as</strong> <strong class="markup--strong markup--pre-strong">plt</strong>%<strong class="markup--strong markup--pre-strong">matplotlib</strong> inline</pre>
<p id="a462" class="graf graf--p graf-after--pre">Existem dois tipos principais de estruturas de dados no pandas:</p>

<h4 id="55a0" class="graf graf--h4 graf-after--p">Series</h4>
<p id="2a3d" class="graf graf--p graf-after--h4">Uma Series é como um array unidimensional, uma lista de valores. Toda Series possui um índice, o&nbsp;<code class="markup--code markup--p-code">index</code>, que dá rótulos a cada elemento da lista. Abaixo criamos uma Series&nbsp;<code class="markup--code markup--p-code">notas</code>, o&nbsp;<code class="markup--code markup--p-code">index</code>&nbsp;desta Series é a coluna à esquerda, que vai de 0 a 4 neste caso, que o pandas criou automaticamente, já que não especificamos uma lista de rótulos.</p>

<pre id="474d" class="graf graf--pre graf-after--p">notas = pd.Series([2,7,5,10,6])notas</pre>
<pre id="0b4b" class="graf graf--pre graf-after--pre">02172531046dtype: int64</pre>
<p id="ff78" class="graf graf--p graf-after--pre">Já podemos aqui verificar os atributos da nossa Series, comecemos pelos valores e o índice, os dois atributos&nbsp;<em class="markup--em markup--p-em">fundamentais</em>&nbsp;nesta estrutura:</p>

<pre id="4354" class="graf graf--pre graf-after--p">notas.values</pre>
<pre id="8ad6" class="graf graf--pre graf-after--pre">array([ 2,7,5, 10,6])</pre>
<pre id="172d" class="graf graf--pre graf-after--pre">notas.index</pre>
<pre id="f623" class="graf graf--pre graf-after--pre">RangeIndex(start=0, stop=5, step=1)</pre>
<p id="7342" class="graf graf--p graf-after--pre">Como ao criar a Series não demos um índice específico o pandas usou os inteiros positivos crescentes como padrão. Pode ser conveniente atribuirmos um índice diferente do padrão, supondo que essas sejam notas de uma turma, poderíamos atribuir nomes ao index:</p>

<pre id="1ba7" class="graf graf--pre graf-after--p">notas = pd.Series([2,7,5,10,6], index=["Wilfred", "Abbie", "Harry", "Julia", "Carrie"])notas</pre>
<pre id="07b3" class="graf graf--pre graf-after--pre">Wilfred2Abbie7Harry5Julia10Carrie6dtype: int64</pre>
<p id="5540" class="graf graf--p graf-after--pre">O index nos ajuda para referenciar um determinado valor, ele nos permite acessar os valores pelo seu rótulo:</p>

<pre id="b5f7" class="graf graf--pre graf-after--p">notas["Julia"]</pre>
<pre id="804e" class="graf graf--pre graf-after--pre">10</pre>
<p id="eb01" class="graf graf--p graf-after--pre">Outra facilidade proporcionada pela estrutura são seus métodos que fornecem informações estatísticas sobre os valores, como&nbsp;<strong class="markup--strong markup--p-strong">média</strong>&nbsp;<code class="markup--code markup--p-code">.mean()</code>&nbsp;e&nbsp;<strong class="markup--strong markup--p-strong">desvio padrão</strong>&nbsp;<code class="markup--code markup--p-code">.std()</code>. Encorajo o leitor(a) a investigar e verificar alguns dos métodos e atributos da estrutura usando o&nbsp;<code class="markup--code markup--p-code">TAB</code>&nbsp;para auto-completação na shell do Python, ou simplesmente checar a completíssima&nbsp;<a class="markup--anchor markup--p-anchor" href="https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html#pandas.Series" target="_blank" rel="noopener nofollow" data-href="https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html#pandas.Series">documentação oficial</a>&nbsp;deste objeto.</p>

<pre id="5e5d" class="graf graf--pre graf-after--p">print("Média:", notas.mean())print("Desvio padrão:", notas.std())</pre>
<pre id="6fb8" class="graf graf--pre graf-after--pre">Média: 6.0Desvio padrão: 2.9154759474226504</pre>
<p id="f00f" class="graf graf--p graf-after--pre">Geralmente para resumir brevemente as estatísticas dos dados se usa o&nbsp;<code class="markup--code markup--p-code">.describe()</code></p>

<pre id="e51f" class="graf graf--pre graf-after--p">notas.describe()</pre>
<pre id="3211" class="graf graf--pre graf-after--pre">count5.000000mean6.000000std2.915476min2.00000025%5.00000050%6.00000075%7.000000max10.000000dtype: float64</pre>
<p id="af42" class="graf graf--p graf-after--pre">A estrutura é flexível o suficiente pra aplicarmos algumas expressões matemáticas e funções matemáticas do numpy diretamente:</p>

<pre id="8396" class="graf graf--pre graf-after--p">notas**2</pre>
<pre id="8bc6" class="graf graf--pre graf-after--pre">Wilfred4Abbie49Harry25Julia100Carrie36dtype: int64</pre>
<pre id="00be" class="graf graf--pre graf-after--pre">np.log(notas)</pre>
<pre id="b44b" class="graf graf--pre graf-after--pre">Wilfred0.693147Abbie1.945910Harry1.609438Julia2.302585Carrie1.791759dtype: float64</pre>
<h4 id="164f" class="graf graf--h4 graf-after--pre"><strong class="markup--strong markup--h4-strong">DataFrame</strong></h4>
<p id="3972" class="graf graf--p graf-after--h4">Já um DataFrame é uma estrutura bidimensional de dados, como uma planilha. Abaixo criaremos um DataFrame que possui valores de diferentes tipos, usando um dicionário como entrada dos dados:</p>

<pre id="786c" class="graf graf--pre graf-after--p">df = pd.DataFrame({'Aluno' : ["Wilfred", "Abbie", "Harry", "Julia", "Carrie"],'Faltas' : [3,4,2,1,4],'Prova' : [2,7,5,10,6],'Seminário': [8.5,7.5,9.0,7.5,8.0]})df</pre>
<figure id="b966" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*pJjjHNL_P0TgUMfJ0Ihvpw.png" data-width="253" data-height="171" data-scroll="native"><img class="size-full wp-image-2410 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/2-min.png" alt="" width="253" height="171"></div>
</div></figure>
<p id="f9e9" class="graf graf--p graf-after--figure">Os tipos de dados que compõe as colunas podem ser verificados por um método próprio:</p>

<pre id="b525" class="graf graf--pre graf-after--p">df.dtypes</pre>
<pre id="72f4" class="graf graf--pre graf-after--pre">AlunoobjectFaltasint64Provaint64Semináriofloat64dtype: object</pre>
<p id="600e" class="graf graf--p graf-after--pre">É possível acessar a lista de colunas de forma bem intuitiva:</p>

<pre id="fcfe" class="graf graf--pre graf-after--p">df.columns</pre>
<pre id="aed2" class="graf graf--pre graf-after--pre">Index(['Aluno', 'Faltas', 'Prova', 'Seminário'], dtype='object')</pre>
<p id="8407" class="graf graf--p graf-after--pre">Os nomes das colunas podem ser usadas pra acessar seus valores:</p>

<pre id="0b61" class="graf graf--pre graf-after--p">df["Seminário"]</pre>
<pre id="8992" class="graf graf--pre graf-after--pre">08.517.529.037.548.0Name: Seminário, dtype: float64</pre>
<p id="51ea" class="graf graf--p graf-after--pre">Para DataFrames,&nbsp;<code class="markup--code markup--p-code">.describe()</code>&nbsp;também é uma boa forma de verificar resumidamente a disposição estatística dos dados numéricos:</p>

<pre id="e905" class="graf graf--pre graf-after--p">df.describe()</pre>
<figure id="a622" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*vC8JO_2hnIsh7Xd6MNocwg.png" data-width="261" data-height="246" data-scroll="native"><img class="size-full wp-image-2411 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/3-min.png" alt="" width="261" height="246"></div>
</div></figure>
<p id="4140" class="graf graf--p graf-after--figure">Outra tarefa comum aplicada em DataFrames é ordená-los por determinada coluna:</p>

<pre id="2581" class="graf graf--pre graf-after--p">df.sort_values(by="Seminário")</pre>
<figure id="fae3" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*JZTxzzOExUXbq8c8-qxw2g.png" data-width="244" data-height="173" data-scroll="native"><img class="size-full wp-image-2412 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/4-min.png" alt="" width="244" height="173"></div>
</div></figure>
<p id="92d9" class="graf graf--p graf-after--figure">Note que simplesmente usar o método&nbsp;<code class="markup--code markup--p-code">sort_values</code>&nbsp;não modifica o nosso DataFrame original:</p>

<pre id="3c38" class="graf graf--pre graf-after--p">df</pre>
<figure id="478f" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2413 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/5-min.png" alt="" width="254" height="166"></div>
</div></figure>
<p id="c71e" class="graf graf--p graf-after--figure">Muitas vezes é necessário selecionarmos valores específicos de um DataFrame, seja uma linha ou uma célula específica, e isso pode ser feito de diversas formas. A documentação oficial contém&nbsp;<a class="markup--anchor markup--p-anchor" href="https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing" target="_blank" rel="nofollow noopener" data-href="https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing">vasta informação</a>&nbsp;para esse tipo de tarefa, aqui nos concentraremos nas formas mais comuns de selecionarmos dados.</p>
<p id="5ecb" class="graf graf--p graf-after--p">Para selecionar pelo index ou rótulo usamos o atributo&nbsp;<code class="markup--code markup--p-code">.loc</code>:</p>

<pre id="9242" class="graf graf--pre graf-after--p">df.loc[3]</pre>
<pre id="feb6" class="graf graf--pre graf-after--pre">AlunoJuliaFaltas1Prova10Seminário7.5Name: 3, dtype: object</pre>
<p id="fd1d" class="graf graf--p graf-after--pre">Para selecionar de acordo com critérios condicionais, se usa o que se chama de&nbsp;<strong class="markup--strong markup--p-strong">Boolean Indexing</strong>.</p>
<p id="d742" class="graf graf--p graf-after--p">Suponha que queiramos selecionar apenas as linhas em que o valor da coluna&nbsp;<em class="markup--em markup--p-em">Seminário&nbsp;</em>seja acima de 8.0, podemos realizar esta tarefa passando a condição diretamente como índice:</p>

<pre id="5013" class="graf graf--pre graf-after--p">df[df["Seminário"] &gt; 8.0]</pre>
<figure id="bdae" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"></div>
<img class="size-full wp-image-2414 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/6-min.png" alt="" width="263" height="98">

</div></figure>
<p id="0847" class="graf graf--p graf-after--figure">Este tipo de indexação também possibilita checar condições de múltiplas colunas. Diferentemente do que estamos habituados em Python, aqui se usam operadores bitwise, ou seja,&nbsp;<code class="markup--code markup--p-code">&amp;</code>,&nbsp;<code class="markup--code markup--p-code">|</code>,&nbsp;<code class="markup--code markup--p-code">~</code>&nbsp;ao invés de&nbsp;<code class="markup--code markup--p-code">and</code>,&nbsp;<code class="markup--code markup--p-code">or</code>,&nbsp;<code class="markup--code markup--p-code">not</code>, respectivamente. Suponha que além de&nbsp;<code class="markup--code markup--p-code">df["Seminário"] &gt; 8.0</code>&nbsp;queiramos que o valor da coluna&nbsp;<code class="markup--code markup--p-code">Prova</code>&nbsp;não seja menor que 3:</p>

<pre id="e50e" class="graf graf--pre graf-after--p">df[(df["Seminário"] &gt; 8.0) &amp; (df["Prova"] &gt; 3)]</pre>
<figure id="5579" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"></div>
<img class="size-full wp-image-2415 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/7-min.png" alt="" width="244" height="63">

</div></figure>
<p id="9800" class="graf graf--p graf-after--figure">Por enquanto é isso para manipulação de Series e DataFrames, conforme a seção de leitura de dados for se estendendo irei aprensentar alguns outros métodos dessas estruturas que poderão ser interessantes no contexto.</p>

<h4 id="fb05" class="graf graf--h4 graf-after--p">Leitura de&nbsp;Dados</h4>
<p id="8ce0" class="graf graf--p graf-after--h4">Na seção anterior vimos como manipular dados que foram criados durante esta apresentação, acontece que, na maioria das vezes, queremos analisar dados que já estão prontos. O pandas nos fornece uma série de funcionalidades de leitura de dados, pros mais diversos formatos estruturais de dados, experimente a auto-completação de&nbsp;<code class="markup--code markup--p-code">pd.read_&lt;TAB&gt;</code>, entre eles estão:</p>

<ol class="postList">
 	<li id="eedf" class="graf graf--li graf-after--p"><code class="markup--code markup--li-code">pd.read_csv</code>, para ler arquivos&nbsp;.csv, formato comum de armazenar dados de tabelas</li>
 	<li id="d99f" class="graf graf--li graf-after--li"><code class="markup--code markup--li-code">pd.read_xlsx</code>, para ler arquivos Excel&nbsp;.xlsx, é necessário instalar uma biblioteca adicional pra esta funcionalidade.</li>
 	<li id="c546" class="graf graf--li graf-after--li"><code class="markup--code markup--li-code">pd.read_html</code>, para ler tabelas diretamente de um website</li>
</ol>
<p id="a8b0" class="graf graf--p graf-after--li">Usaremos para analisar dados externos nesta introdução o&nbsp;<code class="markup--code markup--p-code">.read_csv</code>, pois é neste formato que se encontram nossos dados. CSV, ou comma-separated values é um formato muito comum de dados abertos, trata-se, como a sigla sugere, de valores divididos por vírgula, apesar de o caracter separador poder ser o ponto-e-vírgula ou outro.</p>
<p id="7f08" class="graf graf--p graf-after--p">O arquivo&nbsp;<code class="markup--code markup--p-code">dados.csv</code>&nbsp;está na mesma pasta do nosso script, então podemos passar como argumento do&nbsp;<code class="markup--code markup--p-code">.read_csv</code>&nbsp;apenas o seu nome. Outro argumento interessante da função é o&nbsp;<code class="markup--code markup--p-code">sep</code>, que por padrão é a vírgula, mas que pode ser definido como outro caractere caso seu dado esteja usando outro separador.</p>
<p id="f2e1" class="graf graf--p graf-after--p">Estes dados que usaremos como exemplo são dados sobre preços de apartamentos em 7 bairros da cidade do Rio de Janeiro: Botafogo, Copacabana, Gávea, Grajaú, Ipanema, Leblon, Tijuca. Os dados podem ser encontrados&nbsp;<a class="markup--anchor markup--p-anchor" href="https://raw.githubusercontent.com/mvinoba/notebooks-for-binder/master/dados.csv" target="_blank" rel="noopener nofollow" data-href="https://raw.githubusercontent.com/mvinoba/notebooks-for-binder/master/dados.csv">aqu</a>i&nbsp;<em class="markup--em markup--p-em">(Basta baixar diretamente ou copiar o texto pro seu editor preferido e salvar como dados.csv)</em>.</p>

<pre id="b6ab" class="graf graf--pre graf-after--p">df = pd.read_csv("dados.csv")df</pre>
<figure id="8a40" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*jduZH3sPi_EjJeQJll6sIQ.png" data-width="281" data-height="950" data-scroll="native"><canvas class="progressiveMedia-canvas js-progressiveMedia-canvas" width="22" height="75"></canvas>&nbsp;<img class="wp-image-2416 size-full aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/8-min.png" alt="" width="281" height="950"></div>
</div></figure>
<p id="2305" class="graf graf--p graf-after--figure">Como esperado, o DataFrame tem muitas linhas de dados, pra visualizar sucintamente as primeiras linhas de um DataFrame existe o método&nbsp;<code class="markup--code markup--p-code">.head()</code></p>

<pre id="6386" class="graf graf--pre graf-after--p">df.head()</pre>
<figure id="e35b" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill">&nbsp;<img class="size-full wp-image-2417 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/9-min.png" alt="" width="478" height="173"></div>
</div></figure>
<p id="b6b7" class="graf graf--p graf-after--figure">Por padrão&nbsp;<code class="markup--code markup--p-code">.head()</code>&nbsp;exibe as 5 primeiras linhas, mas isso pode ser alterado:</p>

<pre id="ebb3" class="graf graf--pre graf-after--p">df.head(n=10)</pre>
<figure id="74ae" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2418 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/10-min.png" alt="" width="486" height="308"></div>
</div></figure>
<p id="6697" class="graf graf--p graf-after--figure">Similarmente existe o&nbsp;<code class="markup--code markup--p-code">.tail()</code>, que exibe por padrão as últimas 5 linhas do DataFrame:</p>

<pre id="8f38" class="graf graf--pre graf-after--p">df.tail()</pre>
<figure id="0316" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill">&nbsp;&nbsp;<img class="size-full wp-image-2419 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/11-min.png" alt="" width="484" height="179"></div>
</div></figure>
<h4 id="b152" class="graf graf--h4 graf-after--figure">Manipulação de&nbsp;Dados</h4>
<p id="8ed3" class="graf graf--p graf-after--h4">Além de confiar em mim, quando mencionei os bairros que continham no nosso conjunto de dados, você pode verificar a informação usando um método que lista os valores únicos numa coluna:</p>

<pre id="9387" class="graf graf--pre graf-after--p">df["bairro"].unique()</pre>
<pre id="8348" class="graf graf--pre graf-after--pre">array(['Botafogo', 'Copacabana', 'Gávea', 'Grajaú', 'Ipanema', 'Leblon','Tijuca'], dtype=object)</pre>
<p id="1b7c" class="graf graf--p graf-after--pre">Também parece interessante verificarmos a hegemoneidade da nossa amostra em relação aos bairros. Pra tarefas de contar valores podemos sempre aproveitar de outro método disponível, o&nbsp;<code class="markup--code markup--p-code">.value_counts()</code>, também veremos um pouco mais abaixo como visualizar estes valores em forma de gráfico de barras.</p>

<pre id="4e05" class="graf graf--pre graf-after--p">df["bairro"].value_counts()</pre>
<pre id="a589" class="graf graf--pre graf-after--pre">Copacabana346Tijuca341Botafogo307Ipanema281Leblon280Grajaú237Gávea205Name: bairro, dtype: int64</pre>
<p id="5a73" class="graf graf--p graf-after--pre">Os valores contados também podem ser normalizados para expressar porcentagens:</p>

<pre id="4082" class="graf graf--pre graf-after--p">df["bairro"].value_counts(normalize=<strong class="markup--strong markup--pre-strong">True</strong>)</pre>
<pre id="415a" class="graf graf--pre graf-after--pre">Copacabana0.173260Tijuca0.170756Botafogo0.153731Ipanema0.140711Leblon0.140210Grajaú0.118678Gávea0.102654Name: bairro, dtype: float64</pre>
<p id="913e" class="graf graf--p graf-after--pre">Agrupar os dados se baseando em certos critérios é outro processo que o pandas facilita bastante com o&nbsp;<code class="markup--code markup--p-code">.groupby()</code>. Esse método pode ser usado para resolver os mais&nbsp;<strong class="markup--strong markup--p-strong">amplos&nbsp;</strong>dos problemas, aqui abordarei apenas o agrupamento simples, a divisão de um DataFrame em grupos.</p>
<p id="309e" class="graf graf--p graf-after--p">Abaixo agrupamos o nosso DataFrame pelos valores da coluna&nbsp;<code class="markup--code markup--p-code">"bairro"</code>, e em seguida aplicamos o&nbsp;<code class="markup--code markup--p-code">.mean()</code>&nbsp;para termos um objeto GroupBy com informação das médias agrupadas pelos valores da coluna bairros.</p>

<pre id="2cf6" class="graf graf--pre graf-after--p">df.groupby("bairro").mean()</pre>
<figure id="33b5" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2420 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/12-min.png" alt="" width="644" height="266"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*_-cjZRxXqvrMAGmT6J7Bfw.png" data-width="644" data-height="266" data-scroll="native"><canvas class="progressiveMedia-canvas js-progressiveMedia-canvas" width="75" height="30"><img class="alignnone size-full wp-image-2420" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/12-min.png" alt="" width="644" height="266"></canvas></div>
</div></figure>
<p id="6362" class="graf graf--p graf-after--figure">Para extrairmos dados de uma coluna deste objeto basta acessá-lo convencionalmente, para obtermos os valores da média do preço do metro quadrado em ordem crescente, por exemplo:</p>

<pre id="2ee3" class="graf graf--pre graf-after--p">df.groupby("bairro").mean()["pm2"].sort_values()</pre>
<pre id="c40d" class="graf graf--pre graf-after--pre">bairroGrajaú6145.624473Tijuca7149.804985Copacabana11965.298699Botafogo12034.486189Gávea16511.582780Ipanema19738.407794Leblon20761.351036Name: pm2, dtype: float64</pre>
<p id="6c37" class="graf graf--p graf-after--pre">É comum queremos aplicar uma função qualquer aos dados, ou à parte deles, neste caso o pandas fornece o método&nbsp;<code class="markup--code markup--p-code">.apply</code>. Por exemplo, para deixar os nomes dos bairros como apenas as suas três primeiras letras:</p>

<pre id="6ae7" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">def</strong> truncar(bairro):<strong class="markup--strong markup--pre-strong">return</strong> bairro[:3]</pre>
<pre id="0aa5" class="graf graf--pre graf-after--pre">df["bairro"].apply(truncar)</pre>
<pre id="035e" class="graf graf--pre graf-after--pre">0Bot1Bot2Bot3Bot4Bot5Bot6Bot7Bot8Bot9Bot10Bot...1987Tij1988Tij1989Tij1990Tij1991Tij1992Tij1993Tij1994Tij1995Tij1996TijName: bairro, Length: 1997, dtype: object</pre>
<p id="44be" class="graf graf--p graf-after--pre">Ou de um jeito mais prático, usando uma função lambda:</p>

<pre id="f3d7" class="graf graf--pre graf-after--p">df["bairro"].apply(<strong class="markup--strong markup--pre-strong">lambda</strong> x: x[:3])</pre>
<pre id="3c25" class="graf graf--pre graf-after--pre">0Bot1Bot2Bot3Bot4Bot5Bot6Bot7Bot8Bot9Bot10Bot...1986Tij1987Tij1988Tij1989Tij1990Tij1991Tij1992Tij1993Tij1994Tij1995Tij1996TijName: bairro, Length: 1997, dtype: object</pre>
<p id="ab36" class="graf graf--p graf-after--pre">Uma das tarefas na qual o pandas é reconhecidamente poderoso é a habilidade de tratar dados incompletos. Por muitos motivos pode haver incompletude no dataset, o&nbsp;<code class="markup--code markup--p-code">np.nan</code>&nbsp;é um valor especial definido no&nbsp;<strong class="markup--strong markup--p-strong">Numpy</strong>, sigla para&nbsp;<strong class="markup--strong markup--p-strong">Not a Number</strong>, o pandas preenche células sem valores em um DataFrame lido com&nbsp;<code class="markup--code markup--p-code">np.nan</code>.</p>
<p id="8e0d" class="graf graf--p graf-after--p">Vamos criar um novo dataframe usando as 5 primeiras linhas do nosso original, usando o já visto&nbsp;<code class="markup--code markup--p-code">.head()</code>. Abaixo é usado o&nbsp;<code class="markup--code markup--p-code">.replace</code>&nbsp;para substituir um valor específico por um&nbsp;<code class="markup--code markup--p-code">NaN</code>.</p>

<pre id="dc76" class="graf graf--pre graf-after--p">df2 = df.head()df2 = df2.replace({"pm2": {12031.25: np.nan}})df2</pre>
<figure id="4ee8" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2421 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/13-min.png" alt="" width="473" height="168"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*FI63YsNzQ1l2e8O6UZ9s1w.png" data-width="473" data-height="168" data-scroll="native"></div>
</div></figure>
<p id="cba2" class="graf graf--p graf-after--figure">O pandas simplifica a remoção de quaiquer linhas ou colunas que possuem um&nbsp;<code class="markup--code markup--p-code">np.nan</code>, por padrão o&nbsp;<code class="markup--code markup--p-code">.dropna()</code>&nbsp;retorna as linhas que não contém um NaN:</p>

<pre id="db99" class="graf graf--pre graf-after--p">df2.dropna()</pre>
<figure id="1232" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2422 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/14-min.png" alt="" width="478" height="147"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*6dXjIY9cwxi4IdW77pBoHA.png" data-width="478" data-height="147" data-scroll="native"></div>
</div></figure>
<p id="e040" class="graf graf--p graf-after--figure">Preencher todos os valores NaN por um outro específico também é bastante simples:</p>

<pre id="589c" class="graf graf--pre graf-after--p">df2.fillna(99)</pre>
<figure id="bc28" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2423 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/15-min.png" alt="" width="481" height="178"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*X6bu3GSxNcI5Ms8MdRfLbg.png" data-width="481" data-height="178" data-scroll="native"></div>
</div></figure>
<p id="428f" class="graf graf--p graf-after--figure">Acaba sendo muitas vezes conveniente termos um método que indica quais valores de um dataframe são NaN e quais não são:</p>

<pre id="2b69" class="graf graf--pre graf-after--p">df2.isna()</pre>
<figure id="1d69" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2424 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/16-min.png" alt="" width="438" height="171"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*cU7sIWM9DBHuEpnnIlADrA.png" data-width="438" data-height="171" data-scroll="native"></div>
</div></figure>
<h4 id="8c46" class="graf graf--h4 graf-after--figure">Visualização de&nbsp;Dados</h4>
<p id="0c37" class="graf graf--p graf-after--h4">Partiremos agora para visualização de dados com o pandas. Os métodos de visualização do pandas são construídos com base no matplotlib para exploração rápida dos dados. Para se ter mais liberdade no conteúdo e possibilidades de visualização se recomenda usar diretamente o matplotlib ou ainda, para visualização estatística, o seaborn. Nesta introdução tratarei apenas dos métodos de visualização incluídos no pandas, que por outro lado, oferece uma sintaxe bastante simples para realizar a tarefa.</p>
<p id="64f0" class="graf graf--p graf-after--p">Comecemos verificando que tanto Series como DataFrame possuem um método&nbsp;<code class="markup--code markup--p-code">.plot()</code>&nbsp;que também é um atributo e pode ser encadeado para gerar visualização de diversos tipos, como histograma, área, pizza e dispersão, com respectivamente&nbsp;<code class="markup--code markup--p-code">.hist()</code>,&nbsp;<code class="markup--code markup--p-code">.area()</code>,&nbsp;<code class="markup--code markup--p-code">.pie()</code>&nbsp;e&nbsp;<code class="markup--code markup--p-code">.scatter()</code>, além de vários&nbsp;<a class="markup--anchor markup--p-anchor" href="https://pandas.pydata.org/pandas-docs/stable/api.html#api-dataframe-plotting" target="_blank" rel="nofollow noopener" data-href="https://pandas.pydata.org/pandas-docs/stable/api.html#api-dataframe-plotting">outros</a>.</p>
<p id="f1c2" class="graf graf--p graf-after--p">Vamos verificar a distribuição dos preços usando o encadeamento&nbsp;<code class="markup--code markup--p-code">.plot.hist()</code>, o eixo x, que é o preço, está numa escala de *10^7, como mostrado na imagem:</p>

<pre id="5b31" class="graf graf--pre graf-after--p">df["preco"].plot.hist()</pre>
<figure id="bc62" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*MYGTZPtB9nPOd5YJhjYHgQ.png" data-width="414" data-height="271" data-scroll="native"><img class="size-full wp-image-2425 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/17-min.png" alt="" width="414" height="271"></div>
</div></figure>
<p id="9916" class="graf graf--p graf-after--figure">Por padrão esse método usa 10 bins, ou seja, divide os dados em 10 partes, mas é claro que podemos especificar um valor para a plotagem. Abaixo, além de especificar a quantidade de bins, também especifiquei a cor das bordas como preta, que por padrão é transparente.</p>

<pre id="6aba" class="graf graf--pre graf-after--p">df["preco"].plot.hist(bins=30, edgecolor='black')</pre>
<figure id="a87b" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2426 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/18-min.png" alt="" width="418" height="271"></div>
</div></figure>
<p id="b374" class="graf graf--p graf-after--figure">Podemos usar os valores de contagem de cada bairro como exemplo de dado para um plot tanto de barras verticais quando de barras horizontais, para verificar visualmente esses dados:</p>

<pre id="177f" class="graf graf--pre graf-after--p">df["bairro"].value_counts().plot.bar()</pre>
<figure id="36f3" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="alignnone size-full wp-image-2427 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/19-min.png" alt="" width="394" height="316"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" style="text-align: center;" data-image-id="1*89s-t-O4GwLlc8MRden1ng.png" data-width="394" data-height="316" data-scroll="native"></div>
</div></figure>
<pre id="0c60" class="graf graf--pre graf-after--figure">df["bairro"].value_counts().plot.barh()</pre>
<figure id="d1da" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*obyrImoaTKQimaestHIF9g.png" data-width="422" data-height="252" data-scroll="native"><img class="alignnone size-full wp-image-2428 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/20-min.png" alt="" width="422" height="252"></div>
</div></figure>
<p id="dbc4" class="graf graf--p graf-after--figure">Os métodos são flexíveis o suficiente para aceitarem argumentos como um título para a imagem:</p>

<pre id="7bad" class="graf graf--pre graf-after--p">df["bairro"].value_counts().plot.barh(title="Número de apartamentos")</pre>
<figure id="61d2" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*KYW3unFyNr0u1bg6e0eH7w.png" data-width="433" data-height="271" data-scroll="native"><img class="alignnone size-full wp-image-2429 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/21-min.png" alt="" width="433" height="271"></div>
</div></figure>
<p id="8eda" class="graf graf--p graf-after--figure">Um gráfico de dispersão usando um DataFrame pode ser usado especificando-se quais colunas usar como dados no eixo x e y:</p>

<pre id="5113" class="graf graf--pre graf-after--p">df.plot.scatter(x='preco', y='area')</pre>
<figure id="b5da" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="alignnone size-full wp-image-2430 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/22-min.png" alt="" width="412" height="279"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*_wMpiCLrlAClvsSgzbnwEw.png" data-width="412" data-height="279" data-scroll="native"></div>
</div></figure>
<p id="5f95" class="graf graf--p graf-after--figure">Para fins estéticos, o matplotlib fornece uma série de styles diferentes que podem ser usados, um deles é o ggplot</p>

<pre id="e0ca" class="graf graf--pre graf-after--p">plt.style.use('ggplot')</pre>
<p id="482d" class="graf graf--p graf-after--pre">Agora este estilo será usado em todas as imagens geradas após essa linha</p>

<pre id="39eb" class="graf graf--pre graf-after--p">df.plot.scatter(x='pm2', y='area')</pre>
<figure id="6ac0" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="alignnone size-full wp-image-2431 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/23-min.png" alt="" width="402" height="276"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*N7UzOyO5OnzXSzDOvdO-Dw.png" data-width="402" data-height="276" data-scroll="native"></div>
</div></figure>
<p id="5770" class="graf graf--p graf-after--figure">A lista de estilos disponíveis pode ser vista através de um método próprio</p>

<pre id="2e3f" class="graf graf--pre graf-after--p">plt.style.available</pre>
<pre id="374c" class="graf graf--pre graf-after--pre">['bmh','Solarize_Light2','seaborn-talk','seaborn-bright','seaborn-white','seaborn-pastel','seaborn-ticks','seaborn-dark-palette','seaborn','tableau-colorblind10','seaborn-deep','classic','seaborn-dark','grayscale','seaborn-paper','fivethirtyeight','seaborn-muted','_classic_test','seaborn-poster','seaborn-notebook','seaborn-darkgrid','seaborn-colorblind','dark_background','seaborn-whitegrid','ggplot','fast']</pre>
<p id="4489" class="graf graf--p graf-after--pre">A coluna de quartos diz quantos quartos tem um determinado apartamento, também se pode ver a contagem e distribuição usando outros métodos de plotagem oferecidos pelo pandas:</p>

<pre id="37ca" class="graf graf--pre graf-after--p">df["quartos"].value_counts().plot.pie()</pre>
<figure id="9522" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*6ft09vISeO0KkzcGQ4E9ww.png" data-width="347" data-height="252" data-scroll="native"><img class="alignnone size-full wp-image-2432 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/24-min.png" alt="" width="347" height="252"></div>
</div></figure>
<p id="117c" class="graf graf--p graf-after--figure">Uma coisa a se notar do gráfico de scatter é a poluição causada pela enorme quantidade de dados agrupadas num dos cantos do gráfico, além de podermos diminuir o tamanho dos pontos passando o argumento&nbsp;<code class="markup--code markup--p-code">s</code>&nbsp;ao método&nbsp;<code class="markup--code markup--p-code">.scatter</code>&nbsp;podemos também usar um método do pandas que cria uma amostragem aleatória dos dados.</p>
<p id="9e44" class="graf graf--p graf-after--p">O&nbsp;<code class="markup--code markup--p-code">.sample</code>&nbsp;pode receber tanto um argumento&nbsp;<code class="markup--code markup--p-code">frac</code>, que determina uma fração dos itens que o método retornará (no caso abaixo, 10%), ou&nbsp;<code class="markup--code markup--p-code">n</code>, que determina um valor absoluto de itens.</p>

<pre id="5a12" class="graf graf--pre graf-after--p">df.plot.scatter(x='preco', y='area', s=.5)</pre>
<figure id="bcfb" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*A4qPUberN95atvPdsvF72Q.png" data-width="409" data-height="279" data-scroll="native"><img class="alignnone size-full wp-image-2433 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/25-min.png" alt="" width="409" height="279"></div>
</div></figure>
<pre id="2a1b" class="graf graf--pre graf-after--figure">df.sample(frac=.1).plot.scatter(x='preco', y='area')</pre>
<figure id="9100" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*bFWddRDPEjOpOoIlkLT0nw.png" data-width="411" data-height="272" data-scroll="native"><img class="alignnone size-full wp-image-2434 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/26-min.png" alt="" width="411" height="272"></div>
</div></figure>
<p id="6e34" class="graf graf--p graf-after--figure">Finalmente, a tarefa de salvar seu DataFrame externamente para um formato específico é feita com a mesma simplicidade que a leitura de dados é feita no pandas, pode-se usar, por exemplo, o método&nbsp;<code class="markup--code markup--p-code">to_csv</code>, e o arquivo será criado com os dados do DataFrame:</p>

<pre id="bf96" class="graf graf--pre graf-after--p">df = pd.DataFrame({'Aluno' : ["Wilfred", "Abbie", "Harry", "Julia", "Carrie"],'Faltas' : [3,4,2,1,4],'Prova' : [2,7,5,10,6],'Seminário': [8.5,7.5,9.0,7.5,8.0]})df.to_csv("aulas.csv")</pre>
<pre id="bd73" class="graf graf--pre graf-after--pre">pd.read_csv("aulas.csv")</pre>
<figure id="88cd" class="graf graf--figure graf-after--pre">
<div class="aspectRatioPlaceholder is-locked">
<div class="aspectRatioPlaceholder-fill"><img class="size-full wp-image-2435 aligncenter" src="https://pythondeaaz.com.br/wp-content/uploads/2018/11/27-min.png" alt="" width="334" height="173"></div>
<div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*KqH6anQf3HhAtDnq-6uBdg.png" data-width="334" data-height="173" data-scroll="native"></div>
</div></figure>
<p id="750f" class="graf graf--p graf-after--figure">Com o que foi abordado nesta introdução você já deve estar apto a fazer exploração e manipulação básica de dados com o&nbsp;<strong class="markup--strong markup--p-strong">pandas</strong>, para aprofundar mais aqui vão algumas referências:</p>

<ul class="postList">
 	<li id="1be6" class="graf graf--li graf-after--p"><a class="markup--anchor markup--li-anchor" href="http://pandas.pydata.org/pandas-docs/stable/index.html" target="_blank" rel="nofollow noopener" data-href="http://pandas.pydata.org/pandas-docs/stable/index.html">Documentação oficial</a></li>
 	<li id="5ffb" class="graf graf--li graf-after--li"><a class="markup--anchor markup--li-anchor" href="https://github.com/donnemartin/data-science-ipython-notebooks#pandas" target="_blank" rel="nofollow noopener" data-href="https://github.com/donnemartin/data-science-ipython-notebooks#pandas">Coletânea de notebooks Jupyter que abordam profundamente várias ferramentas e casos de uso do Pandas</a></li>
 	<li id="babb" class="graf graf--li graf-after--li graf--trailing"><a class="markup--anchor markup--li-anchor" href="https://github.com/guipsamora/pandas_exercises" target="_blank" rel="noopener nofollow" data-href="https://github.com/guipsamora/pandas_exercises">Exercícios de Pandas com soluções, separados por temas</a></li>
</ul>
<a href="https://medium.com/data-hackers/uma-introdu%C3%A7%C3%A3o-simples-ao-pandas-1e15eea37fa1" target="_blank">Postagem Original no site medium.com</a>