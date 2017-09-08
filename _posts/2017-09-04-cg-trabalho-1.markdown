---
layout: post
title:  "Introdução à Computação Gráfica - Rasterização de Pontos e Linhas"
date:   2017-09-04 22:44:03 -0300
categories: jekyll update
---
Este post trata-se de um relatório sobre o primeiro trabalho da disciplina de Introdução à Computação Gráfica, ministrada pelo Prof. Dr. [Christian Azambuja Pagot](http://lattes.cnpq.br/4353928200012173).

O trabalho consiste nas implementações de algoritmos para rasterização de primitivas na liguagem C/C++ em conjunto com as bibliotecas GLUT e OpenGL. Como os sistemas operacionais não permitem o acesso direto na memória de vídeo, será utilizado um framework, desenvolvido pelo professor, que tem como objetivo simular a memória de vídeo.



### Pixels

Primeiramente algumas considerações: Em relação à disposição dos pixels no monitor, temos que considerar desde já que se trata de um espaço bidimensional (largura e altura) mas, a disposição dos pixels na memória se dá de forma linear, através do Color Buffer. Estes fatores devem ser respeitados para que o accionamento do pixel na posição correta seja feito.

Foi utilizado neste trabalho o padrão RGBA, ou seja, cada pixel é formado por 4 componentes de cor: R para vermelho (RED), G para verde (GREEN), B para azul (BLUE) e A para o alfa (ALPHA). Considerando isto, temos o seguinte esquema:

![Color Buffer](/assets/cg-trabalho-1/color_buffer.png)


Portanto, a posição de cada pixel e cada canal de um pixel na memória é dada da seguinte forma:

![Color Buffer2](/assets/cg-trabalho-1/color_buffer2.png)

Consolidados estes conceitos, foi implementada a classe **Pixel** que possui todas as informações de coordenadas e cores relacionadas a ele.

``` cpp
class Pixel
{

  int x;
  int y;
  double red;
  double green;
  double blue;
  double alpha;

public:

  Pixel(int X_coord, int Y_coord, int R_comp,
        int G_comp, int B_comp, int A_comp);

  int get_X() {return x;}
  int get_Y() {return y;}
  double get_R() {return red;}
  double get_G() {return green;}
  double get_B() {return blue;}
  double get_A() {return alpha;}

  void set_X(int new_x) {x = new_x;}
  void set_Y(int new_y) {y = new_y;}
  void set_RGBA(double new_r, double new_g, double new_b, double new_a);

};
```

O framework disponibilizado pelo professor disponibiliza um ponteiro chamado FBPtr para o início da região do framebuffer e manipulando o mesmo foi possível implementar a função **PutPixel()** . Esta é responsável por rasterizar um ponto na memória de vídeo recebendo como parâmetro o objeto da classe Pixel, que possui a posição (x,y) dele na tela e sua cor (RGBA).

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

Vale ressaltar que durante todo o processo de rasterização da linha, apenas três objetos da classe **Pixel** são criados: O objeto referente ao pixel inicial, referente ao pixel final e um objeto referente ao pixel que a todo instante possui suas coordenadas x e y atualizadas. Este último irá ser sempre acendido na tela e como suas coordenadas mudam, eventualmente chegam até as do último pixel.

Para realizar o processo de seleção dos pixels entre os pontos final e inicial da linha, foi utilizado o algoritmo de Bresenham. Este foi o maior desafio do trabalho devido a implementação e generalização do algoritmo para todos os 8 quadrantes do espaço 2D.

![Octantes](/assets/cg-trabalho-1/octantes.png)

Os casos em que as linhas são verticais e horizontais tiveram que ser tratados separadamente. Para o caso da linha estar sobre o eixo Y (dx = 0), temos:

``` cpp
if(dx == 0) // line above axis y
  {

    if(inc_y > 0) // positive axis y
    {

      while(y != yf)
      {

        pix->set_Y(++y);

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
Depois de tratar esses casos, o primeiro passo para a generalização foi identificar se os valores de x e y que compõem a reta crescem ou decrescem.

``` cpp
(xf > x) ? (inc_x = 1) : (inc_x = -1);  // if true then x increases, else decreases
(yf > y) ? (inc_y = 1) : (inc_y = -1);  // if true then y increases, else decreases
  ```
Após identificar o valor das variáveis de controle *inc_x* e *inc_y* e sabendo se *dx >= dy* ou *dx < dy*, é possível acender os pixels que formarão a reta em qualquer quadrante considerando os valores da variável de decisão *d*. Por exemplo, para *dx >= dy*, *inc_x = -1* e *inc_y = -1*, temos a seguinte implementação para o quinto quadrante:

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
Como resultado, temos:

![Red Line](/assets/cg-trabalho-1/red_line.png)
![Red Lines](/assets/cg-trabalho-1/red_lines.png)

### Triângulos

Após a parte mais trabalhosa em termos de implementação, foi desenvolvida a função **DrawTriangle()**. Esta função desenha as arestas de um triângulo na tela recebendo como parâmetros os três pixels que representam os vértices. Lembrando que cada objeto pixel possui as informações de suas coordenadas x e y, além de suas componentes RGBA.

Portanto, basta realizar a chamada da função **DrawLine()** três vezes passando dois vértices em cada.

``` cpp
void DrawTriangle(Pixel p1, Pixel p2, Pixel p3)
{

  DrawLine(p1, p2);
  DrawLine(p2, p3);
  DrawLine(p3, p1);

}  
```

Em tela, temos:

![Triângulo Verde](/assets/cg-trabalho-1/green_triangle.png)
![Triângulos Verdes](/assets/cg-trabalho-1/green_triangles.png)

### Interpolação Linear de Cores

A Interpolação Linear neste trabalho consiste em interpolar as cores desde o ponto inicial até o final da linha linearmente, logo uma transição gradual das cores ocorre dependendo da distância entre o início e o fim da reta.

É realizada a diferença de cores entre os pontos final e inicial, obtendo assim uma variação de cor. Para tal finalidade foi implementada uma classe **Distances**. A mesma é responsável por armazenar e calcular informações relacionadas à distância entre os pontos e às distâncias referentes a cada cor e opacidade.

``` cpp
class Distances
{

  double hypotenuse;
  int r_distance;
  int g_distance;
  int b_distance;
  int a_distance;

public:

  int get_Hypo(){return hypotenuse;}
  int get_RDist(){return r_distance;}
  int get_GDist(){return g_distance;}
  int get_BDist(){return b_distance;}
  int get_ADist(){return a_distance;}

  void setDistances(Pixel, Pixel);

};
```
Como visto, há um método chamado **setDistances()**. Este é responsável por receber os pixels inicial e final, calcular a hipotenusa que é distância entre os pontos em questão e calcular as distâncias entre os componentes RGBA.

``` cpp
void Distances::setDistances(Pixel start, Pixel end)
{
  ...

  double hypo = sqrt(dx*dx + dy*dy); // hypotenuse


  int r_dist = end.get_R() - start.get_R();
  int g_dist = end.get_G() - start.get_G();
  int b_dist = end.get_B() - start.get_B();
  int a_dist = end.get_A() - start.get_A();

  hypotenuse = hypo;
  r_distance = r_dist;
  g_distance = g_dist;
  b_distance = b_dist;
  a_distance = a_dist;

}
```  

Para cada linha que se deseja rasterizar, um objeto dessa classe é criado contendo todas essas informações.

Posteriormente foi crianda a função **Interpolate()**, que recebe o pixel que irá ser acendido na tela e também recebe o objeto da classe **Distances** com todas as informações das distâncias.

É feito um cálculo para se saber os novos valores das componentes RGBA baseando-se na distância que falta para se chegar nos valores de cor do pixel final. Cada pixel que irá ser acendido irá ter valores mais próximos a ele e assim a transição gradual de cor acontece.

``` cpp
void Interpolate(Pixel *p, Distances dist)
{

  double hypo = dist.get_Hypo();
  double new_red = p->get_R() + (dist.get_RDist()/hypo);
  double new_green = p->get_G() + (dist.get_GDist()/hypo);
  double new_blue = p->get_B() + (dist.get_BDist()/hypo);
  double new_alpha = p->get_A() + (dist.get_ADist()/hypo);

  p->set_RGBA(new_red, new_green, new_blue, new_alpha);

}
```

Portanto, a função sempre vai ser chamada no momento anterior à chamada da função **PutPixel()**

``` cpp
...
Interpolate(pix, all_distances);
PutPixel(pix);
...
```
Como resultado, temos:

![Colored Lines](/assets/cg-trabalho-1/colored_lines.png)
![Colored Art](/assets/cg-trabalho-1/colored_art.png)
![Colored Triangle](/assets/cg-trabalho-1/colored_triangle.png)
![Colored Triangles](/assets/cg-trabalho-1/colored_triangles.png)
![Colored Triangles2](/assets/cg-trabalho-1/colored_triangles2.png)
![Colored All2](/assets/cg-trabalho-1/colored_all2.png)
![Colored All](/assets/cg-trabalho-1/colored_all.png)

### Considerações Finais

A maior dificuldade encontrada neste trabalho da disciplina foi a generalização do algoritmo de Bresenham para todos os octantes mas, após vários testes sua implementação correta foi alcançada.

Uma segunda dificuldade encontrada estava na execução da interpolação. Por estar utilizando variáveis do tipo *int* para armazenar os valores das cores, a transição gradual não estava ocorrendo já que a quantidade de cor a ser adicionada poderia ser inferior a um, acontecendo assim o arredondamento para zero. Desta forma a cor não se alterava e permanecia a mesma para toda a reta. Este problema foi facilmente contornado ao utilizar variáveis do tipo *double*.

Como melhoria seria interessante o preenchimento por completo dos triângulos inicialmente sem interpolação e posteriormente com.

### Bibliografia

* [The Bresenham Line-Drawing Algorithm, por Colin Flanagan](https://www.cs.helsinki.fi/group/goa/mallinnus/lines/bresenh.html)
* [Bresenham's line algorithm](https://en.wikipedia.org/wiki/Bresenham%27s_line_algorithm)
* [Tabela de cores](http://www.flextool.com.br/tabela_cores.html)
* Notas de aula do Prof. Christian
