---
title: "Aplicações Interpretadas vs Compiladas"
excerpt_separator: "<!--more-->"
categories:
  - Programação
tags:
  - Aplicações
  - Python
  - Java
  - Compiladas
  - Interpretadas
---


Os interpretadores leem um código fonte de uma linguagem e os convertem em código executável.
Eles só precisam escrever, testar, corrigir, escrever, testar e distribuir. Não sendo necessário copilar.
Em muitos casos, o interpretador lê linha a linha e converter em código objeto a medida de que vai executando.



#### Compiladores



O compilador é um programa do sistema que traduz um programa escrito em alto nível para linguagem para um código equivalente da máquina do computador. Em geral não se traduz diretamente para código da máquina, mas em uma linguagem denominada: Assembly (equivalente a linguagem de baixo nível).



#### Vantagem e desvantagem



Interpretador Vantagens
`Correções e alterações são mais rápidas de realizar.
Código não precisar ser compilado.
Consomem menos memória.
Entendida rapidamente.



#### Interpretador Desvantagens



Qualquer erro no código afeta o sistema todo.
Necessita sempre ter lido o código original para ser executado.



#### Compilador Vantagens



O Código copilado é mais rápido de ser acessado
Impossibilita ou pelo menos dificulta ser quebrado e visualizado o código-fonte original.
Permite otimização do corte pelo compilador.
Compila apenas se o código estiver sem erros.



#### Compilador Desvantagens



O código passa por diversos níveis de compilação
Processo de correção, necessita que o código seja copilado novamente.
Linguagens de programação interpretadas e compiladas



#### Interpretadas - Python



Mais leve e simples para scripts pequenos e websites.
Mais dinâmico, pois permite carregar e executar trechos de código facilmente
Mais fácil para quem está começando, não tem que aprender toda uma arquitetura como no Java para criar projetos simples
Em geral, sem tanta dor de cabeça para configurar seu sistema
Mas também`
Em geral, Python é mais lento que o Java para sua execução, tendo em vista que aplicações interpretadas rodam linha a linha no momento da execução, verificando cada uma delas antes de executar o código, enquanto em linguagens compiladas o compilador analisa o código todo antes de rodar e caso não haja modificação nele a próxima vez que você for executá-lo ele será mais rápido.



#### Compiladas - Java



Facilita encontrar erros mais cedo, já que as variáveis são fortemente tipadas e isso facilita que os compiladores e IDEs mostrem os erros antes da execução.
Mas também
`As vezes parece que você precisa ser um especialista em 10 APIs para você criar um “hello world” web.
Os desenvolvedores Java costumam matar moscas usando bombas nucleares, isto é, muitas vezes um problema que seria simples de resolver com um HTML estático acaba gerando um sistema que precisa de um servidor de aplicação JEE Full Profile e 1 GB de RAM.
Não tem um lugar bom, barato e rápido para colocar seu sistema. E cada hospedagem vai ter seu jeito diferente.



#### Conclusão:



O compilador, analisa totalmente o código fonte em busca de erros léxicos ou sintáticos, de uma maneira que o programa somente será executado, se não houver nenhum erro.
Já o Interpretador, interpreta o código, e o analisa e executa linha a linha diretamente, se tudo estiver correto ele passará para a próxima linha.
Além disso, o compilador, converte o programa de uma maneira a aperfeiçoar o uso da memória. Porém, ele transforma a linguagem fonte, em outras até chegar em Assembly, o que lhe custa certo tempo.
Já interpretador apenas executa.
Com isso, observa-se que a linguagem compilada é mais rápida, do que a interpretada no momento da execução, porém pode ser uma doe de cabeça em casos que você precisa flexibilizar seu desenvolvimento. Por isso é fundamental entender qual o propósito de seu projeto ao escolher o modelo de desenvolvimento que pretende seguir.