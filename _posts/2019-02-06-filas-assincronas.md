---
title: "Post: Filas assíncronas com a Classe Queue no Python"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Paralelismo
  - Python
  - Paralellism
  - Queue
  - Fila
  - Filas
  - Queues
  - Threads
---

Filas são excelentes para que um script rode de forma eficiente, pois com elas é possível organizar as prioridades do software de forma correta. Uma das vantagens das filas é trabalhar com elas de forma assíncrona. 


No Python podemos trabalhar com Filas assíncronas através da classe `Queue`, que permite trabalharmos com uma estrutura de dados que compartilha suas informações com mais de um processo ao mesmo tempo, dentro de uma script que esteja rodando de forma multiprocesaada. Se você quiser saber mais sobre multiprocessos veja nossa postagem <a rel="noreferrer noopener" aria-label="link (abre em uma nova aba)" href="https://pythondeaaz.com.br/paralelismo-em-python-usando-concurrent-futures/" target="_blank">Paralelismo em Python usando concurrent.futures</a>.


Se soubermos utilizar os recursos de paralelismo e filas de modo correto, podemos criar scripts muito mais eficientes e completo. Por isso `Python` é considerado uma excelente linguagem para trabalhar com criação de scripts que performam com melhor qualidade e com grande escalabilidade.



Vamos criar um primeiro exemplo de filas, onde uma função irá abrir arquivos `csv's` e realizará a junção desses `csv's` em um único arquivo. Para o que aprenderemos aqui você precisará baixar um pequeno `zip` que criei com 100 arquivos `csv's` dentro, para que possamos entender melhor a execução. Baixe-o nesse <a rel="noreferrer noopener" aria-label="link (abre em uma nova aba)" href="https://pythondeaaz.com.br/wp-content/uploads/2019/01/csvs_exemplo.zip" target="_blank">link</a>. À seguir veremos a estrutura que o projeto precisa ter e o exemplo que será explicado logo após. 



### Estrutura do projeto:
```python
├── run.py
├── csvs
|   ├── csv_exemplo_0.csv
|   └── csv_exemplo_1.csv
|   └── csv_exemplo_2.csv
|   └── csv_exemplo_3.csv
|   └── ...
```


### Código exemplo 1:
```python
#-*- coding:utf-8 -*-
# encoding=utf8

from Queue import Queue
import os, csv

fila_de_arquivos = Queue(101)
estrutura_unificada = []

def adicionar_na_fila(fila_de_arquivos):
	arquivos = os.listdir('./csvs') 
	for i, arquivo in enumerate(arquivos):
		# A função put é responsável por adicionar um item à fila. Você pode adicionar uma string, list, tupla, dicionário, inteiro. Fique à vontade.
		fila_de_arquivos.put(arquivo)

def unificar_arquivo(fila_de_arquivos, estrutura_unificada):
	while True:
		try:
		# A qsize é o método que verifica o tamanho de itens que está na fila naquele momento.
		if fila_de_arquivos.qsize() == 0:
				break
			# O método get consome um item da fila, ao consumir o item, um espaço é liberado para que outro item possa ser adicionado a fila.		
			arquivo = fila_de_arquivos.get()
			with open('./csvs/%s' % arquivo) as arquivo_aberto:
				linhas_csv = csv.DictReader(arquivo_aberto, delimiter=',')
				for linha in linhas_csv:
					if not linha['nome'] == 'nome':
						estrutura_unificada.append(
							[linha['id'], linha['nome'], linha['sobrenome'], linha['idade']]
						)
		except Exception as e:
			print(e)

def salvar_unificacao(estrutura_unificada):
	with open('novo.csv', mode='w') as novo_csv:
	    n_csv = csv.writer(novo_csv, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)

	    n_csv.writerow(['id', 'nome', 'sobrenome', 'idade'])

	    for estrutura_linha in estrutura_unificada:
	    	n_csv.writerow(estrutura_linha)

if __name__ == "__main__":
	adicionar_na_fila(fila_de_arquivos)
	unificar_arquivo(fila_de_arquivos, estrutura_unificada)
	salvar_unificacao(estrutura_unificada)
```


### Entendendo as filas


Podemos perceber, que dentro desse exemplo temos uma variável chamada `fila_de_arquivos` onde é atribuído uma instância da classe `Queue`. A classe `Queue` faz com que essa variável se torne uma estrutura de dados, ou seja, ela se comportará podendo receber x valores dentro dela, cada valor atribuído ocupará uma posição de índice dentro dessa variável. Se pararmos para perceber, uma estrutura de dados como uma lista por exemplo possui dentro dela uma fila, do mesmo modo que a classe Queue faz com quem instância ela, mas existem algumas particularidades nessa classe. Veja nos tópicos à seguir quais são as particularidades:


#### Funciona de forma assíncrona


Diferente da estrutura de dados padrão a estrutura de dados da `Queue`  trabalha de modo assíncrono, ou seja, ela compartilha seus dados para vários lugares ao mesmo tempo, sem o risco de duas funções por exemplo pegarem o mesmo índice da fila, ou seja, se temos duas funções lendo essa lista, a função 1 pegará o índice que está na posição 0 da fila e a função 2 ao pedir um índice para a `Queue` receberá a posição 1, ou seja, se você possui um conjunto de dados para ser lido e quer acelerar o processo lendo esses dados de forma multiprocessada, uma função não lerá o mesmo dado que a outra, isso torna o software seguro.


#### Possui limite para não exceder a memória


Como vimos no exemplo anterior a Queue recebeu como parâmetro o valor 101, esse valor diz respeito ao tamanho máximo que uma fila comporta. Você pode colocar 50, 1000, 100000 e por aí vai. Talvez você se pergunte o que acontece que temos 100 arquivos para serem lidos e o tamanho da fila for 50. Essa é mais uma vantagem de usar filas assíncronas. Veja o próximo tópico.


