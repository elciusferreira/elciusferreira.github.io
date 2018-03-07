---
layout: post
title:  "Análise de Proposições Políticas - Um estudo com dados de 1998 à 2016"
date:   2018-03-06 22:35:03 -0300
tags: [proposições, análise]
feature: /assets/img/propositions-analysis/cover.jpg
---

No dia 16 de maio de 2012 a [Lei de Acesso à Informação](http://www.planalto.gov.br/ccivil_03/_ato2011-2014/2011/lei/l12527.htm) entrou em vigor regulamentando o direito constitucional do cidadão ao acesso de informações produzidas ou detidas pelo Governo. Atualmente, existem portais governamentais que disponibilizam dados que possam ser analisados das mais diversas formas.

O [portal de dados abertos da Câmara](https://dadosabertos.camara.leg.br/) disponibiliza algumas formas de obtenção de informações relacionadas às proposições feitas desde o ano de 1998 até 2018. Utilizando os arquivos disponíveis pra download, resolvi realizar uma análise gráfica das informações.

Existem arquivos no formato json com informações, segundo o portal, referentes às proposições feitas nos seguintes intervalos de tempo:
* 1998 e 2002
* 2002 e 2006
* 2006 e 2010
* 2010 e 2014
* 2014 e 2018

Cada intervalo de tempo acima possui uma análise neste post e no final um estudo completo de 2002 a 2016 é feito. Apesar do portal informar que disponibiliza para download dados referentes do ano de 1998 até o ano de 2018, na prática veremos que só se disponibiliza de 2002 até o ano de 2016.

Foi feito o download dos 5 arquivos que representam os 5 intervalos de tempo listados acima. Posteriormente foram transformados em outros 5, no formato csv, por um script implementado em python que realiza o parsing.


Foram examinadas as relações entre:

* Proposições x Estados
* Proposições x Gênero
* Proposições x Temas
* Proposições x Tipo do Autor
* Proposições x Ano
* Proposições x Região
* Proposições x Tipos
* Proposições x Partidos Políticos
* Proposições x Nome do Parlamentar

## Informações técnicas
Antes de apresentar o estudo de fato, é interessante informar que todo o código implementado para tal análise se deu na linguagem de programação [Python](https://www.python.org/). Algumas bibliotecas para plotagem de gráficos foram usadas, tais como [Matplotlib](https://matplotlib.org/) e [Seaborn](https://seaborn.pydata.org/). Foi utilizada ainda [Pandas](http://pandas.pydata.org/), considerada a melhor biblioteca Python para análise de dados.

###### Todo o código documentado se encontra em um repositório no meu Github neste [link](https://github.com/elciusferreira/propositions-analysis).

## Resultados da análise das proposições entre 1998 e 2002

No geral existem 3473 proposições no arquivo correspondente à este intervalo de tempo.

#### Proposições x Estados

![98_02_Estados](/assets/img/propositions-analysis/img1.png)

Ranking dos 6 estados com mais proposições e as respectivas quantidades:

|     Estado          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| RJ                  | 414                |
| SP                  | 245                |
| RS                  | 130                |
| MG                  | 97                 |
| PR                  | 83                 |
| SC                  |  70                |

Em 1985 proposições não há informação da UF em que  proposição se origina.

#### Proposições x Gênero

![98_02_Genero](/assets/img/propositions-analysis/img2.png)

|     Gênero          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| MASCULINO           | 1383               |
| FEMININO            | 105                |

Em 1985 proposições não há informação do gênero do(a) parlamentar que propôs.

#### Proposições x Temas

Ranking dos 6 temas mais frequentes:

|     Tema            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| COMUNICAÇÕES        | 1643               |
| TRABALHO E EMPREGO  | 176                |
| DIREITO PENAL E PROCESSUAL PENAL| 161    |
| ADMINISTRAÇÃO PÚBLICA| 157               |
| TRIBUTAÇÃO          | 124                |
| VIAÇÃO E TRANSPORTES|  109               |
| EDUCAÇÃO            |  94                |

#### Proposições x Tipo do Autor


Ranking dos tipos de autores do mais frequente ao menos frequente:

|     Tipo do Autor          |  Qtd. Proposições  |
| :------------------------- |:------------------:|
| COMISSÃO PERMANENTE        | 1666               |
| DEPUTADO                   | 1488               |
| ÓRGÃO DO PODER EXECUTIVO   | 163                |
| ÓRGÃO DO PODER LEGISLATIVO | 114                |
| ÓRGÃO DO PODER JUDICIÁRIO  | 13                 |
| COMISSÃO MISTA PERMANENTE  |  9                 |
| COMISSÃO ESPECIAL          |  7                 |
| MPU - MINISTÉRIO PÚBLICO DA UNIÃO| 5            |
|COMISSÃO PARLAMENTAR DE INQUÉRITO|   4           |
|COMISSÃO DIRETORA           | 4                  |

#### Proposições x Ano

![98_02_Ano](/assets/img/propositions-analysis/img3.png)

Como observa-se, o arquivo disponibilizado pelo portal do governo como contendo informações de 1998 até 2002 só possui dados de 2002 e alguns de 2003.

#### Proposições x Região

![98_02_Regiao](/assets/img/propositions-analysis/img4.png)


Ranking:

|     Região          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SUDESTE             | 783                |
| SUL                 | 283                |
| NORDESTE            | 201                |
| CENTRO-OESTE        | 129                |
| NORTE               | 92                 |

Em 1985 proposições não há informação da região em que  proposição se origina.

#### Proposições x Tipos

![98_02_Tipos](/assets/img/propositions-analysis/img5.png)

Ranking:

|     Tipo            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PDC                 | 1678               |
| PL                  | 1480               |
| PEC                 | 108                |
| MPV                 | 82                 |
| PLP                 | 80                 |
| PRC                 | 45                 |


Legenda:

* PL = Projetos de Lei
* PDC = Projetos de Decreto Legislativo da Câmara
* PLP = Projetos de Lei Complementar
* PEC = Projetos de Emenda à Constituição
* MPV = Medidas Provisórias (MPV)

#### Proposições x Partidos Políticos

![98_02_Partidos](/assets/img/propositions-analysis/img6.png)


Ranking dos 6 partidos com mais proposições e as respectivas quantidades:

|     Partido         |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PFL                 | 507                |
| PMDB                | 164                |
| PT                  | 156                |
| PPB                 | 129                |
| PSDB                | 124                |
| PDT                 | 113                |

Em 1994 proposições não há informação do partido associado.

#### Proposições x Partidos Políticos


Ranking dos 10 deputados com mais proposições:

|     Partido         |  Qtd. Proposições  |
| :------------------ |:------------------:|
| JOSÉ CARLOS COUTINHO   | 327             |
| ENI VOLTOLINI          | 42              |
| POMPEO DE MATTOS       | 40              |
| NAIR XAVIER LOBO       | 29              |
| CRESCÊNCIO PEREIRA JR  | 28              |
| CABO JÚLIO             | 25              |
| ALBERTO FRAGA          | 24              |
| NEUTON LIMA            | 18              |
| LUIZ CARLOS HAULY      | 17              |
| JOÃO DADO              | 15              |



Média de proposições por candidato: 4.82
