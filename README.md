# analise-telemetria-f1
Projeto da disciplina de Introdução à Ciência de Dados, no qual vamos analisar dados da Formula 1.
---
## Integrantes
* 	RENAN SINESIO ALMEIDA
*   VINICIUS ALENCAR DE MEDEIROS
*   VYNICIOS DANIEL CAETANO LOPES DA SILVA
*   YOSEF JOSEPH GONCALVES DO NASCIMENTO
---
## Abordagem

Utilizaremos a API OpenF1 https://openf1.org/ para analisar a telemetria dos carros, focando em voltas rápidas de qualificação. Nosso objetivo é identificar qual combinação de estilo de frenagem e configuração do carro resulta em maior velocidade e menor tempo de volta.

"Com foco em analisar a frenagem em uma longa reta seguida de uma curva, coletaremos dados cruciais como velocidade, pressão de freio, posição do acelerador e telemetria espacial e temporal. 
Para garantir a relevância dos nossos dados, selecionaremos especificamente as seções dos circuitos que permitam frenagens a partir da velocidade máxima dos carros, minimizando assim as variações de potência entre diferentes veículos."

---
## Objetivo

O objetivo do nosso projeto é explorar o equilíbrio da frenagem na Fórmula 1. Entendemos que uma frenagem mais agressiva permite que o carro mantenha uma velocidade superior por mais tempo, conferindo uma vantagem competitiva. No entanto, essa manobra desafia os limites dos pneus dianteiros devido à transferência de massa inercial, podendo levar ao subesterço (understeer), onde o carro tem dificuldade em fazer a curva.
Por outro lado,na realização da curva, pilotos podem induzir o sobresterço (oversteer) utilizando o acelerador para gerenciar a potência e a tração traseira, otimizando o controle. Nosso projeto visa quantificar e correlacionar essas variáveis para identificar estratégias de frenagem mais eficazes.
