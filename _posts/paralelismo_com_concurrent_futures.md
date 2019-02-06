---
title: "Paralelismo em Python usando concurrent.futures"
excerpt_separator: "<!--more-->"
categories:
  - Programação
tags:
  - Paralelismo
  - Python
  - Parallelism
  - Queue
  - Fila
  - Filas
  - Queues
  - Threads
---

Esse post tem por objetivo abordar o uso da bliblioteca&nbsp;<a href="https://docs.python.org/dev/library/concurrent.futures.html">concurrent.futures</a>&nbsp;para realizar operações paralelas em Python. Dito isto, gostaria de contextualizar de forma simples&nbsp;<em>paralelismo</em>&nbsp;e&nbsp;<em>concorrência</em>:
<ul>
 	<li><strong>Concorrência:</strong>&nbsp;é quando um computador que possui apenas um core parece estar realizando duas ou mais operações ao mesmo tempo, quando na verdade está alternando a execução destas operações de forma tão rápida que temos a ilusão de que tudo é executado simultaneamente. e</li>
 	<li><strong>Paralelismo:</strong>&nbsp;é quando um computador que possui dois ou mais cores executa operações realmente de forma paralela, utilizando para isso os cores disponíveis, ou seja, se um determinado computador tem 2 cores, posso ter duas operações sendo executadas paralelamente cada uma em um core diferente.</li>
</ul>
Infelizmente o GIL (Global Interpreter Lock do Python) é restritivo quanto ao uso de threads paralelas em Python, porém o módulo&nbsp;<code>concurrent.futures</code>&nbsp;permite que possamos utilizar múltiplos cores. Para isso, este módulo "engana" o GIL criando novos interpretadores como subprocessos do interpretador principal. Desta maneira, cada subprocesso tem seu próprio GIL e, por fim, cada subprocesso tem um ligação com o processo principal, de forma que recebem instruções para realizar operações e retornar resultados.

Agora que já vimos um pouco de teoria vamos colocar em prática o uso do&nbsp;<code>concurrent.futures</code>. Vamos supor que tenhamos um lista de preços e que queremos aumentar em 10% o valor de cada item.

Vamos então criar uma função que gere uma lista de preços:
<div class="highlight">
<pre><span class="k">def</span> <span class="nf">generate_list</span><span class="p">():</span>
    <span class="n">result</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">20</span><span class="p">):</span>
        <span class="n">result</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">pow</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span> <span class="o">*</span> <span class="mi">42</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">result</span>
</pre>
</div>
Agora vamos criar uma função que calcule o preço acrescido de 10%.
<div class="highlight">
<pre><span class="k">def</span> <span class="nf">increase_price_by_10_percent</span><span class="p">(</span><span class="n">price</span><span class="p">):</span>
    <span class="n">price</span> <span class="o">+=</span> <span class="n">price</span> <span class="o">/</span> <span class="mi">10</span> <span class="o">*</span> <span class="mi">100</span>
    <span class="k">return</span> <span class="n">price</span>
</pre>
</div>
Dando continuidade, definiremos mais três funções.
<div class="highlight">
<pre><span class="k">def</span> <span class="nf">increase_price_serial</span><span class="p">(</span><span class="n">price_list</span><span class="p">,</span> <span class="n">increase_function</span><span class="p">):</span>
    <span class="n">start</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="n">result</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="n">increase_function</span><span class="p">,</span> <span class="n">price_list</span><span class="p">))</span>
    <span class="n">end</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="k">print</span><span class="p">(</span><span class="s2">"Took {}s to increase the values"</span><span class="o">.</span><span class="n">format</span><span class="p">((</span><span class="n">end</span> <span class="o">-</span> <span class="n">start</span><span class="p">)</span><span class="o">.</span><span class="n">total_seconds</span><span class="p">()))</span>

<span class="k">def</span> <span class="nf">increase_price_with_threads</span><span class="p">(</span><span class="n">price_list</span><span class="p">,</span> <span class="n">increase_function</span><span class="p">):</span>
    <span class="n">start</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="n">pool</span> <span class="o">=</span> <span class="n">ThreadPoolExecutor</span><span class="p">(</span><span class="n">max_workers</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>
    <span class="n">results</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">pool</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">increase_function</span><span class="p">,</span> <span class="n">price_list</span><span class="p">))</span>
    <span class="n">end</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="k">print</span><span class="p">(</span><span class="s2">"Took {}s to increase the prices with python Threads"</span><span class="o">.</span><span class="n">format</span><span class="p">((</span><span class="n">end</span> <span class="o">-</span> <span class="n">start</span><span class="p">)</span><span class="o">.</span><span class="n">total_seconds</span><span class="p">()))</span>

