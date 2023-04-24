---
marp: true
paginate: true
_paginate: false
footer: 'MO601 - Arquitetura de Computadores II - Rodolfo Azevedo - CC BY-SA 4.0'
headingDivider: 2
---

# Workload Design

**MO601 - Arquitetura de Computadores II**

http://www.ic.unicamp.br/~rodolfo/mo601

Rodolfo Azevedo - rodolfo@ic.unicamp.br

## Criando ou selecionando benchmarks

* Benchmarks são programas que são utilizados para avaliar o desempenho de um sistema
* Construir um benchmark requer conhecimento do sistema e do problema
* Escolhas erradas/imprecisas no processo de construção levarão a avaliações não confiáveis
* Existem muitos benchmarks disponíveis, mas nem todos são adequados para o seu problema
* É importante considerar aspectos como:
  * Tipo de compuador (desktop, servidor, embarcado, etc)
  * Comportamento dos subsistemas (memória, cache, disco, rede, etc)
  * Tipo de aplicação (processamento, I/O, etc)
  * Requisitos de memória

## Tipos de benchmarks

* Existem muitas formas de categorizar benchmarks, normalmente levando em conta o tipo de aplicação ou sistema a ser avaliado
* Quando se fala da construção de benchmarks, eles se dividem em duas categorias
  * **Benchmark sintético**: são benchmarks que são construídos para avaliar um aspecto específico do sistema, criando um programa ou utilizando partes de programas
  * **Benchmark real**: são benchmarks que são construídos para avaliar o desempenho de um sistema em um cenário real, utilizando programas reais

## Benchmark sintético

* São benchmarks que são construídos para avaliar um aspecto específico do sistema, criando um programa ou utilizando partes de programas
* Normalmente são mais fáceis de executar e de interpretar os resultados
* A execução do benchmark não produz outro resultado além das métricas de desempenho
* Pode ser burlado por otimizações de compiladores ou sistemas para conseguirem métricas melhores
* As vezes representam a única alternativa, como no caso dos microbenchmarks

## Benchmark real

* São benchmarks que são construídos para avaliar o desempenho de um sistema em um cenário real, utilizando programas reais
* Normalmente são mais difíceis de executar e de interpretar os resultados
* Otimizações de sistema ou compiladores que melhoram o desempenho do benchmark devem melhorar o desempenho de seus componentes
* Costumam ser construídos através de um conjunto de aplicações diferentes com múltiplas entradas cada
* São mais confiáveis para avaliar o desempenho de sistemas reais

## Criando benchmarks

* O espaço de possíveis programas para criar um benchmark é chamado de *workload space*
* Em alguns sistemas (tipicamente embarcados), é possível utilizar como benchmark todo o universo de software que será executado no sistema
* Para a maior parte dos sistemas, não é possível coletar todos os softwares que podem ser executados
  * Torna-se necessário criar benchmarks específicos (*reference workload*)
  * Ainda assim, esse benchmark pode ser muito grande e ele pode precisar ser reduzido (*reduced workload*)

## Workload de referência

* Apesar de não conter todos os softwares que serão executados, o *reference workload* deve conter todos os tipos de softwares que serão executados, o que torna a tarefa ainda muito complexa
* Existem inúmeros domínios de aplicações como: multimídia, computação científica, bioinformática, médica, comercial, computação geral, etc
* Mesmo restringindo para um sub-domínio, ainda é difícil construir um benchmark representativo
* Alguns benchmarks foram criados para subdomínios: SPEC CPU (computação geral), MediaBench (multimedia), BioPerf (bioinformática), PARSEC (multithread), DaCapo (Java), STAMP(memória transacional)
* Sempre que surgem novas demandas, novos benchmarks são criados

## O espaço de workloads está sempre mudando

* Otimizações de workloads para hoje podem não ser tão úteis para o futuro
* À medida que os sistemas ficam maiores, fala-se cada vez mais de sistemas projetados no passado, com compiladores antigos, definindo o destino do futuro da computação
* Atualizar sistemas e compiladores é sempre uma tarefa árdua
* O próprio critério para definição dos programas que comporão um benchmark possui subjetividade
* Como exemplo, os critérios do SPEC incluem portabilidade e manutenção do código

## Reduzindo workload

* Com muitos domínios de aplicações, o conjunto de benchmarks possíveis cresce significativamente
* Execuções baseadas em simulação ou mesmo coleta de dados dinâmicos tornam-se inviáveis
* É necessário reduzir o conjunto de benchmarks para um tamanho que seja viável
* O processo de redução do benchmark precisa ser metódico
  * Não deve ser baseado no critério "*somente o que rodou no meu computador*"
  * Nem pode ser baseado em critérios subjetivos como "*o que eu acho que é importante*"

