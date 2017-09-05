---
layout: post
title:  "Introdução à Computação Gráfica - Rasterização de Pontos e Linhas"
date:   2017-09-04 22:44:03 -0300
categories: jekyll update
---
Este post trata-se de um relatório sobre o primeiro trabalho da disciplina de Introdução à Computação Gráfica, ministrada pelo Prof. Dr. [Christian Azambuja Pagot](http://lattes.cnpq.br/4353928200012173).

O trabalho consiste nas implementações de algoritmos para rasterização de primitivas na liguagem C/C++ em conjunto com as bibliotecas GLUT e OpenGL. Como os sistemas operacionais não permitem o acesso direto na memória de vídeo, será utilizado um framework, desenvolvido pelo professor, que tem como objetivo simular a memória de vídeo.

### Pixels

Foi utilizado neste trabalho o padrão RGBA, ou seja, cada pixel é formado por 4 componentes de cor: R para vermelho (RED), G para verde (GREEN), B para azul (BLUE) e A para o alfa (ALPHA).

Manipulando o ponteiro FBptr foi possível implementar a função **PutPixel()** . Esta é responsável por rasterizar um ponto na memória de vídeo recebendo como parâmetro o objeto da classe Pixel, que possui a posição dele na tela (x,y) e sua cor (RGBA).  

```cpp
void PutPixel(Pixel *pxl)
{

  if(pxl->get_X()>IMAGE_WIDTH || pxl->get_X()<0 || pxl->get_Y()>IMAGE_HEIGHT || pxl->get_Y()<0) // exceeded limits
    return;

  else
  {

    int index = pxl->get_X()*4 + pxl->get_Y()*4*IMAGE_WIDTH;  // coordinates
    FBptr[index + 0] = pxl->get_R();  // red
    FBptr[index + 1] = pxl->get_G();  // green
    FBptr[index + 2] = pxl->get_B();  // blue
    FBptr[index + 3] = pxl->get_A();  // alpha

  }

}
```
Como resultado, temos:
![Pixel]({{ https://github.com/elciusferreira/elciusferreira.github.io/blob/master}} /assets/img/pixel.png)