<span class="k">def</span> <span class="nf">increase_price_with_subprocess</span><span class="p">(</span><span class="n">price_list</span><span class="p">,</span> <span class="n">increase_function</span><span class="p">):</span>
    <span class="n">start</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="n">pool</span> <span class="o">=</span> <span class="n">ProcessPoolExecutor</span><span class="p">(</span><span class="n">max_workers</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>
    <span class="n">results</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">pool</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">increase_function</span><span class="p">,</span> <span class="n">price_list</span><span class="p">))</span>
    <span class="n">end</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">now</span><span class="p">()</span>
    <span class="k">print</span><span class="p">(</span><span class="s2">"Took {} to increase the prices with sub proccess"</span><span class="o">.</span><span class="n">format</span><span class="p">((</span><span class="n">end</span> <span class="o">-</span> <span class="n">start</span><span class="p">)</span><span class="o">.</span><span class="n">total_seconds</span><span class="p">()))</span>
</pre>
</div>
Note que as funções&nbsp;<code>increase_price_serial</code>,&nbsp;<code>increase_price_with_threads</code>&nbsp;e&nbsp;<code>increase_price_with_subprocess</code>&nbsp;são bem semelhantes, todas tem dois parâmetros:
<ul>
 	<li>o&nbsp;<code>price_list</code>, que é a lista de preços onde iremos fazer as operações ;</li>
 	<li>e o&nbsp;<code>increase_function</code>&nbsp;que é função que realizará as operações de acréscimo em cada item da lista.</li>
</ul>
A diferença entre estas funções está na forma em que as operações de acréscimo serão executadas conforme explicarei a seguir:
<ul>
 	<li><code>increase_price_serial</code>: aqui a função passada pelo parâmetro&nbsp;<code>increase_function</code>&nbsp;será executada para cada item da&nbsp;<code>price_list</code>&nbsp;de forma sequencial.</li>
 	<li><code>increase_price_with_threads</code>: aqui já começamos a fazer uso da classe&nbsp;<code>ThreadPoolExecutor</code>, que pertencente a lib&nbsp;<code>concurrent.futures</code>, e que vai nos permitir executar a&nbsp;<code>increase_function</code>&nbsp;de forma concorrente. Note que ao instanciar&nbsp;<code>ThreadPoolExecutor</code>&nbsp;estamos passando o parâmetro&nbsp;<code>max_workers=2</code>, isto está indicando o numero máximo de threads que será usado para executar as operações.</li>
 	<li><code>increase_price_with_subprocess</code>: nesta função estamos fazendo uso da classe&nbsp;<code>ProcessPoolExecutor</code>&nbsp;que tem a funionalidade bastante semelhante à classe&nbsp;<code>ThreadPoolExecutor</code>exceto pelo fato de que esta classe permite que a função&nbsp;<code>increase_function()</code>&nbsp;seja executada realmente de forma paralela. Essa "mágica" é conseguida da seguinte forma:
<ol>
 	<li>Cada item da lista de preços é serializado através do&nbsp;<code>pickle</code>;</li>
 	<li>Os dados serializados são copiados do processo principal para os processos filhos por meio de um socket local;</li>
 	<li>Aqui o&nbsp;<code>pickle</code>&nbsp;entra em cena novamente para deserializar os dados para os subprocessos;</li>
 	<li>Os subprocessos importam o módulo Python que contém a função que será utilizada; no nosso caso, será importado o módulo onde&nbsp;<code>increase_function</code>&nbsp;está localizada;</li>
 	<li>As funções são executadas de forma paralela em cada subprocesso;</li>
 	<li>O resultado destas funções é serializado e copiado de volta para o processo principal via socket;</li>
 	<li>Os resultados são desserializados e mesclados em uma lista para que possam ser retornados;</li>
</ol>
</li>
</ul>
Nota-se que a classe&nbsp;<code>ProcessPoolExecutor</code>&nbsp;faz muitos "malabarismos" para que o paralelismo seja realmente possível.
<h3>Os resultados</h3>
Na minha máquina, que tem mais de um core, executei o seguinte código:
<div class="highlight">
<pre>    <span class="n">prices</span> <span class="o">=</span> <span class="n">generate_list</span><span class="p">()</span>
    <span class="n">increase_price_serial</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_by_10_percent</span><span class="p">)</span>
    <span class="n">increase_price_with_threads</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_by_10_percent</span><span class="p">)</span>
    <span class="n">increase_price_with_subprocess</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_by_10_percent</span><span class="p">)</span>
</pre>
</div>
Trazendo os seguintes resultados:

|Função |#|Execução |#|Tempo gasto | |:--------------------------------|#|:------------------:|#|--------------------:| |&nbsp;<code>increase_price_serial</code>&nbsp;|#|Sequencial |#| 2.2e-05 secs | |&nbsp;<code>increase_price_with_threads</code>|#|Concorrente |#| 0.001646 secs | |&nbsp;<code>increase_price_with_subprocess</code>&nbsp;|#|Paralela |#| 0.016269 secs |

