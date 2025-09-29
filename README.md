# Análise de Telemetria de Curvas na Fórmula 1
Projeto da disciplina de Introdução à Ciência de Dados, no qual vamos analisar dados da Formula 1.
---
## Integrantes
* 	RENAN SINESIO ALMEIDA
*   VINICIUS ALENCAR DE MEDEIROS
*   VYNICIOS DANIEL CAETANO LOPES DA SILVA
*   YOSEF JOSEPH GONCALVES DO NASCIMENTO
---
## O conjunto de dados

Foi gerado um arquivo .csv para cada etapa desde o começo do ano até a pausa de verão com as velocidades médias de cada piloto nas curvas selecionadas, em km/h, além da fase de qualificação (Q1,Q2 ou Q3) na qual o piloto marcou sua melhor volta, e sua posição final na qualificação. Ao todo foram gerados arquivos para 17 etapas e para cada um dos 20 pilotos na sessão foi calculada a velocidade média em 88 curvas selecionadas.

---
## O Processo de coleta

Foi utilizada a API Openf1.org

Cada curva foi selecionada a partir da escolha manual após utilizarmos um piloto como exemplo, selecionando a área que compreenda a curva.

Para garantir a avaliação de forma similar a cada piloto, foram selecionadas suas voltas mais rápidas em sessões de qualificação, padronizando assim cada volta como o desempenho máximo demonstrado pelo piloto e eliminando fatores externo como peso de combustível, desgaste dos pneus e carga da bateria ( completamente carregada, sem acarretar em perda de desempenho do motor principal).

Para criar cada gráfico e selecionar as curvas, foram unidos dois endpoints do API: o da localização e o da telemetria, sendo reindexados com base no tempo, e depois interpolados. Com isso, é criado um gráfico de pontos no qual cada ponto é associado a uma velocidade, e podemos selecionar curvas de alta, média e baixa velocidade.

Após a delimitação da área de cada curva, criamos o gráfico para cada área, para validar que a área compreende somente a curva desejada, sem incluir outras partes do circuito, que podem alterar a velocidade a ser calculada.

A velocidade de cada piloto é calculada a partir da distância euclidiana entre cada ponto: Primeiro verificamos qual a distancia entre cada ponto em uma volta completa do piloto exemplo. Depois, somamos essas distâncias e dividimos pela distância real do circuito, obtendo uma escala da distância arbitrária da API para a distância real do circuito, em km. Depois, para cada curva, é calculada a distância total do trajeto, e tal distância é dividida pelo tempo que o piloto gastou nesse setor, obtendo assim uma velocidade média da curva, em km/h.

Esse processo é repetido em cada sessão de qualificação, para cada piloto e para cada curva selecionada.

Ao todo, foram selecionadas 88 curvas, divididas em 17 sessões. Cada sessão tem 20 pilotos.

Houve uma tentativa de abordar cada curva por meio de associação a uma função e utilizando o conceito de curvatura, mas foi descartado porque cada trajetória que temos é de um piloto específico, e como podem existir diferenças nas trajetórias de cada piloto, a avaliação poderia ser desigual.

O método de seleção atual enfrenta dificuldades para circuitos com trajetórias próximas, como Jeddah, Monte Carlo e Suzuka, este último tendo uma setor que passa por baixo de outro.

Houve também alguns pilotos que não tiveram dados coletados na sessão, como Ollie Bearman em Melbourne e Yuki Tsunoda em Imola, ambos por terem se envolvido em acidentes durante a qualificação e George Russell em Miami, cujo carro estava com problemas no localizador do gps, resultando em um dataframe vazio quando tentamos verificar sua posição durante toda a qualificação.

## Descrição

Cada .csv corresponde a uma sessão de qualificação, e contem as colunas driver_number,full_name,name_acronym,team_name,position,Etapa e curva n:

driver_number se refere ao número que cada piloto utiliza como referência, e é mais útil para filtrar cada piloto.

full_name é o nome de cada piloto, contendo nome e sobrenome.

name_acronym é a abreviação do nome de cada piloto, composta de 3 letras.

team_name é a equipe a qual o piloto faz parte.

position é a classificação do piloto ao final da qualificação.

Etapa é a fase da qualificação na qual a volta mais rápida do piloto foi marcada, variando entre (Q1, Q2 e Q3).

curva n é a velocidade média, em km/h, do piloto na n-ésima curva selecionada.

Por exemplo, no .csv de Hungaroring temos uma primeira linha como:

1,Max VERSTAPPEN,VER,Red Bull Racing,8,Q2,168.976559865075,152.2973837574405,167.92158761155343,208.0145178703163,269.15155887391904

1 é o número utilizado pelo piloto.

Max VERSTAPPEN é o nome e sobrenome do piloto.

VER é a abreviação do nome utilizada pelo piloto.

Red Bull Racing é a equipe a qual o piloto faz parte.

8 é a classificação do piloto na qualificação.

Q2 é a fase da qualificação na qual a volta mais rápida foi realizada.

168.976559865075 é a velocidade média na primeira curva selecionada.

152.2973837574405 é a velocidade média na segunda curva selecionada.

167.92158761155343 é a velocidade média na terceira curva selecionada.

208.0145178703163 é a velocidade média na quarta curva selecionada.

269.15155887391904 é a velocidade média na quinta curva selecionada.

---
## Dificuldades e Limitações:

Cada curva é delimitada apenas pela velocidade média de um piloto em seu comprimento. Poderiam ser adicionados outros fatores como ponto de frenagem, velocidades de entrada, saída e mínima, ou ainda, desaceleração ou acelerações médias. Todas essas variáveis podem contribuir para a caracterização de cada curva e o consequente agrupamento utilizando o Kmeans.

As curvas são selecionadas por meio do recorte da área do circuito, demandando visualização e estimativa para as selecionar, além de ser um processo limitado e pouco escalável. Além disso, é um processo que enfrenta dificuldades quando um circuito possui passagens próximas, como em Jeddah e Monte Carlo, ou que se cruzam, como em Suzuka.

O modelo de regressão linear é básico, levando em consideração somente a velocidade média das curvas selecionadas, o que resulta em etapas com previsibilidade variada, mesmo em um circuitos iguais. O uso de regressão linear múltipla pode melhorar a previsibilidade, além do uso da categorização das curvas. 

Em razão de diversos motivos, como acidentes ou falhas técnicas, certos pilotos como Ollie Bearman em Melbourne e Yuki Tsunoda em Imola e George Russell em Miami não foram avaliados pois seus dataframes de posição estão vazios.


## Google drive com os .csv:

https://drive.google.com/drive/folders/1wugaWdI3Cy4_QX465KNFFWp5y6M6zwhj?usp=sharing