## PCA - Principal Component Analysis

* Uma técnica de redução de dimensionalidade que pode ser utilizada para reduzir o espaço de workloads
* O processo costuma passar por 3 fases distintas:
  1. Seleção do workload de referência com **n** programas com a definição e coleta de **p** características por programa
  1. Aplicação do PCA para reduzir o espaço de **p** características para um número menor de **q** características
  1. Cluster analysis para reduzir o conjunto de **n** programas para um número menor de **m** programas

## Considerações sobre PCA

* É comum encontrar características similares em programas distintos e acreditar que eles são similares
* A parte mais crítica do processo passa a ser a definição e coleta das características, que podem ser caracterizadas como dependentes ou independentes de microarquitetura
* As características dependentes de arquitetura costumam ser mais fáceis de coletar mas são também dependentes do ambiente de execução
* As características independentes de arquitetura podem precisar de simuladores com precisão de ciclo para serem coletadas

## Hardware performance monitors

* Praticamente todos os processadores modernos possuem um conjunto de contadores de desempenho
* Monitorar esse conjunto de contadores é uma forma de coletar características dependentes de microarquitetura como CPI, hit/miss na cache, etc
* Uma forma melhor seria coletar esses mesmos contadores em múltiplas arquiteturas/processadores diferentes

## Exemplo de caracterização dependente de microarquitetura

| Característica | gzip-graphic | fasta |
|----------------|-------------:|------:|
| CPI on Alpha 21164 | 1,01 | 0,92 |
| CPI on Alpha 21264 | 0,63 | 0,66 |
| L1 D-cache misses/instrução | 1,61% | 1,90% |
| L1 I-cache misses/instrução | 0,15% | 0,18% |
| L2 cache misses/instrução | 0,78% | 0,25% |

> Os dois programas parecem iguais sobre essa ótica!

## Exemplo de caracterização independente de microarquitetura

| Característica | gzip-graphic | fasta |
|----------------|-------------:|------:|
| Data working set size (x4KB) | 46.199 | 4.058 |
| Instruction working set size (x4KB) | 33 | 79 |
| Two consecutive load accssing the same data | 0,67 | 0,30 |
| Two consecutive store acessing the same data | 0,64 | 0,05 |
| Probability of data stride in loads < 64 | 0,26 | 0,18 |
| Probability of data stride in stores < 64 | 0,35 | 0,93 |

## Características independentes de microarquitetura

* **Instruction mix**: Porcentagem de loads, stores, branches, operações de inteiros, operações de ponto-flutuante
* **ILP**: Quantidade de ILP para uma dada janela de instruções
* **Data working set size**: Número de blocos ou páginas de memória distintos acessados
* **Code footprint**: Número de blocos ou páginas de memória distintos executados
* **Branch transition rate**: Número de vezes que branches trocam de direção durante a execução
* **Stride de dados**: Distribuição de strides entre loads e stores consecutivos estática ou dinamicamente

## Simulação detalhada

* Requer um simulador com preisão de ciclos
* Por ser um software, pode coletar mais informações sobre os benchmarks
* Execução muito demorada
* Precisa executar apenas no momento da caracterização
* Costuma ser a base para coletar características independente de microarquitetura

## Completando o processo (PCA + Cluster Analysis)

* Com base nas características, a utilização de PCA permite coletar um conjunto menor de componentes onde o primeiro agrega mais características e o último menos
* Muitos pacotes de software realizam essa tarefa
* Com base nessas características, os programas são agrupados conforme o espaço de características
* A escolha do número de características também é uma decisão crítica do processo
* Pontos próximos nesse novo espaço possuem comportamentos similares
* O novo espaço também pode ser analisado procurando por locais não representados pelos benchmarks

## Plackett and Burman based workload design

* Uma técnica sistemática de redução de dimensionalidade com um número menor de simulações
  * 2c simulações para c características
* Permite a escolha das características que mais impactam o sistema
* Não entraremos em detalhe aqui, mas vale a leitura da descrição no livro

## Limitações

* Benchmarks reduzidos podem não capturar todos os comportamentos necessários
* É importante projetar os experimentos tendo em mente os parâmetros que foram utilizados para a redução dos benchmarks
* É importante também ter em mente que o espaço de workloads está sempre mudando
* Os processadores também estão evoluindo mas as características não costumam ser alteradas de forma drástica de uma geração para a próxima

