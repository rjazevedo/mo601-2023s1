---
marp: true
paginate: true
_paginate: false
footer: 'MO601 - Arquitetura de Computadores II - Rodolfo Azevedo - CC BY-SA 4.0'
headingDivider: 2
---
# Caches

**MO601 - Arquitetura de Computadores II**

http://www.ic.unicamp.br/~rodolfo/mo601

Rodolfo Azevedo - rodolfo@ic.unicamp.br

## Por que precisamos de cache?

* Acelera, de forma transparente, o acesso à memória
* Múltiplos níveis: L1, L2, L3
* Nível L1 dividido em dois
  * L1-I: instruções
  * L1-D: dados
* Demais níveis são unificados

## Qual o tamanho da cache em um sistema ideal?

## Organização básica

![](cache-hierarquia-basica.png)

## Multi-core - surge a necessidade de coerência

![](cache-multicore-coerencia-l2-l3.png)


## Antecipando a coerência

![](cache-multicore-coerencia-l1-l2.png)

## Particionando a L2

![](cache-multicore-duas-l2.png)

## Questões importantes

* Cache inclusiva vs exclusiva
* Leituras parciais
  * Primeiro o dado que o processador precisa
  * Afeta a ordem de leitura da memória
* Write buffer
  * Atrasa a escrita na memória
  * Acelera a escrita na cache
* Write-through vs write-back  

## Memória Virtual

  * Endereço Físico
  * Endereço Virtual
  * Página
  * TLB
  * Alias virtual
  * Ordem de tradução
    * Antes da cache
    * Após a cache

## Mapeamento de endereço virtual para físico

![](memoria-virtual-address-translation-table.png)

## Estrutura interna

![w:1000](cache-estrutura-interna.png)

## Múltiplas vias (ways)

![](cache-multi-ways.png)

## Organização real

![](cache-organizacao-real.png)

## Pipeline para acesso paralelo

![](cache-pipeline-paralelo.png)

## Pipeline para acesso serial

![](cache-pipeline-serial.png)

## Lookup-free caches

  * Suporta mais de um acesso em andamento
    * Miss Status Holding Registers (MSHR)
  * Enquanto está resolvendo um miss, executa outro acesso (Hit ou Miss)
    * Miss primário: primeiro miss em um bloco de cache
    * Miss secundário: miss subsequente em um bloco de cache
    * Stall por miss estrutural: miss extra por falta de recurso de hardware

## Outros conceitos

* Multiport
* Multibank

## Considerações sobre cache de instruções

* Multiport vs single port
* Lookup free vs blocking
* Associatividade
