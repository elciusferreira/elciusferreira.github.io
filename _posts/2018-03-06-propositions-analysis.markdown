---
layout: post
title:  "Análise de Proposições Políticas - Um estudo com dados de 2002 à 2016"
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

## Todo o código documentado se encontra em um repositório no meu Github neste [link](https://github.com/elciusferreira/propositions-analysis).


# Resultados da análise das proposições entre 2010 e 2014

Verificando o conteúdo do arquivo que, segundo o portal da Câmara, corresponde ao intervalo de 2010 a 2014, temos que existem 11307 proposições.

### Proposições x Estados

![10_14_Estados](/assets/img/propositions-analysis/img19.png)

Ranking dos 6 estados com mais proposições e as respectivas quantidades:

|     Estado          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SP                  | 1360               |
| RJ                  | 864                |
| MG                  | 798                |
| PB                  | 548                |
| RS                  | 537                |
| SC                  | 476                |

Em 2448 proposições não há informação da UF em que  proposição se origina.

### Proposições x Gênero

![10_14_Genero](/assets/img/propositions-analysis/img20.png)

|     Gênero         |  Qtd. Proposições  |
| :------------------|:------------------:|
| MASCULINO          | 7922               |
| FEMININO           | 939                |

Em 2446 proposições não há informação do gênero do(a) parlamentar que propôs.

### Proposições x Temas

Ranking dos 6 temas mais frequentes:

|     Tema            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| COMUNICAÇÕES        | 1477               |
| TRIBUTAÇÃO          | 657                |
| TRABALHO E EMPREGO  | 649                |
| ADMINISTRAÇÃO PÚBLICA| 635               |
| HOMENAGENS E DATAS COMEMORATIVAS| 487    |
| EDUCAÇÃO            | 480                |
| DIREITOS HUMANOS, MINORIAS E CIDADANIA   |  480            |

### Proposições x Tipo do Autor

Ranking dos tipos de autores do mais frequente ao menos frequente:

|     Tipo do Autor          |  Qtd. Proposições  |
| :------------------------- |:------------------:|
| DEPUTADO                   | 8861               |
| COMISSÃO PERMANENTE        | 1487               |
| ÓRGÃO DO PODER LEGISLATIVO | 524                |
| ÓRGÃO DO PODER EXECUTIVO   | 229                |
| ÓRGÃO DO PODER JUDICIÁRIO  | 86                 |
| COMISSÃO DIRETORA          |  39                |
| COMISSÃO MISTA PERMANENTE  |  17                |
| COMISSÃO ESPECIAL          | 15                 |
| MPU - MINISTÉRIO PÚBLICO DA UNIÃO  | 15         |
| COMISSÃO PARLAMENTAR DE INQUÉRITO  | 14         |
| COMISSÃO PARLAMENTAR MISTA DE INQUÉRITO | 6     |
| COMISSÃO EXTERNA           | 6                  |
| DPU - DEFENSORIA PÚBLICA DA UNIÃO | 4           |
| COMISSÃO MISTA ESPECIAL    | 3                  |
| COMISSÃO PERMANENTE DO SENADO FEDERAL| 1        |

### Proposições x Ano

![10_14_Ano](/assets/img/propositions-analysis/img21.png)

Ranking:

|     Ano             |  Qtd. Proposições  |
| :------------------ |:------------------:|
| 2011                | 4011               |
| 2013                | 3115               |
| 2012                | 2433               |
| 2014                | 1744               |


### Proposições x Região

![10_14_Regiao](/assets/img/propositions-analysis/img22.png)


Ranking:

|     Região          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SUDESTE             | 3297               |
| NORDESTE            | 2355               |
| SUL                 | 1398               |
| CENTRO-OESTE        | 1126               |
| NORTE               | 683                |

Em 3297 proposições não há informação da região em que  proposição se origina.

### Proposições x Tipos

![10_14_Tipos](/assets/img/propositions-analysis/img23.png)

Ranking:

|     Tipo            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PL                  | 8327               |
| PDC                 | 1667               |
| PLP                 | 455                |
| PEC                 | 451                |
| PRC                 | 268                |
| MPV                 | 139                |


Legenda:

* PL = Projetos de Lei
* PDC = Projetos de Decreto Legislativo da Câmara
* PLP = Projetos de Lei Complementar
* PEC = Projetos de Emenda à Constituição
* MPV = Medidas Provisórias (MPV)
* PRC = Projetos de Resolução da Câmara  

### Proposições x Partidos Políticos

![10_14_Partidos](/assets/img/propositions-analysis/img24.png)


Ranking dos 6 partidos com mais proposições e as respectivas quantidades:

|     Partido         |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PT                  | 1257               |
| PMDB                | 1182               |
| PSDB                | 948                |
| PSD                 | 743                |
| DEM                 | 646                |
| PSB                 | 588                |

Em 2448 proposições não há informação do partido associado.

### Proposições x Nome do Parlamentar


Ranking dos 10 deputados com mais proposições:

|     Nome do Parlamentar         |  Qtd. Proposições  |
| :-------------------------------|:------------------:|
| WELITON PRADO                   | 172                |
| MAJOR FÁBIO                     | 169                |
| CARLOS BEZERRA                  | 159                |
| ONOFRE SANTO AGOSTINI           | 132                |
| ROMERO RODRIGUES                | 100                |
| LAERCIO OLIVEIRA                | 98                 |
| SANDRA ROSADO                   | 93                 |
| RICARDO IZAR                    | 91                 |
| ERIKA KOKAY                     | 89                 |
| SANDES JÚNIOR                   | 84                 |



Média de proposições por candidato: _15.38 proposições_.

## Para mais informações de cada comparação mostrada acima, basta acessar meu repositório no Github com a análise e o código usado para processar os dados de 2010 a 2014 neste [link](https://github.com/elciusferreira/propositions-analysis/blob/master/analise_proposicoes10-14.ipynb).  


# Resultados da análise das proposições entre 2006 e 2010

Verificando o conteúdo do arquivo que, segundo o portal da Câmara, corresponde ao intervalo de 2006 a 2010, temos que existem 12781 proposições.

### Proposições x Estados

![06_10_Estados](/assets/img/propositions-analysis/img13.png)

Ranking dos 6 estados com mais proposições e as respectivas quantidades:

|     Estado          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SP                  | 1656               |
| RJ                  | 847               |
| MG                  | 703                |
| RS                  | 517                |
| BA                  | 401                |
| MT                  | 392                |

Em 4319 proposições não há informação da UF em que  proposição se origina.

### Proposições x Gênero

![06_10_Genero](/assets/img/propositions-analysis/img14.png)

|     Gênero         |  Qtd. Proposições  |
| :------------------|:------------------:|
| MASCULINO          | 7726               |
| FEMININO           | 736                |

Em 4319 proposições não há informação do gênero do(a) parlamentar que propôs.

### Proposições x Temas

Ranking dos 6 temas mais frequentes:

|     Tema            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| COMUNICAÇÕES        | 2774               |
| TRABALHO E EMPREGO  | 603                |
| EDUCAÇÃO            | 598                |
| VIAÇÃO E TRANSPORTES| 554                |
| ADMINISTRAÇÃO PÚBLICA| 524               |
| ORGANIZAÇÃO POLÍTICO-ADMINISTRATIVA DO ESTADO|  495            |
| INDÚSTRIA, COMÉRCIO E DEFESA DO CONSUMIDOR   |  439            |

### Proposições x Tipo do Autor

Ranking dos tipos de autores do mais frequente ao menos frequente:

|     Tipo do Autor          |  Qtd. Proposições  |
| :------------------------- |:------------------:|
| DEPUTADO                   | 8461               |
| COMISSÃO PERMANENTE        | 2988               |
| ÓRGÃO DO PODER LEGISLATIVO | 778                |
| ÓRGÃO DO PODER EXECUTIVO   | 382                |
| ÓRGÃO DO PODER JUDICIÁRIO  | 54                 |
| COMISSÃO MISTA PERMANENTE  |  35                |
| COMISSÃO PARLAMENTAR DE INQUÉRITO  |  21        |
| COMISSÃO DIRETORA          |21                  |
| COMISSÃO ESPECIAL          |  18                |
| MPU - MINISTÉRIO PÚBLICO DA UNIÃO  | 13         |
| COMISSÃO MISTA ESPECIAL    | 6                  |
| CONSELHO                   | 2                  |
| SENADOR                    | 1                  |
| COMISSÃO PERMANENTE DO SENADO FEDERAL| 1        |

### Proposições x Ano

![06_10_Ano](/assets/img/propositions-analysis/img15.png)

Ranking:

|     Ano             |  Qtd. Proposições  |
| :------------------ |:------------------:|
| 2007                | 3849               |
| 2009                | 3509               |
| 2008                | 3096               |
| 2010                | 2251               |
| 2011                | 43                 |


### Proposições x Região

![06_10_Regiao](/assets/img/propositions-analysis/img16.png)


Ranking:

|     Região          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SUDESTE             | 3497               |
| NORDESTE            | 1949               |
| SUL                 | 1175               |
| CENTRO-OESTE        | 977                |
| NORTE               | 864                |

