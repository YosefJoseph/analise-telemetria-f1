# analise-telemetria-f1
Projeto da disciplina de Introdução à Ciência de Dados, no qual vamos analisar dados da Formula 1.
---
## Integrantes
* 	RENAN SINESIO ALMEIDA
*   VINICIUS ALENCAR DE MEDEIROS
*   VYNICIOS DANIEL CAETANO LOPES DA SILVA
*   YOSEF JOSEPH GONCALVES DO NASCIMENTO
---
## O conjunto de dados
Foi gerado um arquivo .csv para cada etapa com as velocidades médias de cada piloto nas curvas selecionadas, em km/h. 
---
## O Processo de coleta
Cada curva foi selecionada a partir da escolha manual após utilizarmos um piloto como exemplo, selecionando a área que compreenda a curva.
Para garantir a avaliação de forma similar a cada piloto, foram selecionadas suas voltas mais rápidas em sessões de qualificação, padronizando assim cada volta como o desempenho máximo demonstrado pelo piloto e eliminando fatores externo como peso de combustível, desgaste dos pneus e carga da bateria ( completamente carregada, sem acarretar em perda de desempenho do motor principal).
Para criar cada gráfico e selecionar as curvas, foram unidos dois endpoints do API: o da localização e o da telemetria, sendo reindexados com base no tempo, e depois interpolados. Com isso, é criado um gráfico de pontos no qual cada ponto é associado a uma velocidade, e podemos selecionar curvas de alta, média e baixa velocidade.
Após a delimitação da área de cada curva, criamos o gráfico para cada área, para validar que a área compreende somente a curva desejada, sem incluir outras partes do circuito, que podem alterar a velocidade a ser calculada.
A velocidade de cada piloto é calculada a partir da distância euclidiana entre cada ponto: Primeiro verificamos qual a distancia entre cada ponto em uma volta completa do piloto exemplo. Depois, somamos essas distâncias e dividimos pela distância real do circuito, obtendo uma escala da distância arbitrária da API para a distância real do circuito, em km. Depois, para cada curva, é calculada a distância total do trajeto, e tal distância é dividida pelo tempo que o piloto gastou nesse setor, obtendo assim uma velocidade média da curva, em km/h.
Esse processo é repetido em cada sessão de qualificação, para cada piloto e para cada curva selecionada.
Ao todo, foram selecionadas 88 curvas, divididas em 17 sessões. Cada sessão tem 20 pilotos.
Houve uma tentativa de abordar cada curva por meio de associação a uma função e utilizando o conceito de curvatura, mas foi descartado porque cada trajetória que temos é de um piloto específico, e como podem existir diferenças nas trajetórias de cada piloto, a avaliação poderia ser desigual.
O método de seleção atual enfrenta dificuldades para circuitos com trajetórias próximas, como Jeddah, Monte Carlo e Suzuka, este último tendo um setor que passa por baixo de outro.
Houve também alguns pilotos que não tiveram dados coletados na sessão, como Ollie Bearman em Melbourne, Yuki Tsunoda em Imola e George Russell em Miami, seja por não terem terminado voltas suficientes, seja por falha técnica.

## Descrição

Cada .csv corresponde a uma sessão de qualificação, e contem as colunas driver_number,full_name,name_acronym,team_name, e curva n:

driver_number se refere ao número que cada piloto utiliza como referência, e é mais útil para filtrar cada piloto.

full_name é o nome de cada piloto, contendo nome e sobrenome.

name_acronym é a abreviação do nome de cada piloto, composta de 3 letras.

team_name é a equipe a qual o piloto faz parte.

curva n é a velocidade média, em km/h, do piloto na n-ésima curva selecionada.

Por exemplo, no .csv de Hungaroring temos uma primeira linha como:

1,Max VERSTAPPEN,VER,Red Bull Racing,168.976559865075,152.2973837574405,167.92158761155343,208.0145178703163,269.15155887391904

1 é o número utilizado pelo piloto.

Max VERSTAPPEN é o nome e sobrenome do piloto.

VER é a abreviação do nome utilizada pelo piloto.

Red Bull Racing é a equipe a qual o piloto faz parte.

168.976559865075 é a velocidade média na primeira curva selecionada.
152.2973837574405 é a velocidade média na segunda curva selecionada.
167.92158761155343 é a velocidade média na terceira curva selecionada.
208.0145178703163 é a velocidade média na quarta curva selecionada.
269.15155887391904 é a velocidade média na quinta curva selecionada.

## Para uma futura análise dos dados

Podemos analisar a dispersão das velocidade para cada curva, verificando quais pilotos apresentam desempenho favorável a quais tipos de curva.
É possível verificar agrupamentos de pilotos que se dedicam a ter um desempenho melhor em determinado tipo de curva.
É possível observar a evolução de cada carro/piloto ao longo da temporada em relação aos demais.
Para uma análise mais completa, é necessário verificar a posição final de qualificação de cada piloto, e também fatores climáticos como chuva no dia da qualificação ou no dia da seguinte, impactando o ajuste dos carros.
Com base nos dados, é possível estimar a posição de largada de cada piloto utilizando regressão linear.
