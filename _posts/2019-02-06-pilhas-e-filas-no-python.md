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

Você pode não perceber, mas boa parte dos programas que você usa no dia-a-dia utilizam internamente os tipos abstratos de dados chamados filas e pilhas. Eles são chamados dessa forma porque representam uma estrutura de dados com operações associadas que definem um certo comportamento. Eles são muito úteis para o programador pois podem ser utilizados em diversas situações e têm um grande poderde simplificar algoritmos. A seguir, explicarei cada uma dessas estruturas e demonstrarei como poderíamos implementá-las em Python.


## Filas


Tenho certeza que você já sabe como uma fila funciona. Pense na fila que você pega toda vez que vai ao supermercado. Para que você seja atendido, é preciso que todas as pessoas que estiverem na sua frente na fila sejam atendidas ou desistam para que você seja atendido, certo? Por isso, podemos dizer que a idéia da fila é que o último a entrar na fila seja o último a sair.



```
                                     _________
                                    | o caixa |
------------------------------------|_________|
 o    ~o    @    &     Q    0    O     0
/|\    []  {0\  /|\   /|\  /||  /-\   /0|
/ \    |\   |\  / \    |\  /|   |-|   / \
você   p6   p5  p4     p3  p2    p1   p0
-------------------------------------------
```


No exemplo acima, é preciso que p0, p1, p2, p3, p4, p5 e p6 sejam atendidas para que seja a sua vez de passar as compras e pagar por elas. Uma estrutura de dados Fila funciona da mesma maneira. Uma fila é uma estrutura utilizada especificamente para armazenamento temporário de dados na memória. Diferentemente de uma lista, que também serve para esse fim, uma fila possui regras quanto a qual elemento será retirado e onde será inserido um novo elemento. Em uma lista, é possível inserir elementos em qualquer posição e retirar quaisquer elementos, não importando sua posição. Em uma fila, os novos elementos que são inseridos são sempre posicionados ao final dela. Quando se faz a retirada de um elemento de uma fila, sempre iremos retirar o elemento que há mais tempo está nela (o primeiro). Imagine um servidor Webque é capaz de atender a, no máximo, 2 requisições simultâneas. O que acontece quando chega uma terceira requisição no momento em que o servidor já está ocupado atendendo a 2 requisições? A solução mais óbvia seria colocar a nova requisição em uma área de espera. Assim, quando o servidor terminar de atender uma das atuais 2 requisições, ele poderá retirar a nova requisição da área de espera e atendê-la. E se, enquanto o servidor estiver ocupado atendendo a 2 requisições, chegarem em sequência 5 novas requisições?



```
   ______              
  |  r0  |       [ r6  r3]
  |  r1  |       [  r5   ]
  |______|       [r4  r2 ]
    /  \  
Servidor Web    Área de espera
```

  

O servidor poderia colocar as novas requisições em uma área de espera, e sempre que houver disponibilidade, retirar uma de lá e processá-la, até que não hajam mais requisições a serem processadas. A solução é boa, mas para ser justo com as solicitações que chegam dos usuários, o servidor deve processar primeiro as que já estão esperando há mais tempo, correto? Assim, o melhor a se fazer é utilizar uma filapara armazenar as requisições que estão em espera.




```
        ______    
       |  r0  |           
       |  r1  |      saída  -----------------------  entrada
       |______|      <----   r2  r3  r4  r5  r6     <------
         /  \               -----------------------
     Servidor Web                 Fila de espera
```


Dessa forma, a requisição que está há mais tempo esperando é a primeira a sair da fila quando o servidor tiver disponibilidade.


### Implementando uma fila


Uma fila nada mais é do que uma estrutura de armazenamento com políticas de ordem de entrada e saída de elementos. Assim, ela pode ser implementada usando uma lista, por exemplo. Como poderíamos fazer? Sabemos que as listas oferecem alguns métodos conhecidos para inserção/remoção de elementos:


* `append(elemento)`: adiciona `elemento` ao final da lista;
* `insert(índice, elemento)`: insere `elemento` após a posição `índice`;
* `pop(índice)`: remove e retorna o `elemento` contido na posição `índice`.


Para inserir elementos, podemos usar o método `append()`, que insere um elemento ao final de uma lista. Para a retirada de elementos, podemos utilizar o método `pop(x)`, que retira e retorna um elemento da posição `x`. Em se tratando de uma fila em que estamos inserindo elementos no final, de qual posição devemos retirar os elementos? Acertou quem pensou “da primeira”. Isso mesmo vamos remover o primeiro elemento utilizando `pop(0)`. Veja:


```console
>>> fila = [10, 20, 30, 40, 50]
>>> fila.append(60)  # insere um elemento no final da fila
>>> print fila
[10, 20, 30, 40, 50, 60]
>>> print fila.pop(0) # remove o primeiro elemento da lista
10
>>> print fila
[20, 30, 40, 50, 60]
>>> print fila.pop(0) # remove o primeiro elemento da lista
20
>>> print fila
[30, 40, 50, 60]
>>> print fila.pop(0) # remove o primeiro elemento da lista
30
>>> print fila
[40, 50, 60]
```


