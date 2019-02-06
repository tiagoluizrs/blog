---
title: "Filas e Pilhas em Python"
excerpt_separator: "<!--more-->"
date: 2019-01-25 09:00:00
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

<p>Você pode não perceber, mas boa parte dos programas que você usa no dia-a-dia utilizam internamente os tipos abstratos de dados chamados filas e pilhas. Eles são chamados dessa forma porque representam uma estrutura de dados com operações associadas que definem um certo comportamento. Eles são muito úteis para o programador pois podem ser utilizados em diversas situações e têm um <em>grande poder</em>de simplificar algoritmos. A seguir, explicarei cada uma dessas estruturas e demonstrarei como poderíamos implementá-las em Python.</p>
<h2>Filas</h2>
<p>Tenho certeza que você já sabe como uma fila funciona. Pense na fila que você pega toda vez que vai ao supermercado. Para que você seja atendido, é preciso que todas as pessoas que estiverem na sua frente na fila sejam atendidas ou desistam para que você seja atendido, certo? Por isso, podemos dizer que a idéia da fila é que o último a entrar na fila seja o último a sair.</p>
<pre class="wp-block-code"><code>                                     _________
                                    | o caixa |
------------------------------------|_________|
 o    ~o    @    &amp;     Q    0    O     0
/|\    []  {0\  /|\   /|\  /||  /-\   /0|
/ \    |\   |\  / \    |\  /|   |-|   / \
você   p6   p5  p4     p3  p2    p1   p0
-------------------------------------------
</code></pre>
<p>No exemplo acima, é preciso que p0, p1, p2, p3, p4, p5 e p6 sejam atendidas para que seja a sua vez de passar as compras e pagar por elas. Uma estrutura de dados <strong>Fila</strong> funciona da mesma maneira. Uma fila é uma estrutura utilizada especificamente para armazenamento temporário de dados na memória. Diferentemente de uma lista, que também serve para esse fim, uma fila possui regras quanto a qual elemento será retirado e onde será inserido um novo elemento. Em uma lista, é possível inserir elementos em qualquer posição e retirar quaisquer elementos, não importando sua posição. <strong>Em uma fila</strong>, os novos elementos que são inseridos são sempre posicionados ao final dela. Quando se faz a retirada de um elemento de uma fila, sempre iremos retirar o elemento que há mais tempo está nela (o primeiro). Imagine um <a href="https://pt.wikipedia.org/wiki/Servidor_web">servidor Web</a>que é capaz de atender a, no máximo, 2 requisições simultâneas. O que acontece quando chega uma terceira requisição no momento em que o servidor já está ocupado atendendo a 2 requisições? A solução mais óbvia seria colocar a nova requisição em uma área de espera. Assim, quando o servidor terminar de atender uma das atuais 2 requisições, ele poderá retirar a nova requisição da área de espera e atendê-la. E se, enquanto o servidor estiver ocupado atendendo a 2 requisições, chegarem em sequência 5 novas requisições?</p>
<pre class="wp-block-code"><code>   ______              
  |  r0  |       [ r6  r3]
  |  r1  |       [  r5   ]
  |______|       [r4  r2 ]
    /  \  
Servidor Web    Área de espera
</code></pre>
<p>O servidor poderia colocar as novas requisições em uma área de espera, e sempre que houver disponibilidade, retirar uma de lá e processá-la, até que não hajam mais requisições a serem processadas. A solução é boa, mas para ser justo com as solicitações que chegam dos usuários, o servidor deve processar primeiro as que já estão esperando há mais tempo, correto? Assim, o melhor a se fazer é utilizar uma <strong>fila</strong>para armazenar as requisições que estão em espera.</p>
<pre class="wp-block-code"><code>        ______    
       |  r0  |           
       |  r1  |      saída  -----------------------  entrada
       |______|      &lt;----   r2  r3  r4  r5  r6     &lt;------
         /  \               -----------------------
     Servidor Web                 Fila de espera
</code></pre>
<p>Dessa forma, a requisição que está há mais tempo esperando é a primeira a sair da fila quando o servidor tiver disponibilidade.</p>
<h3>Implementando uma fila</h3>
<p>Uma fila nada mais é do que uma estrutura de armazenamento com políticas de ordem de entrada e saída de elementos. Assim, ela pode ser implementada usando uma lista, por exemplo. Como poderíamos fazer? Sabemos que as listas oferecem alguns métodos conhecidos para inserção/remoção de elementos:</p>
<ul>
<li><code>.append(elemento)</code>: adiciona <code>elemento</code> ao final da lista;</li>
<li><code>.insert(índice, elemento)</code>: insere <code>elemento</code> após a posição <code>índice</code>;</li>
<li><code>.pop(índice)</code>: remove e retorna o elemento contido na posição <code>índice</code>.</li>
</ul>
<p>Para inserir elementos, podemos usar o método <code>append()</code>, que insere um elemento ao final de uma lista. Para a retirada de elementos, podemos utilizar o método <code>pop(x)</code>, que retira e retorna um elemento da posição <code>x</code>. Em se tratando de uma fila em que estamos inserindo elementos no final, de qual posição devemos retirar os elementos? Acertou quem pensou <em>“da primeira”</em>. Isso mesmo vamos remover o primeiro elemento utilizando <code>pop(0)</code>. Veja:</p>
<pre data-lang="python"><code>
&gt;&gt;&gt; fila = [10, 20, 30, 40, 50]
&gt;&gt;&gt; fila.append(60)  # insere um elemento no final da fila
&gt;&gt;&gt; print fila
[10, 20, 30, 40, 50, 60]
&gt;&gt;&gt; print fila.pop(0) # remove o primeiro elemento da lista
10
&gt;&gt;&gt; print fila
[20, 30, 40, 50, 60]
&gt;&gt;&gt; print fila.pop(0) # remove o primeiro elemento da lista
20
&gt;&gt;&gt; print fila
[30, 40, 50, 60]
&gt;&gt;&gt; print fila.pop(0) # remove o primeiro elemento da lista
30
&gt;&gt;&gt; print fila
[40, 50, 60]
</code></pre>
<p>Você deve estar se perguntando: <em>“e se eu fizesse o contrário, inserindo no início e removendo do final, funcionaria também como uma fila?”</em> Sim, funcionaria. Pois, da mesma forma, teríamos a política do <strong>primeiro a entrar, primeiro a sair</strong> também conhecida como <em>First-In, First-Out</em>, ou simplesmente FIFO. Agora, para criar uma forma consistente de usar filas em Python, vamos criar uma classe para encapsular as operações da fila. Podemos definir uma classe <code>Fila</code>que internamente tenha uma lista representando o local onde serão armazenados os elementos. Essa classe deverá ter dois métodos principais:</p>
<ul>
<li><code>insere(elemento)</code>: recebe como entrada um elemento a ser inserido na fila.</li>
<li><code>retira()</code>: remove um elemento da fila e o retorna para o chamador.</li>
</ul>
<p>Complete a implementação de fila abaixo, de acordo com o que foi explicado acima. O código completo se encontra no final deste texto, para que você possa comparar.</p>
<pre data-lang="python"><code>
class Fila(object):
    def __init__(self):
        self.dados = []
 
    def insere(self, elemento):
        __________________________________
 
    def retira(self):
</code></pre>
<p>Tendo a classe acima definida em um arquivo <code>fila.py</code>, poderíamos importar o módulo e usar tal classe:</p>
<pre data-lang="python"><code>
&gt;&gt;&gt; import fila
&gt;&gt;&gt; f = fila.Fila()
&gt;&gt;&gt; f.insere(10)
&gt;&gt;&gt; f.insere(20)
&gt;&gt;&gt; f.insere(30)
&gt;&gt;&gt; print f.retira()
10
&gt;&gt;&gt; print f.retira()
20
</code></pre>
<p><strong>Importante:</strong> segundo a própria documentação oficial Python, uma lista não é a estrutura mais recomendada para a implementação de uma fila, porque a inserção ou remoção de elementos do início da lista é lenta, se comparada à inserção/remoção do final da lista. Assim, é sugerido que seja usado um <code>deque</code> (<a href="http://docs.python.org/library/collections.html#collections.deque"><code>collections.deque</code></a>).</p>
<h3>Só isso?</h3>
<p>Não, nós vimos apenas as filas “comuns”. Voltando ao exemplo da fila do supermercado, imagine que você está chegando aos caixas e ainda não decidiu qual deles vai usar. Aí você vê que o caixa de atendimento preferencial para idosos/gestantes/deficientes possui apenas 3 pessoas na fila, enquanto que os outros caixas têm filas com no mínimo 10 pessoas. Como o caixa não é exclusivo para idosos, você vai lá e entra na fila. Outras pessoas percebem a sua “sagacidade” (:P) e fazem o mesmo. Fica tudo certo até que chega um idoso para entrar na fila e todas as pessoas que estão na fila são obrigados a ceder sua vez para o idoso. E eis que chega o clube da terceira idade inteiro para ser atendido logo em seguida. O que acontece? As pessoas que estão na fila cedem sua vez para os idosos, e assim, seu atendimento vai sendo postergado cada vez mais. Enfim, esse é um exemplo de uma <em>fila de prioridades</em>. Elementos (as pessoas) que possuem maior prioridade, saem antes da fila. Se quiser saber mais, veja <a href="http://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/priority.html">aqui</a>.</p>
<h2>Pilhas</h2>
<p>Assim como as filas, aposto que você sabe exatamente como funciona uma pilha. Pense em uma pilha de papéis sobre uma mesa. Se você precisar adicionar um papel a essa pilha, você o adiciona sobre a pilha, ou seja, no topo dela, certo? E quando vai retirar um papel da pilha, você começa pelo que estiver no topo, certo? Ou seja, diferentemente da fila (FIFO), em uma pilha o último a entrar nela, é o primeiro a sair (Last-In, First-Out — LIFO). Veja abaixo uma ilustração de como funciona uma pilha. No primeiro item da ilustração (1), temos uma pilha composta por 5 elementos, que foram inseridos cronologicamente na seguinte ordem: p0, p1, p2, p3, e, por fim, p4. A segunda parte da ilustração (2) mostra o estado da pilha p após ter sido realizada a inserção de um novo elemento (p5). A terceira parte (3) mostra a pilha p após haver a retirada de um elemento. Como você pode ver, o elemento retirado foi o último a ter sido inserido (p5). Na última parte da ilustração (4), é apresentada mais uma retirada de elemento da pilha, desta vez p4. Se houvessem mais operações de retirada, teríamos a retirada, em ordem, dos elementos: p3, p2, p1 e p0.</p>
<pre class="wp-block-code"><code>|          |    |----p5----|    |          |    |          |
|----p4----|    |----p4----|    |----p4----|    |          |
|----p3----|    |----p3----|    |----p3----|    |----p3----|
|----p2----|    |----p2----|    |----p2----|    |----p2----|
|----p1----|    |----p1----|    |----p1----|    |----p1----|
|----p0----|    |----p0----|    |----p0----|    |----p0----|
============    ============    ============    ============
  Pilha p       p.insere(p5)     p.retira()      p.retira()
    (1)             (2)              (3)            (4)
</code></pre>
<p>Tranquilo, né? O que você deve lembrar sobre as pilhas é que ela usa uma política LIFO (Last-In, First-Out) para inserção/retirada de elementos.</p>
<h3>Onde as pilhas são usadas?</h3>
<p>Talvez a mais famosa utilização de pilhas em computação esteja no gerenciamento de chamadas de função de um programa. Uma pilha pode ser usada para manter informações sobre as funções de um programa que estejam ativas, aguardando por serem terminadas. Considere o seguinte exemplo:</p>
<pre data-lang="python"><code>
def ola():
    print "olá, "
    mundo()
 
def mundo():
    print "mundo!"
 
def olamundo():
    ola()
 
olamundo()
</code></pre>
<p>A primeira função a ser chamada é a <code>olamundo()</code>, que por sua vez chama a função <code>ola()</code>, então a função <code>olamundo()</code> é empilhada, pois seu término depende do término da função <code>ola()</code>. Essa, por sua vez, chama a função <code>mundo()</code> e é empilhada. Ao terminar a execução da função <code>mundo()</code>, a função <code>ola()</code> é desempilhada e sua execução termina de onde havia parado (chamada à função <code>mundo()</code>). Como não há mais nada a ser executado nessa função, sua execução termina, e a função <code>olamundo()</code>é desempilhada e sua execução continua, encerrando assim o programa.</p>
<pre class="wp-block-code"><code>                 ola()
olamundo()  --&gt;  olamundo()  --&gt; olamundo() --&gt;   Fim do programa.
</code></pre>
<p>Outra utilização de pilhas é a verificação do balanceamento de parênteses. Como saber se os seguintes parênteses estão balanceados, isto é, se para cada abre-parênteses, existe um fecha-parênteses correspondente?</p>
<pre class="wp-block-code"><code>(((((((((((((((((()()()()))))))())))()))()))()))((()))))
</code></pre>
<p>Uma forma bem simples de resolver esse problema é ler a sequência de parênteses, um por um e, a cada abre-parênteses que encontrarmos, vamos empilhá-lo. Quando encontrarmos um fecha-parênteses, devemos desempilhar um abre-parênteses, pois encontramos um fecha-parênteses correspondente a ele. Assim, ao final da avaliação da sequência acima, se ela estiver balanceada corretamente, não restarão elementos na pilha. Vejamos um exemplo mais simples:</p>
<pre class="wp-block-code"><code>(())()

                (
Pilha       (   (   (       (

Leitura     (   (   )   )   (   )   FIM
</code></pre>
<p>Repare agora em uma sequência desbalanceada:</p>
<pre class="wp-block-code"><code>(())(

                (
Pilha       (   (   (       (   (

Leitura     (   (   )   )   (   FIM
</code></pre>
<p>Perceba que a leitura de parênteses da entrada terminou, mas a pilha não estava mais vazia.</p>
<h3>Implementação</h3>
<p>Agora eu lhe pergunto: o que muda da implementação da fila para a implementação da pilha? A diferença é pouca, mas é muito importante. Assim como para as filas, para a implementação de pilhas podemos utilizar uma lista como estrutura para armazenamento dos dados. Basta agora definir como será o funcionamento:</p>
<ol>
<li>Iremos inserir e retirar elementos do início da lista?</li>
<li>Ou iremos inserir e retirar elementos do final da lista?</li>
</ol>
<p>Sabendo que em Python a inserção e remoção de elementos no final de uma lista é menos custoso do que fazer as mesmas operações no início dela, vamos adotar a segunda opção. Então, complete o código abaixo e teste em seu computador.</p>
<pre data-lang="python"><code>
class Pilha(object):
    def __init__(self):
        self.dados = []
 
    def empilha(self, elemento):
        __________________________________
 
    def desempilha(self):
        __________________________________
 
p = Pilha()
p.empilha(10)
p.empilha(20)
p.empilha(30)
p.empilha(40)
print p.desempilha()
print p.desempilha()
print p.desempilha()
print p.desempilha()
</code></pre>
<p>O programa acima, se implementado corretamente, deverá mostrar o seguinte resultado na tela:</p>
<pre class="wp-block-code"><code>40 30 20 10</code></pre>
<p>Para adicionar um elemento no final de uma lista, basta usar o método <code>append()</code>. E para remover o último elemento da lista? <code>.pop(tamanho_da_lista-1)</code> é o que devemos fazer. E para obter o tamanho da lista, podemos usar a função <code>len()</code>. Então:</p>
<pre data-lang="python"><code><br />
def desempilha(self):<br />
    return self.dados.pop(len(dados)-1)<br />
</code></pre>
<p>Ou então, podemos usar <code>self.dados.pop(-1)</code>. O acesso ao índice <code>-1</code>é a forma pythônica de se referir ao último elemento de uma sequência.</p>
<pre data-lang="python"><code><br />
def desempilha(self):
    return self.dados.pop(-1)
</code></pre>
<h4>Mais alguma operação?</h4>
<p>Outra operação fundamental que deve estar disponível em uma Pilha, é um método que retorne um booleano indicando se a pilha está vazia. Um jeito bem simples seria usando a <em>builtin</em> <code>len()</code> sobre a nossa lista interna <code>self.dados</code> e verificando se ela retorna <code>0</code>como resultado.</p>
<pre data-lang="python"><code><br />
def vazia(self):
    return len(self.dados) == 0
</code></pre>
<h2>Finalizando…</h2>
<p>Tanto a fila quanto a pilha são estruturas importantes pra caramba e sua implementação deve fornecer um bom desempenho, visto que elas são amplamente usadas nos programas que compõem o nosso dia-a-dia. As implementações vistas aqui nesse post possuem fins didáticos apenas. Embora funcionem de forma adequada para serem utilizadas, elas não utilizam os recursos mais adequados para obter o melhor desempenho. Para usar na prática, existem soluções prontas e muito mais recomendadas, como por exemplo o módulo python <a href="http://docs.python.org/library/queue.html">queue</a>, que pode ser usado tanto para implementação de Filas quanto para a implementação de Pilhas.</p>
<h2>Códigos completos</h2>
<p>Abaixo, seguem os códigos completos para a Fila e para a Pilha.</p>
<h3>Fila</h3>
<pre data-lang="python"><code>
  class Fila(object):
      def __init__(self):
          self.dados = []
   
      def insere(self, elemento):
          self.dados.append(elemento)
   
      def retira(self):
          return self.dados.pop(0)
   
      def vazia(self):
          return len(self.dados) == 0
</code></pre>
<h3>Pilha</h3>
<pre data-lang="python"><code>
class Pilha(object):
    def __init__(self):
        self.dados = []
 
    def empilha(self, elemento):
        self.dados.append(elemento)
 
    def desempilha(self):
        if not self.vazia():
            return self.dados.pop(-1)
 
    def vazia(self):
        return len(self.dados) == 0
</code></pre>

<!-- wp:paragraph -->
<p>Postagem de referência:<br><a rel="noreferrer noopener" href="https://medium.com/@TDamiao/aplica%C3%A7%C3%B5es-interpretadas-e-compiladas-3a4fc0c29a61" target="_blank">Python&nbsp;Help</a>.</p>
<!-- /wp:paragraph -->