# Projeto 3 - Experimentar ferramentas e coletar dados

## Objetivo

Ampliar o conhecimento de ferramentas úteis para avaliações em arquitetura de computadores executando múltiplas delas

## Especificação

Você deve conhecer algumas das ferramentas e coletar dados sobre a execução delas. Cada ferramenta tem um conjunto de tarefas a realizar. Não deixe para fazer em cima da hora pois demanda tempo. 

## Ferramentas

* [SPEC CPU 2017](https://www.spec.org/cpu2017) benchmark
* Simulador multi-core [Sniper](https://snipersim.org//w/The_Sniper_Multi-Core_Simulator)
* [Perf](https://perf.wiki.kernel.org/index.php/Tutorial) profiler
* [Parsec](https://parsec.cs.princeton.edu) benchmark
* [Rodinia](http://rodinia.cs.virginia.edu/doku.php) benchmark
* [Intel Pin](https://software.intel.com/content/www/us/en/develop/articles/pin-a-dynamic-binary-instrumentation-tool.html)
* [Dinero](https://pages.cs.wisc.edu/~markhill/DineroIV) cache simulator

## Tarefas

* **SPEC**: Executar em um computador e coletar as métricas finais de desempenho. Consultar o site do SPEC e indicar como suas métricas se comparam a outros computadores. Fique confortável com a seleção de tamanho das entradas. Entrega: sequência de comandos executados e métricas com suas comparações a outros computadores.
* **Sniper**: Instalar e executar no seu computador. Executar 3 programas pequenos (< 1 milhão de instruções cada). Entrega: sequência de comandos executados, slowdown de simulação (tempo do programa executado no simulador dividido pelo tempo do programa executando nativamente), colete e apresente algumas métricas de desempenho do coletadas pelo simulador.
* **Perf**: Execute os mesmos 3 programas anteriores e extraia as mesmas métricas de forma nativa. Entrega: Compare as métricas do Perf com as do Sniper e justifique as diferenças.
* **Parsec**: Baixar, compilar e executar. Experimente com múltiplos parâmetros de execução, em particular explorando a parte de paralelismo. Alguns programas podem não executar no seu computador. Enrega: Tabela com quais programas e parâmetros executou e quais não foi possível executar devido a erros/problemas.
* **Rodinia**: Baixar, compilar e executar 3 programas do benchmark. Se tiver hardware suficiente, rodar as múltiplas versões do programa e comparar o desempenho no mesmo computador. Entrega: Lista dos programas e versões executadas. Para múltiplas configurações do mesmo programa, indicar diferenças de desempenho.
* **Pin**: Baixar e executar algumas ferramentas de exemplo (pintool do diretório examples) utilizando os 3 programas escolhidos para o Sniper e Perf. Indicar comandos executados e resultado da execução.
* **Dinero**: Testar múltiplas configurações de caches L1, L2 e L3 para um dos programas que você utilizou anteriormente. Entrega: Múltiplas configurações exploradas e decisão sobre a melhor configuração de cache entre as testadas.

## Entrega

Entregar, através do Google Classroom, um relatório (PDF) com uma seção para cada ferramenta acima especificando os aprendizados e resultados encontrados conforme especificação. Data de entrega: 31/05/2023.