Você deve estar se perguntando: “e se eu fizesse o contrário, inserindo no início e removendo do final, funcionaria também como uma fila?” Sim, funcionaria. Pois, da mesma forma, teríamos a política do primeiro a entrar, primeiro a sair também conhecida como First-In, First-Out, ou simplesmente FIFO. Agora, para criar uma forma consistente de usar filas em Python, vamos criar uma classe para encapsular as operações da `fila`. Podemos definir uma classe Filaque internamente tenha uma lista representando o local onde serão armazenados os elementos. Essa classe deverá ter dois métodos principais:

* `insere(elemento)`: recebe como entrada um elemento a ser inserido na fila.
* `retira()`: remove um elemento da fila e o retorna para o chamador.

Complete a implementação de fila abaixo, de acordo com o que foi explicado acima. O código completo se encontra no final deste texto, para que você possa comparar.


```python
class Fila(object):
    def __init__(self):
        self.dados = []
 
    def insere(self, elemento):
        __________________________________
 
    def retira(self):
```


Tendo a classe acima definida em um arquivo fila.py, poderíamos importar o módulo e usar tal classe:



```console
>>> import fila
>>> f = fila.Fila()
>>> f.insere(10)
>>> f.insere(20)
>>> f.insere(30)
>>> print f.retira()
10
>>> print f.retira()
20
```



Importante: segundo a própria documentação oficial Python, uma lista não é a estrutura mais recomendada para a implementação de uma fila, porque a inserção ou remoção de elementos do início da lista é lenta, se comparada à inserção/remoção do final da lista. Assim, é sugerido que seja usado um deque (collections.deque).


#### Só isso?


Não, nós vimos apenas as filas “comuns”. Voltando ao exemplo da fila do supermercado, imagine que você está chegando aos caixas e ainda não decidiu qual deles vai usar. Aí você vê que o caixa de atendimento preferencial para idosos/gestantes/deficientes possui apenas 3 pessoas na fila, enquanto que os outros caixas têm filas com no mínimo 10 pessoas. Como o caixa não é exclusivo para idosos, você vai lá e entra na fila. Outras pessoas percebem a sua “sagacidade” (:P) e fazem o mesmo. Fica tudo certo até que chega um idoso para entrar na fila e todas as pessoas que estão na fila são obrigados a ceder sua vez para o idoso. E eis que chega o clube da terceira idade inteiro para ser atendido logo em seguida. O que acontece? As pessoas que estão na fila cedem sua vez para os idosos, e assim, seu atendimento vai sendo postergado cada vez mais. Enfim, esse é um exemplo de uma fila de prioridades. Elementos (as pessoas) que possuem maior prioridade, saem antes da fila. Se quiser saber mais, veja aqui.


## Pilhas


Assim como as filas, aposto que você sabe exatamente como funciona uma pilha. Pense em uma pilha de papéis sobre uma mesa. Se você precisar adicionar um papel a essa pilha, você o adiciona sobre a pilha, ou seja, no topo dela, certo? E quando vai retirar um papel da pilha, você começa pelo que estiver no topo, certo? Ou seja, diferentemente da fila (FIFO), em uma pilha o último a entrar nela, é o primeiro a sair (Last-In, First-Out — LIFO). Veja abaixo uma ilustração de como funciona uma pilha. No primeiro item da ilustração (1), temos uma pilha composta por 5 elementos, que foram inseridos cronologicamente na seguinte ordem: p0, p1, p2, p3, e, por fim, p4. A segunda parte da ilustração (2) mostra o estado da pilha p após ter sido realizada a inserção de um novo elemento (p5). A terceira parte (3) mostra a pilha p após haver a retirada de um elemento. Como você pode ver, o elemento retirado foi o último a ter sido inserido (p5). Na última parte da ilustração (4), é apresentada mais uma retirada de elemento da pilha, desta vez p4. Se houvessem mais operações de retirada, teríamos a retirada, em ordem, dos elementos: p3, p2, p1 e p0.


```
|          |    |----p5----|    |          |    |          |
|----p4----|    |----p4----|    |----p4----|    |          |
|----p3----|    |----p3----|    |----p3----|    |----p3----|
|----p2----|    |----p2----|    |----p2----|    |----p2----|
|----p1----|    |----p1----|    |----p1----|    |----p1----|
|----p0----|    |----p0----|    |----p0----|    |----p0----|
============    ============    ============    ============
  Pilha p       p.insere(p5)     p.retira()      p.retira()
    (1)             (2)              (3)            (4)
```


Tranquilo, né? O que você deve lembrar sobre as pilhas é que ela usa uma política LIFO (Last-In, First-Out) para inserção/retirada de elementos.