#### Ficam em espera


Quando adicionamos um tamanho à fila por exemplo 50, e já adicionamos 50 índices à ela, ela irá esperar que alguém consuma 1 item da fila para desocupar, ao desocupar espaço ela irá inserir outro item na fila. 


<blockquote class="wp-block-quote"> Fique atento, pois em filas assìncronas os processos funcionam paralelamente, enquanto um processo fica enxendo a fila, o outro processo fica pegando o que está na fila e quando isso ocorre a fila esvazia, ou seja, você pega o que está na fila e abre espaço para que outro item seja posto lá.<cite>Dica do autor.</cite></blockquote>


### Métodos da classe Queue


Os métodos à seguir podem ser utilizados ao instanciarmos a classe `Queue` em nosso programa.


* `put`: Adiciona um item na fila, fazendo com que ele ocupe o espaço equivalente a 1 na fila;</li>
* `get`: Consome um item da fila, liberando espaço para um novo item ser adicionado;</li>
* `qsize`: Verifica o tamanho atual da fila;</li>
* `empty`: Verifica se a fila está vazia;</li>
* `full`: Verifica se a fila está cheia;</li>
* `task_done`: Informa quando um item da fila acabou de ser processado;</li>


Esse primeiro exemplo é composto por uma estrutura síncrona, ou seja, linear. As funções são executadas respectivamente uma após o término da outra, isso é algo comum, mas perceba que em casos como o do exemplo torna-se ruim, pois é necessário esperar cada função terminar para que a próxima inicie.



Em programas que trabalham de forma assíncrona, podemos utilizar as filas para partilhar o trabalho entre mais de uma função e assim conseguimos fazer mais de uma ação ao mesmo tempo. Veremos à seguir um exemplo utilizando as filas em conjunto com o conceito de paralelismo, assim poderemos unir os arquivos `csv's` mais rapidamente. Se ainda não leu a postagem sobre <a rel="noreferrer noopener" href="https://pythondeaaz.com.br/paralelismo-em-python-usando-concurrent-futures/" target="_blank">Paralelismo em Python usando concurrent.futures</a> fique à vontade para ler e depois voltar para esse post.


### Código exemplo 2:
```python
#-*- coding:utf-8 -*-
# encoding=utf8

from Queue import Queue
from concurrent import futures
import os, csv

fila_de_arquivos = Queue(101)
estrutura_unificada = []

def adicionar_na_fila(fila_de_arquivos):
	while True:
		arquivos = os.listdir('./csvs') 
		for i, arquivo in enumerate(arquivos):
			fila_de_arquivos.put(arquivo)

def unificar_arquivo(fila_de_arquivos, estrutura_unificada):
	while True:
		try:
			arquivo = fila_de_arquivos.get()
			
			file = './csvs/%s' % arquivo
			if os.path.isfile(file):
				try:
					with open(file) as arquivo_aberto:
						linhas_csv = csv.DictReader(arquivo_aberto, delimiter=',')
						for linha in linhas_csv:
							if not linha['nome'] == 'nome':
								estrutura_unificada.append(
									[linha['id'], linha['nome'], linha['sobrenome'], linha['idade']]
								)

					os.remove('./csvs/%s' % arquivo)
				except OSError as e:
					print("Erro no arquiv %s" % e)		
		except Exception as e:
			print(e)

		salvar_unificacao(estrutura_unificada)

def salvar_unificacao(estrutura_unificada):
	with open('novo.csv', mode='w') as novo_csv:
	    n_csv = csv.writer(novo_csv, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)

	    n_csv.writerow(['id', 'nome', 'sobrenome', 'idade'])
	    for estrutura_linha in estrutura_unificada:
	    	n_csv.writerow(estrutura_linha)

def main(fila_de_arquivos, estrutura_unificada):
	with futures.ThreadPoolExecutor(max_workers=4) as pool:
		try:
			threads = []

			threads.append(pool.submit(adicionar_na_fila, fila_de_arquivos))

			threads.append(pool.submit(unificar_arquivo, fila_de_arquivos, estrutura_unificada))
			threads.append(pool.submit(unificar_arquivo, fila_de_arquivos, estrutura_unificada))
			threads.append(pool.submit(unificar_arquivo, fila_de_arquivos, estrutura_unificada))

			futures.wait(threads, return_when='ALL_COMPLETED')

			print("[[main]] &gt;&gt; Processo finalizado")
		except Exception as e:
			print("[[main]] &gt;&gt; Um erro ocorreu. Descrição: %s" % e)

if __name__ == "__main__":
	main(fila_de_arquivos, estrutura_unificada)
```


Como podemos perceber, no exemplo 2, nós criamos uma função chamada main e dentro dela chamamos o objeto da lib concurrent.futures, para que pudessemos executar os 3 processos de forma paralela, assim nós adicionamos 4 max workers e executamos 1 vez a função de adicionar arquivos csv à fila e 3 vezes a função de unificar os arquivos, toda vez que um arquivo for adicionado à estrutura de lista unificada o script de unificação de arquivos salvará o arquivo csv com essa linha atualizada. Essa abordagem é bem simples de entender. Enquanto uma def adicona itens na lista constantemente, a outra ou as outras consomem esses itens, abrindo espaço para que novos itens possam ser colocados na fila.


O conceito de filas é bem interessante e simples, aqui está o <a rel="noreferrer noopener" aria-label="link (abre em uma nova aba)" href="https://pythondeaaz.com.br/wp-content/uploads/2019/01/fila_de_arquivos.zip" target="_blank">link</a> do projeto final para você baixar e ver como funciona o processo.