Veja que&nbsp;<code>increase_price_with_subproces</code>, mesmo sendo executada paralelamente, levou mais tempo que&nbsp;<code>increase_price_serial</code>. Isso ocorreu pois a função&nbsp;<code>increase_price_by_10_percent</code>, que é utilizada para fazer operações nos itens da lista, é uma função que não exige muito trabalho do processador. Desta forma, o&nbsp;<code>ProcessPoolExecutor</code>&nbsp;leva mais tempo fazendo o processo de paralelização propriamente dito do que realmente executando as operações de cálculo.

Vamos criar neste momento uma função que realize operações mais complexas:
<div class="highlight">
<pre><span class="k">def</span> <span class="nf">increase_price_crazy</span><span class="p">(</span><span class="n">price</span><span class="p">):</span>
    <span class="n">price</span> <span class="o">+=</span> <span class="n">price</span> <span class="o">/</span> <span class="mi">10</span> <span class="o">*</span> <span class="mi">100</span>
    <span class="n">new_prices</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">200000</span><span class="p">):</span>
        <span class="n">new_prices</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">price</span> <span class="o">+</span> <span class="nb">pow</span><span class="p">(</span><span class="n">price</span><span class="p">,</span> <span class="mi">2</span><span class="p">))</span>
    <span class="n">new_prices</span> <span class="o">=</span> <span class="nb">map</span><span class="p">(</span><span class="n">sqrt</span><span class="p">,</span> <span class="n">new_prices</span><span class="p">)</span>
    <span class="n">new_prices</span> <span class="o">=</span> <span class="nb">map</span><span class="p">(</span><span class="n">sqrt</span><span class="p">,</span> <span class="n">new_prices</span><span class="p">)</span>

    <span class="k">return</span> <span class="nb">max</span><span class="p">(</span><span class="n">price</span><span class="p">,</span> <span class="nb">min</span><span class="p">(</span><span class="n">new_prices</span><span class="p">))</span>
</pre>
</div>
<blockquote><strong>Nota:</strong>&nbsp;Esta função foi criada apenas para efeitos didáticos.</blockquote>
Vamos agora ulilizar esta função no lugar da função&nbsp;<code>increase_price_by_10_percent</code>:
<div class="highlight">
<pre>    <span class="n">increase_price_serial</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_crazy</span><span class="p">)</span>
    <span class="n">increase_price_with_threads</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_crazy</span><span class="p">)</span>
    <span class="n">increase_price_with_subprocess</span><span class="p">(</span><span class="n">prices</span><span class="p">,</span> <span class="n">increase_price_crazy</span><span class="p">)</span>
</pre>
</div>
Obtendo o reultado abaixo:

|Função |#|Execução |#|Tempo gasto | |:--------------------------------|#|:------------------:|#|--------------------:| |&nbsp;<code>increase_price_serial</code>&nbsp;|#|Sequencial |#| 4.10181 secs | |&nbsp;<code>increase_price_with_threads</code>|#|Concorrente |#| 4.566346 secs | |&nbsp;<code>increase_price_with_subprocess</code>&nbsp;|#|Paralela |#| 2.082025 secs |
<blockquote><strong>Nota:</strong>&nbsp;os valores de tempo gasto vão variar de acordo com o hardware disponível.</blockquote>
Veja que agora função&nbsp;<code>increase_price_with_subprocess</code>&nbsp;foi a mais rápida. Isto se deve o fato de que a nossa nova função ne cálculo&nbsp;<code>increase_price_crazy</code>&nbsp;demanda muito mais processamento , assim, o overhead para que se paralelize as operações tem um custo inferior ao custo de processamento das operações de cálculo.
<h2>Conclusão</h2>
Podemos concluir que é possível executar operações paralelas em python utilizando&nbsp;<code>ProcessPoolExecutor</code>, porém paralelizar nem sempre vai garantir que determinada operação vai ser mais performática. Temos sempre que avaliar a situação que temos em mãos.

Espero que este post tenha contribuído de alguma forma com conhecimento de vocês, sugestões e criticas serão bem vindas, obrigado!.
<blockquote><strong>Disclaimer:</strong>&nbsp;Existem varios conceitos como, locks, deadlocks, futures, data races e etc. que não foram abordados aqui para que o post não ficasse muito longo e complexo. A Versão do python utilizada foi a 3.5, a lib&nbsp;<code>concurrent.futures</code>&nbsp;está dispónivel desde a versão 3.2 do Python, no entanto, exite um backport para a versão 2.7 que é facilmente instalável via 'pip install futures'.</blockquote>
Link da postagem original <a href="http://pythonclub.com.br/paralelismo-em-python-usando-concurrent.futures.html" target="_blank" rel="noopener">aqui</a>.