Em 4319 proposições não há informação da região em que  proposição se origina.

### Proposições x Tipos

![06_10_Tipos](/assets/img/propositions-analysis/img17.png)

Ranking:

|     Tipo            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PL                  | 8114               |
| PDC                 | 3112               |
| PLP                 | 608                |
| PEC                 | 535                |
| PRC                 | 242                |
| MPV                 | 170                |


Legenda:

* PL = Projetos de Lei
* PDC = Projetos de Decreto Legislativo da Câmara
* PLP = Projetos de Lei Complementar
* PEC = Projetos de Emenda à Constituição
* MPV = Medidas Provisórias (MPV)
* PRC = Projetos de Resolução da Câmara  

### Proposições x Partidos Políticos

![06_10_Partidos](/assets/img/propositions-analysis/img18.png)


Ranking dos 6 partidos com mais proposições e as respectivas quantidades:

|     Partido         |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PMDB                | 1326               |
| PT                  | 959                |
| PSDB                | 897                |
| PP                  | 653                |
| DEM                 | 652                |
| PR                  | 645                |

Em 4389 proposições não há informação do partido associado.

### Proposições x Nome do Parlamentar


Ranking dos 10 deputados com mais proposições:

|     Nome do Parlamentar         |  Qtd. Proposições  |
| :-------------------------------|:------------------:|
| CLEBER VERDE                    | 192                |
| CARLOS BEZERRA                  | 186                |
| DR. TALMIR                      | 122                |
| VITAL DO RÊGO FILHO             | 120                |
| ANTONIO CARLOS MENDES THAME     | 105                |
| CARLOS SOUZA                    | 98                 |
| NEILTON MULIM                   | 81                 |
| DR. UBIALI                      | 79                 |
| ELIENE LIMA                     | 78                 |
| VALDIR COLATTO                  | 78                 |



Média de proposições por candidato: _15.36 proposições_.

## Para mais informações de cada comparação mostrada acima, basta acessar meu repositório no Github com a análise e o código usado para processar os dados de 2006 a 2010 neste [link](https://github.com/elciusferreira/propositions-analysis/blob/master/analise_proposicoes06-10.ipynb).  


# Resultados da análise das proposições entre 2002 e 2006

Verificando o conteúdo do arquivo que, segundo o portal da Câmara, corresponde ao intervalo de 2002 a 2006, temos que existem 11899 proposições.

### Proposições x Estados

![02_06_Estados](/assets/img/propositions-analysis/img7.png)

Ranking dos 6 estados com mais proposições e as respectivas quantidades:

|     Estado          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| RJ                  | 1643               |
| SP                  | 1453               |
| MG                  | 623                |
| RS                  | 606                |
| BA                  | 386                |
| PR                  | 342                |

Em 3530 proposições não há informação da UF em que  proposição se origina.

### Proposições x Gênero

![02_06_Genero](/assets/img/propositions-analysis/img8.png)

|     Gênero         |  Qtd. Proposições  |
| :------------------|:------------------:|
| MASCULINO          | 7647               |
| FEMININO           | 722                |

Em 3530 proposições não há informação do gênero do(a) parlamentar que propôs.

### Proposições x Temas

Ranking dos 6 temas mais frequentes:

|     Tema            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| COMUNICAÇÕES        | 2362               |
| TRABALHO E EMPREGO  | 737                |
| EDUCAÇÃO            | 622                |
| ADMINISTRAÇÃO PÚBLICA| 616               |
| TRIBUTAÇÃO          | 563                |
| ORGANIZAÇÃO POLÍTICO-ADMINISTRATIVA DO ESTADO|  492            |
| INDÚSTRIA, COMÉRCIO E DEFESA DO CONSUMIDOR   |  474            |

### Proposições x Tipo do Autor

Ranking dos tipos de autores do mais frequente ao menos frequente:

|     Tipo do Autor          |  Qtd. Proposições  |
| :------------------------- |:------------------:|
| DEPUTADO                   | 8369               |
| COMISSÃO PERMANENTE        | 2506               |
| ÓRGÃO DO PODER EXECUTIVO   | 444                |
| ÓRGÃO DO PODER LEGISLATIVO | 410                |
|COMISSÃO PARLAMENTAR DE INQUÉRITO | 43           |
| COMISSÃO DIRETORA          |  41                |
| ÓRGÃO DO PODER JUDICIÁRIO  |  32                |
| COMISSÃO ESPECIAL          |15                  |
|COMISSÃO PARLAMENTAR MISTA DE INQUÉRITO|  14     |
|COMISSÃO MISTA PERMANENTE   | 10                 |
| MPU - MINISTÉRIO PÚBLICO DA UNIÃO| 7            |
| CONSELHO                   |4                   |
| ÓRGÃO DO SENADO FEDERAL    | 2                  |
| COMISSÃO MISTA ESPECIAL    | 2                  |