### Onde as pilhas são usadas?


Talvez a mais famosa utilização de pilhas em computação esteja no gerenciamento de chamadas de função de um programa. Uma pilha pode ser usada para manter informações sobre as funções de um programa que estejam ativas, aguardando por serem terminadas. Considere o seguinte exemplo:


```python
def ola():
    print "olá, "
    mundo()
 
def mundo():
    print "mundo!"
 
def olamundo():
    ola()
 
olamundo()
```


A primeira função a ser chamada é a `olamundo()`, que por sua vez chama a função `ola()`, então a função `olamundo()` é empilhada, pois seu término depende do término da função `ola()`. Essa, por sua vez, chama a função `mundo()` e é empilhada. Ao terminar a execução da função `mundo()`, a função ola() é desempilhada e sua execução termina de onde havia parado (chamada à função mundo()). Como não há mais nada a ser executado nessa função, sua execução termina, e a função `olamundo()`é desempilhada e sua execução continua, encerrando assim o programa.


```python
                 ola()
olamundo()  -->  olamundo()  --> olamundo() -->   Fim do programa.
```


Outra utilização de pilhas é a verificação do balanceamento de parênteses. Como saber se os seguintes parênteses estão balanceados, isto é, se para cada abre-parênteses, existe um fecha-parênteses correspondente?



```
(((((((((((((((((()()()()))))))())))()))()))()))((()))))
```


Uma forma bem simples de resolver esse problema é ler a sequência de parênteses, um por um e, a cada abre-parênteses que encontrarmos, vamos empilhá-lo. Quando encontrarmos um fecha-parênteses, devemos desempilhar um abre-parênteses, pois encontramos um fecha-parênteses correspondente a ele. Assim, ao final da avaliação da sequência acima, se ela estiver balanceada corretamente, não restarão elementos na pilha. Vejamos um exemplo mais simples:


```
(())()

                (
Pilha       (   (   (       (

Leitura     (   (   )   )   (   )   FIM
```


Repare agora em uma sequência desbalanceada:



```
(())(

                (
Pilha       (   (   (       (   (

Leitura     (   (   )   )   (   FIM
```


Perceba que a leitura de parênteses da entrada terminou, mas a pilha não estava mais vazia.



### Implementação


Agora eu lhe pergunto: o que muda da implementação da fila para a implementação da pilha? A diferença é pouca, mas é muito importante. Assim como para as filas, para a implementação de pilhas podemos utilizar uma lista como estrutura para armazenamento dos dados. Basta agora definir como será o funcionamento:

1. Iremos inserir e retirar elementos do início da lista?
2. Ou iremos inserir e retirar elementos do final da lista?

Sabendo que em Python a inserção e remoção de elementos no final de uma lista é menos custoso do que fazer as mesmas operações no início dela, vamos adotar a segunda opção. Então, complete o código abaixo e teste em seu computador.


```python
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
```


O programa acima, se implementado corretamente, deverá mostrar o seguinte resultado na tela:


```
40 30 20 10
```


Para adicionar um elemento no final de uma lista, basta usar o método `append()`. E para remover o último elemento da lista? `.pop(tamanho_da_lista-1)` é o que devemos fazer. E para obter o tamanho da lista, podemos usar a função `len()`. Então:


```python
def desempilha(self):

    return self.dados.pop(len(dados)-1)
```


Ou então, podemos usar `self.dados.pop(-1)`. O acesso ao índice `-1` é a forma pythônica de se referir ao último elemento de uma sequência.


```python
def desempilha(self):
    return self.dados.pop(-1)
```


### Mais alguma operação?


Outra operação fundamental que deve estar disponível em uma Pilha, é um método que retorne um booleano indicando se a pilha está vazia. Um jeito bem simples seria usando a builtin `len()` sobre a nossa lista interna `self.dados` e verificando se ela retorna `0` como resultado.


```python
def vazia(self):
    return len(self.dados) == 0
```


## Finalizando…


Tanto a fila quanto a pilha são estruturas importantes pra caramba e sua implementação deve fornecer um bom desempenho, visto que elas são amplamente usadas nos programas que compõem o nosso dia-a-dia. As implementações vistas aqui nesse post possuem fins didáticos apenas. Embora funcionem de forma adequada para serem utilizadas, elas não utilizam os recursos mais adequados para obter o melhor desempenho. Para usar na prática, existem soluções prontas e muito mais recomendadas, como por exemplo o módulo python queue, que pode ser usado tanto para implementação de Filas quanto para a implementação de Pilhas.


## Códigos completos


Abaixo, seguem os códigos completos para a Fila e para a Pilha.


### Fila

```python
class Fila(object):
      def __init__(self):
          self.dados = []
   
      def insere(self, elemento):
          self.dados.append(elemento)
   
      def retira(self):
          return self.dados.pop(0)
   
      def vazia(self):
          return len(self.dados) == 0
```

### Pilha

```python
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
```