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


![Pixel](/assets/pixel.png)

### Linhas

Para a rasterização de linhas foi criada a função **DrawLine()** que recebe como parâmetros dois objetos da classe Pixel, o pixel inicial e final da linha.

Para realizar o processo de seleção dos pixels entre os pontos final e inicial da linha, foi utilizado o algoritmo de Bresenham. Este foi o maior desafio do trabalho devido a implementação e generalização do algoritmo para todos os 8 quadrantes. Os casos em que as linhas são verticais e horizontais tiveram que ser tratados separadamente.

![Octantes](/assets/octantes.png)

Os casos em que as linhas são verticais e horizontais tiveram que ser tratados separadamente, para o caso da linha estar sobre o eixo Y (dx = 0), temos:

``` cpp
if(dx == 0) // Line above axis y
  {

    if(inc_y > 0) // positive axis y
    {

      while(y != yf)
      {

        pix->set_Y(++y);
        Interpolate(pix, all_distances);
        PutPixel(pix);

      }

    }
    else  // negative axis y
    {

      while(y != yf)
      {

        pix->set_Y(--y);

        PutPixel(pix);

      }

    }

  }
```
Após tratar esses casos, o primeiro passo para a generalização foi identificar se os valores de x e y que compõem a reta crescem ou decrescem.

``` cpp
(xf > x) ? (inc_x = 1) : (inc_x = -1);  // if true then x increases, else decreases
(yf > y) ? (inc_y = 1) : (inc_y = -1);  // if true then y increases, else decreases
  ```
Após identificar o valor das variáveis de controle inc_x e inc_y e sabendo se dx >= dy ou dx < dy, é possível acender os pixels que formarão a reta em qualquer quadrante. Por exemplo, para dx >= dy, inc_x = -1 e inc_y = -1, temos a seguinte implementação para o quinto quadrante:

``` cpp
if(dx >= dy)
    {

      d = 2 * dy - dx;
      incr1 = 2 * dy;
      incr2 = 2 * (dy - dx);

      while(x != xf)
      {

        if (d <= 0)
        {

          d += incr1;
          x += inc_x;

        }
        else
        {

          d += incr2;
          x += inc_x;
          y += inc_y;

        }

        pix->set_X(x);
        pix->set_Y(y);

        PutPixel(pix);
      }
```

![Green Line](/assets/line.png)
![Red Lines](/assets/red_lines.png)

### Triângulos

Após a parte mais trabalhosa em termos de implementação, foi desenvolvida a função **DrawTriangle()**. Esta função desenha as arestas de um triângulo na tela recebendo como parâmetros os três pixels que representam os vértices. Lembrando que cada objeto pixel possui as informações de suas coordenadas x e y, além de suas componentes RGBA.

Portanto, basta realizar a chamada da função **DrawLine()** três vezes passando um vértice em cada.

``` cpp
void DrawTriangle(Pixel p1, Pixel p2, Pixel p3)
{

  DrawLine(p1, p2);
  DrawLine(p2, p3);
  DrawLine(p3,p1);

}  
```

Em tela, temos:

![Triângulo Verde](/assets/green_triangle.png)
![Triângulos Verdes](/assets/green_triangles.png)