### Proposições x Ano

![02_06_Ano](/assets/img/propositions-analysis/img9.png)

Ranking:

|     Ano             |  Qtd. Proposições  |
| :------------------ |:------------------:|
| 2003                | 4491               |
| 2004                | 2692               |
| 2005                | 2636               |
| 2006                | 2050               |
| 2007                | 19                 |


### Proposições x Região

![02_06_Regiao](/assets/img/propositions-analysis/img10.png)


Ranking:

|     Região          |  Qtd. Proposições  |
| :------------------ |:------------------:|
| SUDESTE             | 3940               |
| NORDESTE            | 1496               |
| SUL                 | 1116               |
| NORTE               | 912                |
| CENTRO-OESTE        | 905                |

Em 3530 proposições não há informação da região em que  proposição se origina.

### Proposições x Tipos

![02_06_ipos](/assets/img/propositions-analysis/img11.png)

Ranking:

|     Tipo            |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PL                  | 7709               |
| PDC                 | 2631               |
| PEC                 | 590                |
| PLP                 | 387                |
| PRC                 | 330                |
| MPV                 | 252                |


Legenda:

* PL = Projetos de Lei
* PDC = Projetos de Decreto Legislativo da Câmara
* PLP = Projetos de Lei Complementar
* PEC = Projetos de Emenda à Constituição
* MPV = Medidas Provisórias (MPV)
* PRC = Projetos de Resolução da Câmara

### Proposições x Partidos Políticos

![02_06_Partidos](/assets/img/propositions-analysis/img12.png)


Ranking dos 6 partidos com mais proposições e as respectivas quantidades:

|     Partido         |  Qtd. Proposições  |
| :------------------ |:------------------:|
| PT                  | 1266               |
| PL                  | 1212               |
| PFL                 | 1065               |
| PMDB                | 1055               |
| PSDB                | 933                |
| PTB                 | 620                |

Em 3531 proposições não há informação do partido associado.

### Proposições x Nome do Parlamentar


Ranking dos 10 deputados com mais proposições:

|     Nome do Parlamentar         |  Qtd. Proposições  |
| :-------------------------------|:------------------:|
| CARLOS NADER                    | 638                |
| ROGERIO SILVA                   | 139                |
| CARLOS SOUZA                    | 131                |
| ANTONIO CARLOS MENDES THAME     | 104                |
| ALBERTO FRAGA                   | 97                 |
| ALMIR MOURA                     | 91                 |
| CELSO RUSSOMANNO                | 91                 |
| LAURA CARNEIRO                  | 88                 |
| POMPEO DE MATTOS                | 86                 |
| EDUARDO PAES                    | 84                 |



Média de proposições por candidato: _15.76 proposições_.

## Para mais informações de cada comparação mostrada acima, basta acessar meu repositório no Github com a análise e o código usado para processar os dados de 2002 a 2006 neste [link](https://github.com/elciusferreira/propositions-analysis/blob/master/analise_proposicoes02-06.ipynb).  


# Resultados da análise das proposições entre 1998 e 2002

No geral existem 3473 proposições no arquivo correspondente à este intervalo de tempo.

### Proposições x Estados

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

### Proposições x Gênero

![98_02_Genero](/assets/img/propositions-analysis/img2.png)

|     Gênero         |  Qtd. Proposições  |
| :------------------|:------------------:|
| MASCULINO          | 1383               |
| FEMININO           | 105                |

Em 1985 proposições não há informação do gênero do(a) parlamentar que propôs.

### Proposições x Temas

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

### Proposições x Tipo do Autor

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

### Proposições x Ano

![98_02_Ano](/assets/img/propositions-analysis/img3.png)

Como observa-se, o arquivo disponibilizado pelo portal do governo como contendo informações de 1998 até 2002 só possui dados de 2002 e alguns de 2003.

### Proposições x Região

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

### Proposições x Tipos

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
* PRC = Projetos de Resolução da Câmara

### Proposições x Partidos Políticos

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

### Proposições x Nome do Parlamentar


Ranking dos 10 deputados com mais proposições:

|     Nome do Parlamentar         |  Qtd. Proposições  |
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



Média de proposições por candidato: _4.82 proposições_.

## Para mais informações de cada comparação mostrada acima, basta acessar meu repositório no Github com a análise e o código usado para processar os dados de 1998 a 2002 neste [link](https://github.com/elciusferreira/propositions-analysis/blob/master/analise_proposicoes98-02.ipynb).  
