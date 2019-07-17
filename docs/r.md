# R - miscelânea e tópicos avançados

Nesse ponto será assumido que você realizou os passos de [**revisão**][Sugestões de passos para revisão da linguagem R] da linguagem R sugeridos, bem como resolveu os [**exercícios propostos**][Exercícios propostos]. Considerá-los é de grande importância para que você consiga assimilar os conceitos apresentados nesse [**Capítulo**][R - miscelânea e tópicos avançados].

Esse [**Capítulo**][R - miscelânea e tópicos avançados] visa apresentar algumas miscelâneas a respeito da linguagem de programação R, bem como, alguns tópicos mais avançados de programação em R. O termo "**avançado**" utilizado aqui não necessariamente tem correlação com dificuldade de entendimento. Aqui utilizo esse termo para abordar assuntos que normalmente eram pouco discutidos em livros mais antigos da linguagem R e que atualmente vem ganhando destaques em livros e discussões mais recentes na internet. Na verdade, a maioria dos conceitos que serão abordados são de fácil compreensão, porẽm ajudarão os programadores em R a construir códigos mais robustos e mais flexíveis. Alguns desses assuntos que serão abordados e divididos em subseções são:

  1. Pipe %>%
  
  2. Funções: 
    
     - Funcionais
    
     - Closures
    
     - dot-dot-dot, ..1, ..2 e etc
     
     - Orientação à objeto por função genérica (sistema S3)
     
   3. Regex
   
   4. Tópicos em metaprogramação
   
   5. Paralelismo
   
   6. Empacotando funções
   

## Operador %>% - Pipe   
   
    
Para que possamos entender a utilidade dos operadores pipe, em especial do operador `%>%`, vamos fazer um pão de queijo. Adiante, você encontrará a receita com 7 passos enumerados que deverão serem seguidos para que possamos fazer o nosso pão de queijo.

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Esse material não garante que você terá sucesso, caso seja curioso e tente fazer a receita. Foque apenas no código. E se você for de Minas Gerais e saiba fazer pão de queijo, desconsidere qualquer inconsistência na receita. =)
</div></div>\EndKnitrBlock{rmdnote}

**Ingredientes**: 2 copos americanos de leite, 1 copo americano de água, 1/3 de um copo americano de óleo, 1 colher de sopa de sal, 500g de povilho doce, queijo ralado a gosto, 3 ovos.

**Passos do Preparo**:

   1. **Ferva** o leite com a água e o óleo;

   2. Em uma vasilha **misture** o polvilho e o sal;
   
   3. **Jogue** o liquido fervido e **misture** com uma colher grande;
   
   4. **Espere** esfriar (30 minutos) e **despeje** o queijo ralado e os ovos;
   
   5. **Misture** a massa com a mão **amassando** até ficar homogênea;
   
   6. **Faça** bolinhas do tamanho que preferir;
   
   7. **Sirva** quentinho;
   
Assuma, por absurdo, que poderemos fazer nossos pães de queijo no R que que os verbos destacados nos passos acima são funções que implementamos em R. Dessa forma, forma, pelo que sabemos de R, poderemos fazer nossos pães de queijo de forma que segue:

```r
sirva(fazer(misture(despeje(esperar(misture(ingredientes = c(povilho, sal), add = ferver(c(leite, óleo),
      add_agua = TRUE), colher_grande = TRUE), tempo = 30), homogenea = TRUE),
      modo = "amassando"), formato = "bolinha"), modo = "quentinho")
```

Perceba que o código acima poderá ser um pouco confuso, uma vez que envolve muitas composições de funções. Porém, nada impede que você esteja salvando os resultados intermediários em objetos, de modo a facilitar a leitura do código ao relacionar esses objetos intermediários. Fazer isso funciona bem e eu particularmente utilizo muito. Porém, você também poderá fazer uso de pipes (operador `%>%`) que poderá, nessas situações, deixar a leitura do código mais fácil, lógica e consequentimente mais compreensível., como veremos adiante.
O operador de tubo `%>%` foi implementando no pacote [**magrittr**](https://github.com/tidyverse/magrittr) por [**Stefan Milton Bache**](https://github.com/smbache) e atualmente recebe a colaboração de diversas pessoas, incluindo programadores da [**RStudio, Inc**](https://www.rstudio.com/). Atualmente, o pacote não recebe muitas atualizações, muito provavelmente por já está estável e cumprindo bem o seu papel. 

O nome **magrittr** muito provavelmente faz alusão à [**René Magritte**](https://pt.wikipedia.org/wiki/Ren%C3%A9_Magritte), um dos principais pintores surrealista belga, em que a letra **r**, ao final, obviamente faz referências à linguagem R. É possível inferir isso com base no logo do pacote, apresentado logo abaixo:

<div class="figure" style="text-align: center">
<img src="images/logo_magrittr.png" alt="Logo do pacote [**magrittr**](https://github.com/tidyverse/magrittr) com frase ***Ceci n'est pas une pipe*** ([**ouça a pronuncia**](files/audio_magrittr.ogg), mesmo frase que acompanha pintura ***La trahison des images*** de [**René Magritte**](https://pt.wikipedia.org/wiki/Ren%C3%A9_Magritte)." width="25%" />
<p class="caption">(\#fig:unnamed-chunk-2)Logo do pacote [**magrittr**](https://github.com/tidyverse/magrittr) com frase ***Ceci n'est pas une pipe*** ([**ouça a pronuncia**](files/audio_magrittr.ogg), mesmo frase que acompanha pintura ***La trahison des images*** de [**René Magritte**](https://pt.wikipedia.org/wiki/Ren%C3%A9_Magritte).</p>
</div>

Voltemos à algo mais interessante, ao preparo de pães de queijo. O preparo, "em R", poderia ser quase tão saboroso quanto comer os pães de queijo, se fossem "preparados" utilizando o operador `%>%`, na forma que segue:



```r
# Fazendo pão de queijo utilizando o operador pipe, isto é,
# utilizando o operador %>%.

ferver(ingradientes = c(leite,  água,  óleo)) %>%
   misturar(colher_grande = TRUE) %>%
   esperar(tempo = 30) %>% despejar(ingredientes = c("queijo", "ovos")) %>%
   amassar(forma = "mãos") %>% fazer_bolinhas(volume = 1) %>%
   sirvir(froma = "quentinho")
```

É possível observar que o código acima é consideravelmente mais legível que o código apresentado mais acima desta subseção. O código acima é mais legível, por que os verbos/funções são encadeadas na sequência lógica do preparo e não lidos de dentro para fora, como no primeiro exemplo. Olhando rapidamente para cada um dos códigos, percebemos que o código que faz uso do operador `%>%` fornece mais informações a respeito do que se está à fazer. 

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant">Apesar de ser um operador útil, não exagere no uso de `%>%`, principalmente quando se tem um conjunto de passos demasiadamente grande. Nessas situações, procure atribuir parte do código à objetos intermediários e depois componha esses objetos. Além disso, as funções envolvidas possuem diversas entradas e saídas, pode ser que o uso do operador `%>%` não seja interessante.

No RStudio, você poderá utilizar o atalho **Ctrl + Shift + M** como atalho para escrever mais rapidamente o operador `%>%`.</div>\EndKnitrBlock{rmdimportant}


**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote">Como curiosidade, o recurso de pipes estão disponíveis em outras linguagens de programação, como [**F\#**](https://pt.wikipedia.org/wiki/F_Sharp), e os pielines de sistemas ***nix** que usa pipes para a [**comunicação entre os processos**](https://en.wikipedia.org/wiki/Pipeline_(Unix)) utilizando passagem de mensagens.
</div></div>\EndKnitrBlock{rmdnote}

Você poderá instalar o [**magrittr**](https://github.com/tidyverse/magrittr) diretamente pelo CRAN ou por meio do repositório GitHub do pacote, ou seja, por meio de um dos comandos abaixo:



```r
# Instalando o pacote magrittr disponível
# nos repositórios do CRAN.
library(magrittr)

# ou

# Para instalar pacotes diretamente do GitHub,
# você de deve ter instalado o pacote
# devtools para poder fazer uso da função
# install_github().

# Instalando o repositório magrittr do usuário/organização de
# nome tidyverse do GitHub.
devtools::install_github("tidyverse/magrittr", ref = "master") 
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Há pontos positivos e negativos ao considerar a instalação de um pacote diretamente do epositório do pacote no GitHub ou em qualquer outro sistema de hospedagem de código. Mencionarei apenas GitHub, mas o comentário se extende à outros sistemas de hospedagem de códigos, como, por exemplo, o GitLab.

Basicamente, o ponto positivo refere-se à possibilidade de estarmos instalando uma versão mais recente do pacote, porém, em alguns casos, o pacote poderá apresentar alguns bugs, muito embora os códigos no ***branch master*** são normalmente estáveis e possuem códigos iguais aos que temos no CRAN. 

Instalar diretamente um pacote que está sendo mantido no GitHub dará a possibilidade de instalar versões mais recentes do pacote que ainda não encontram-se no CRAN. Pelo GitHub, você também terá a vantagem de instalar versões mais antigas do pacote. Por exemplo, no repositório do [**magrittr**](https://github.com/tidyverse/magrittr), no GitHub, você verá que, em ***Branch***, haverá diversas versões versionadas do pacote, em que uma delas chama-se **dev**. Fazer `devtools::install_github("tidyverse/magrittr", ref = "dev")` fará com que você instale a versão de desenvolvimento do pacote. Dessa forma, aconselho que sempre considere a instalação da versão no ***branch master*** de qualquer pacote que venha instalar diretamente do GitHub. Assim, haverá menos possibilidade de você deparar-se com códigos que ainda não funcionam ou que possuam algum(s) bug(s).
</div></div>\EndKnitrBlock{rmdnote}

Para um entendimento geral do operador `%>%`, considere a existência dos objetos `x`, `y`e `f`. Então,

```{r},
x %>% f(y)
```

irá atribuir o objeto `x` à `f`, como **primeiro argumento** da função `f`, ou seja, será equivalente à fazer `f(x, y)`.

Porém, nem sempre desejamos introduzir o que está a esquerda do operador `%>%` como primeiro agumento daquilo que está à sua direita. Para isso, poderemos fazer uso do caracter `.` (ponto). Esse caracter irá designar em qual posição será introduzido o objeto à esquerda de `%>%` na função à sua direita. Por exemplo, a expressão `x %>% f(a, b = .)` fará com que `x` à esqueda de `%>%` seja substituído no lugar do caracter `.`, ou seja, `x` é passado como argumento à `b`, segundo argumento de `f`.

**Exemplo**: Uso do caracter `.` em um contexto de bloco de instrução. Esse exemplo mostra que o que está a direita do operador `%>%` não necessariamente precisa ser uma função. Nesses casos, o caracter `.` é de grande importância para que o operador saiba substituir corretamente o objeto `x` no bloco de instruções.


```r
library(magrittr)
x <- mtcars
x %>% {
  if (is.data.frame(.) || is.matrix(.)){
    cat("A dimensão dos dados é", dim(.))
  } else {
    cat("Objeto não é uma matriz ou um data frame")
  }
}
```

```
## A dimensão dos dados é 32 11
```
**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Observe que, por exemplo, fazer `x %>% f(., y = 1)`  equivale a fazer `x %>% f(y = 1)`, uma vez que por padrão, o objeto que está à esquerda de `%>%`sempre será substituído como primeiro argumento da função que está mais a sua direta, caso não seja utilizado o caractere `.` para indicar o lugar do substituição. 
</div></div>\EndKnitrBlock{rmdnote}


Um outro operador útil disponível no pacote [**magrittr**](https://github.com/tidyverse/magrittr) é o operator ***tee***, denotado por `%T>%`. Esse operador funciona de forma muito parecida com o operador `%>%`, exceto pelo fato de que ele irá retornar o conteúdo do lado esquedo e **não** o resultado da operação do seu lado diretio. 

O uso do operador `%T>%` não é tão comum. Normalmente a frequência de uso do operador `%>%` é muito maior. Porém, veja que não é possível resolver o exemplo que segue utilizando apenas o operador `%>%`.

**Exemplo**: Pelo que entendemos do operador `%>%`, não faz nenhum sentido o código abaixo:


```r
# Fixando uma semente.
set.seed(0) 
rnorm(1000L) %>% hist(., main = "Histograma Qualquer", xlab = "x",
                      ylab = "Frequência", col = rgb(1, 0.9, 0.8), border = NA) %>% mean 
```

```
## Warning in mean.default(.): argumento não é numérico nem lógico: retornando
## NA
```

<img src="r_files/figure-html/unnamed-chunk-9-1.png" width="384" style="display: block; margin: auto;" />

```
## [1] NA
```
Nesse exemplo, observamos que o histograma foi construído, porém, não faz nenhum sentido passar um gráfico à função `mean`. Muito provavelmente o desejo de quem viria escrever um código como esse seria tirar a média do vetor resultante do código `rnorm(1000L)`. Nessas situações, poderemos fazer uso do operador `%T>%` (operador ***tee***).


**Exemplo**: Aqui temos um típico uso do operador `%T>%`. Perceba que utilizando o perador `%T>%`, foi possível passar `rnorm(1000L)` como argumento à função `hist`, assim como seria possível utilizando o operador `%>%`. Porém, com o operador `%T>%`, conseguimos passar `rnorm(1000L)` à função `mean` e não à função `hist`, que seria esperado se utilizássemos o operador `%>%`.


```r
# Fixando uma semente.
set.seed(0) 
rnorm(1000L) %T>% hist(., main = "Histograma Qualquer", xlab = "x",
                       ylab = "Frequência", col = rgb(1, 0.9, 0.8), border = NA) %>% mean 
```

<img src="r_files/figure-html/unnamed-chunk-10-1.png" width="384" style="display: block; margin: auto;" />

```
## [1] -0.01582957
```

Um outro operador pipe que é bastante útil é o perador de exposição, denotado por `%$%`. Trata-se de um operador que é bastante útil quando estamos trabalhando com (quadro de dados) data frames ou matrizes, onde temos variáveis dispostas em suas colunas. Com esse operador, poderemos tornar visíveis as variáveis do objeto à sua esquerda nas funções à sua direita. Considere o exemplo que segue:

**Exemplo**: No código que segue, estamos tornando visíveis as variáveis do objeto `mtcars` na função `cor`. Dessa forma, poderemos calcular a correlação entre as variáveis **cyl** e **hp** do data frame **mtcars**.


```r
mtcars %$% cor(cyl, hp)
```

```
## [1] 0.8324475
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Normalmente esse operador é útil quando a função a direita não possui argumento de dados. Por exemplo, se o objetivo fosse calcular uma regressão linear simples com essas variáveis, poderíamos fazer:
</div>\EndKnitrBlock{rmdnote}

```r
mtcars %>% lm(cyl ~ hp, data = .)
```

```
## 
## Call:
## lm(formula = cyl ~ hp, data = .)
## 
## Coefficients:
## (Intercept)           hp  
##     3.00680      0.02168
```
uma vez que a função `lm` já possui um argumento para o conjunto de dados a ser utilizado. Ao passar o conjunto de dados para a função `lm`, todas as variáveis de **mtcars** estarão visíveis no interior da função `lm`.
</div>

Por fim e não menos importante, existe o operador de pipe compostos, denotado por `%<>%`. Esse operador é útil quando queremos realizar uma operação e atribuir essa modificação ao objeto à esquerda do operador. Considere um exemplo de uso do operador de pipe composto:

**Exemplo**: Utilizando o operador `%<>%` para alterar o conteúdo da variável **disp** do data frame **mtcars**. Perceba que ao chamar mtcars, a variável **disp** agora é do tipo inteiro.


```r
mtcars$disp %<>% as.integer()
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: int  160 160 108 258 360 225 360 146 140 167 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Alguns pacotes de R possuem vinhetas que facilitam o entendimento das funções empacotadas. Não necessariamente as vinhetas irão dissertar sobre todas as funções implementadas. Porém, essas vinhetas normalmente focam no que há de mais importante no pacote. Você poderá encontrar a vinheta do pacote [**magrittr**](https://github.com/tidyverse/magrittr) [**aqui**](https://cran.r-project.org/web/packages/magrittr/vignettes/magrittr.html). Normalmente essas vinhetas são mais fáceis de serem lidas do que as documentações dos pacotes. Porém, consultar a documentação é o caminho correto para encontrar as respostas mais difícies e que muitas vezes não são abordadas nas vinhetas.
</div></div>\EndKnitrBlock{rmdobservation}

### Exercícios {-}

Resolva os exercícios que seguem. Os operadores pipes que você utilizará para resolver os exercícios não necessariamente irão produzir as melhores soluções. Porém, esses exercícios farão você pensar a respeito do emprego dos operadores e, aqui, é isso o que importará.

1. Resolva os itens abaixo utilizando o operador `%>%` do pacote [**magrittr**](https://github.com/tidyverse/magrittr): 

   - `as.character(log(cos(sin(pi))))`

   - `round(var(seq(from = 1, to = 10, by = 0.5)), digits = 1)`
  
   - `summary(anova(lm(mpg ~ wt, data = mtcars)))`
  
   - `summary(lm(dist ~ log(accel), data = na.omit(attenu)))`
   
2. Sem salvar objetos intermediários, utilize operadore(s) pipe(s) para reescrever o código abaixo:

   
   ```r
      dados <- subset(iris, Sepal.Length > mean(Sepal.Length))
      cor(dados$Sepal.Length, dados$Sepal.Width)
   ```

3. Sem salvar objetos intermediários, utilize operadore(s) pipe(s) para reescrever o código abaixo:

   
   ```r
      vetor <- 1:10
      plot(matrix(data = vetor, ncol = 5, nrow = 5))
      quantil <- quantile(vetor)
      print(quantil)
   ```
4. Sem fazer uso dos operadores de atribuições `<-` ou `=`, reescreva o código abaixo usando operadore(s) pipe(s):

   
   ```r
      mtcars <- transform(mtcars, cyl = cyl * 2)
   ```


5. Considere o código abaixo que faz uso do operador `%>%`. **Dica**: busque nas documentações do pacote [**magrittr**](https://github.com/tidyverse/magrittr), o uso das funções `subtract` e `divide_by`. O que esse código faz? Reescreva-o sem fazer uso do operador `%>%`.

   
   ```r
       vetor <- c(1.7, 2.74, 5.66, 8.13, 4.04)
       vetor %<>% subtract(., mean(.)) 
       vetor %>% divide_by(., sd(.))
   ```

6. Considere o código abaixo e reescreva-o utilizando o operador `%>%` sem utilizar de passos intermediários. **Dica**: Procure identificar o uso da função `extract` do pacote [**magrittr**](https://github.com/tidyverse/magrittr).

   
   ```r
      # Essa função não deverá entrar no pipe.
      set.seed(0) 
      
      x <- runif(n = 100, min = 0, max = 100)
      x <- x[x > 10 & x < 30]
      round(mean(x), digits = 1)
   ```

7. Reescreva o código abaixo utilizando o operador pipe `%>%`.

   
   ```r
      dados <- subset(iris, Sepal.Length > 5) 
      aggregate(Sepal.Length ~ Species, dados, FUN = mean)
   ```

   Tente reescrever o código apenas utilizando o operador `%>%`e depois modifique-o para utilizar o operador de exposição `%$%`. **Dica**: procure entender o emprego das funções `subset` e `aggregate`, funções dos pacotes **base** e **stats**, respectivamente.
   
8. Estude a vinheta do pacote [**magrittr**](https://github.com/tidyverse/magrittr). Acesse a vinheta [**aqui**](https://cran.r-project.org/web/packages/magrittr/vignettes/magrittr.html).

9. Explique o que o código abaixo faz:

   
   ```r
      f <- . %>% subtract(., mean(.)) %>% divide_by(., sd(.))
   ```

10. Use o que aprendeu ao resolver o exercício anterior para reescrever o código abaixo usando pipes:

    
    ```r
      vetor <- c(1.7, 2.74, 5.66, 8.13, 4.04)
      sum(x - mean(x))/sd(x)
    ```

## Funções

Como já sabemos, uma vez que você deve ter utilizado bastante o confeito de funções ao resolver os [**exercícios sugeridos**][Exercícios propostos], funções são objetos que recebe uma ou algumas entradas, as processas em seu interior e te retorna uma ou mais saída(s). O diagrama \@ref(fig:diagramafuncao) mostra um comportamento genérico de uma função qualquer (**function**) que recebe uma quantidade arbitrária de argumentos, com estruturas de dados distintas, e retorna também uma quantidade arbitrária de informações, objetos com estruturas de dados distintas:

<div class="figure" style="text-align: center">
<!--html_preserve--><div id="htmlwidget-192e9aee0e22115d0314" style="width:770px;height:350px;" class="DiagrammeR html-widget"></div>
<script type="application/json" data-for="htmlwidget-192e9aee0e22115d0314">{"x":{"diagram":"\ngraph TD\n\nA(arg_1)\nB(arg_2)\nC(arg_3)\nD(...)\nE(arg_n)\nF(arg_n+1)\nG(...)\nH((function))\n\nA-->|vector|H\nB-->|matrix|H\nC-->|data frame|H\nD-->|...|H\nE-->|list|H\nF-->|factor|H\nG-->|new structure|H\n\nH-->|matrix|I(out_1)\nH-->|list|J(out_2)\nH-->|vector|K(out_3)\nH-->|...|L(...)\nH-->|factor|M(out_n)\nH-->|data frame|N(out_n+1)\nH-->|new structure|O(...)\n\nstyle A fill:#ffe5cc\nstyle B fill:#ffe5cc\nstyle C fill:#ffe5cc\nstyle D fill:#ffe5cc\nstyle E fill:#ffe5cc\nstyle F fill:#ffe5cc\nstyle G fill:#ffe5cc\nstyle H fill:#ff8900\nstyle I fill:#ffe5cc\nstyle J fill:#ffe5cc\nstyle K fill:#ffe5cc\nstyle L fill:#ffe5cc\nstyle M fill:#ffe5cc\nstyle N fill:#ffe5cc\nstyle O fill:#ffe5cc\n"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
<p class="caption">(\#fig:diagramafuncao)Comportamento genérico da função de nome **function** que recebe diversos argumentos com estruturas de dados distintas e retorna diversos diversos objetos com estuturas de dados distintas. Note que ***new structure***, no diagrama, deixa claro que o programador poderá criar suas novas estruturas de dados que poderão ser passadas e/ou retornadas por uma função.</p>
</div>

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Algo que torma uma função bastante flexível é a capacidade de podermos passar funções como argumentos à outras funções. Muito embora esse fato não esteja destacado no diagrama acima, nunca se esqueça que, em R, você facilmente poderá passar uma função como argumento de uma outra função.

**Exemplo**: `round(sum(c(1.73, 2.47, 7.21, 8.74, NA), na.rm = TRUE), digits = 1)`
</div></div>\EndKnitrBlock{rmdimportant}

Uma função em R é dividida em três partes:

  1. **Lista de Argumentos**: Conjunto de argumentos, podendo ter as mais variadas estruras de dados que pode inclusive alterar                               o comportamento da função.

  2. **Corpo**: Código no interior da função que será capas de processar e tomar decisões de acordo com sua lista de argumentos.
  
  3. **Ambiente**: Os ambientes (***environment***) de reconhecimentos de objetos no interior da função. Isso permite que possamos ter objetos com o mesmo nome referindo-se à conteúdos distintos na memória do computador.
  
Como já sabemos, mas irei repetir, a forma geral de implementação de uma função é:



```r
f <- function(argumentos){
   # Aqui é onde as coisas acontecem.
   corpo
} # Fim da função.
```

Poderemos identificar essas três partes de uma função utilizando as funções `formals()`, `body()` e `environment()`. Por exemplo, considere a função abaixo:


```r
f <- function(x, y){
   `+`(x,y)
}

# Lista de argumentos.
formals(f)
```

```
## $x
## 
## 
## $y
```

```r
# Corpo da função.
body(f)
```

```
## {
##     x + y
## }
```

```r
# Ambiente que a função foi definida.
environment(f)
```

```
## <environment: R_GlobalEnv>
```

Além disso, lembre-se que funções podem ter argumentos com valores já pré-definidos, como é o caso de `f()` no código que segue:


```r
f <- function(x = 1, y = 2){
   x + y
}
f(5)
```

```
## [1] 7
```

```r
f(2,4)
```

```
## [1] 6
```

### Passando atributos

Uma função em R é um objeto qualquer. Dessa forma, assim como qualquer objeto, uma função poderá carregar consigo uma quantidade qualquer de atributos que podem ser recuperados e utilizados a qualquer momento. Considere os códigos que seguem:


```r
# Vetor com valores inteiros em memória de 1 à 10.
x <- 1L:10L

# Introduzindo dois argumentos ao objeto x.
# Primeiro argumento: desc, que apresenta uma pequena descrição do objeto x.
# Segundo argumento: M, uma matriz qualquer que poderia vir a ser útil guardar.
attr(x = x, which = "desc") <- "vetor com valores inteiros"
attr(x = x, which = "M") <- matrix(data = c(1, 7, 3, 8), ncol = 2, nrow = 2)
```

Note que agora o objeto `x` carrega não apenas os valores inteiros de 1 a 10. Foram acrescentados dois argumentos à `x`, são eles, `desc` que contém uma string descrevendo o que é o objeto `x`. Perceba que os atributos não afetam as operações que realizamos com `x`, mas poderemos, se desejarmos, acessar os atributos e trabalharmos com eles, como postra o trecho de código abaixo:


```r
# Os atributos não irão afetar as operações realizadas 
# considerando o objeto x.
sum(x + 1)
```

```
## [1] 65
```

```r
# Listando os atributos do objeto x:
attributes(x)
```

```
## $desc
## [1] "vetor com valores inteiros"
## 
## $M
##      [,1] [,2]
## [1,]    1    3
## [2,]    7    8
```

```r
# Acessando o atributo de nome M (uma matriz) 
# e invertendo.
solve(attr(x, "M"))
```

```
##            [,1]        [,2]
## [1,] -0.6153846  0.23076923
## [2,]  0.5384615 -0.07692308
```

Como é possível introduzir atributos à qualquer objeto em R, e funções são objetos, então considerre o trecho de código que segue, em que é introduzido o atributo `M` do objeto `x` como atributo da função `f()` abaixo:


```r
# Retorna os caracteres "-", "0", "+"
# a depender do valor informado.
f <- function(x){
   # x é um objeto numérico.
   
   if (x == 0) "0"
   else ifelse(x > 0, "+", "-")
}

# Introduzindo o atributo de nome desc que contém uma breve descrição da
# função f():
attr(f, "desc") <- "retorna -, 0 ou +, a depender do valor passado à x"

# Acessando o conteúdo do atributo desc:
attr(f, "desc")
```

```
## [1] "retorna -, 0 ou +, a depender do valor passado à x"
```

Sabemos que o uso da função `body()` permete-nos acessar o corpo de uma função (código da função). Porém, você apenas irá visualizar as partes do código que foram implementadas estritamente em R. Por exemplo, no trecho de código abaixo é apresentado o sudo da função `body()` sobre uma função implementada em R e outra função que tem o seu código implementado em uma linguagem de mais baixo nível:
   
   
 
 ```r
     # Acessando o corpo da fução rm():
     body(ls)
     
     # Tentando acessar o corpo da função sum():
     body(sum)
 ```

Note que foi possível acessar parte do conteúdo, implementado em R, da função `rm()`. Porém, no caso da função `sum()` o retorno foi `NULL`, uma vez que essa função é por completo implementada em uma linguagem de mais baixo nível. Isso se deve ao fato de que essas funções foram escritas em linguagens compiladas como o caso de C/C++, camhando assim um código objeto e não um código fonte.

Em muitas situações desejamos passar uma função como argumento à outra função. O trecho de código abaixo cria duas simples funções, `f()` e `g()`, em que passamos `f()` como argumento à função `g()`:


```r
# As funções não necessariamente necessitam ter argumentos.
f <- function(){
   "Olá"
}

g <- function(func){
   paste(func, "mundo", sep = " ")
}

# Passando a função f() como argumento da função g():
g(func = f())
```

```
## [1] "Olá mundo"
```

```r
# Compondo as funçoes nchar(), g() e f().
# A função nchar() retorna a quantidade de caracteres 
# na estring retornada por g().
nchar(g(func = f()))
```

```
## [1] 9
```

### Funções anônimas

Algo que é bastante útil quando estamos trabalhando com funções é a possibilidade de não nomear uma função. Essa estratégia é interessante quando temos funções curtas que não queremos nos dar o trabalho de pensarmos em um nome. Normalmente, aplica-se à casos de funções curtas que são passadas como argumento à outras funções. O trecho de código que segue apresenta o uso de uma função anônima passada como argumento à função `integrate()` de R:


```r
# Passando a função anônima function(x) x ^ 2 como argumento da 
# função integrate().
integrate(function(x) x ^ 2, lower = 0, upper = 2)$value
```

```
## [1] 2.666667
```

Não esqueça que, em muitos casos, compor funções utilizando o operador `%>%` pode ser interessante. As composições acimas poderiam ser realizadas da forma que segue:


```r
# Primeira composição utilizando o operador %>%: 
f %>% g %>% nchar

# Segunda composição utulizando os operadores pipes %>%  e %$%:
(function(x) x^2) %>% integrate(lower = 0, upper = 2) %$% value
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Utilizar os operadores pipes pode ser interessante quando estamos a fazer uma análise de dados, em que queremos deixar claro uma sequência lógica de operações. Porém, note que pipes não irão tornar o seu código mais eficientes do ponto de vista computacional, nem o contrário, ou seja, utilizar pipes não irão tornar os seus códigos menos eficientes.
</div></div>\EndKnitrBlock{rmdnote}

### Escopo léxico

Em computação, o escopo é o que delimita a relação de objetos e expressões, ou seja, em que partes do código um ou mais objetos são reconhecidos por uma dada expressão ou conjunto de expressões. Na maioria das linguagens de programção o escopo é léxico, também chamado de escopo estático, uma vez que podem ser delimitados estaticamente, antes da execução do programa por meio da sintaxe da linguagem, ou seja, por meio da estrutura léxica da linguagem.

A linguagem R tem escopo léxico, assim como diversas outras linguagens de programação. Trata-se de tipo de escopo comum em linguagens como Pascal, C, C++, Ada, Go, Haskell, R, Julia, Python, Ruby, entre diversas outras. Considere o exemplo apresentado no código abaixo:


```r
x <- "fora"
f <- function(){
   x <- "dentro"
   x
}; f()
```

```
## [1] "dentro"
```

Para quem já programa um pouco em R, o retorno da função `f()` era esperado, uma vez que olhando para o código, entendemos facilmente qual a saída, uma vez que a sintaxe nos acusa (escopo léxico). Na verdade, o termo vem de ***lexing***, que refere-se ao processo de conversão de partes significativas do código intendíveis para o interpretador. 

Existem linguagens que fazem uso de [**escopo dinâmico**](https://pt.wikipedia.org/wiki/Escopo_(computa%C3%A7%C3%A3o)#Escopo_din%C3%A2mico), como é o caso do Emacs Lisp, shell Bash, LaTeX (linguagem de marcação), entre outras. Como esse não é o caso da linguagem R que frequentemente nos deparamos em R, aqui não é o lugar para dissertar em relação à esse assunto. 

No código acima, perceba que havia um objeto `x` definido no interior da função. Dessa forma, o retorno da função buscará por referências à `x` no mesmo escopo da função, isto é, irá considerar `x` definido por `x <- "dentro"`. Porém, considere a simples modificação do código na forma que segue:


```r
x <- "fora"
f <- function(){
   x
}; f()
```

```
## [1] "fora"
```

No código acima, a função `f()` não pode encontrar referências ao objeto `x` no interior da função. Dessa forma, R considerar-a o objeto `x` no respectivo escopo mais externo, que nesse caso é o objeto `x` definido por `x <- "fora"`. Esse comportamento é válido se consideramos estruturas mais aninhadas, como a que é apresentada no código que segue:


```r
x <- "estou fora de f"
f <- function(){

   # Podemos definir funções dentro de funções.
   g <- function(){
      x
   } # fim da função interna
   list(g = g(), x = x)
} # fim da função externa

f()
```

```
## $g
## [1] "estou fora de f"
## 
## $x
## [1] "estou fora de f"
```

Perceba que tanto o retorno da função `g()` quando o objeto `x` da função `f()` referem-se ao valor de `x` definido fora do escopo da função `f()`. Isso se deve ao fato da linguagem R procurar um objeto de nome `x` de froma sucessivas, partindo do escopo ao qual o objeto é invocado à escopos em níveis mais externos. No código acima, tanto `g()` definida dentro de `f()` quanto a prórpia função `f()` apenas encontrará referência à `x` no ambiente mais externo, isto é, será considerado o objeto `x` definido por `x <- "estou fora de f"`. 

Algo interessante de se observar é que muito embora o R procure em escopos mais externos a primeira referência ao objeto que invocamos em um escopo mais interno, escopo este em que não há nenhuma referência à este objeto, em futuras invocações da função, a partir da segunda chamada, o objeto `x` já encontra-se definido no interior da função `f()`.


```r
x <- 0
f <- function(){
   # x encontra-se definido no escopo externo na primeira chamada à
   # função f.
   x <- x + 1
   x
}
f()
```

```
## [1] 1
```

```r
f()
```

```
## [1] 1
```

Observe que mesmo que você chame por diversas vezes consecutivas a função `f()` o retorno sempre será `1`. Para ser possível obter somas em 1 iterativas, uma solução para esse problema seria fazer uso do operador de atribuição profunda, denotado por `<<-`. Esse operador permite que as alterações no objeto `x` ocorra no primeiro escopo mais abrangente que faz referência à um objeto `x`. Considere o trecho de código que segue:


```r
x <- 0
f <- function(){
   # x encontra-se definido no escopo externo na primeira chamada à
   # função f.
   x <<- x + 1 # Operador de atribuição profunda.
   x
}
f()
```

```
## [1] 1
```

```r
f()
```

```
## [1] 2
```

Porém, perceba o resultado que segue:


```r
x <- 0
f <- function(){
   x = 7
   x <<- x + 1 # Operador de atribuição profunda.
   x
}
f()
```

```
## [1] 7
```

```r
x
```

```
## [1] 8
```
Note no código acima que o valor retornado pela função é `7` (sempre) e não `8`, como alguns poderiam esperar. Perceba que isso se deve ao fato de que no interior de `f()`, sempre teremos que `x` ao lado direito do operador `<<-` será `7`, uma vez que em todas as chamadas, há dentro da função `f()` a definição de `x = 7`. Isso também implicará que o valor de `x` do lado esquerdo do operador `<<-` sempre será atualizado para `8`, em todas as chamadas. Veja que `x` ao lado esquerdo de `<<-` refere-se ao objeto `x` no escopo mais extero ao escopo de `x` no interior da função.

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Em R, os operadores `<-` e `<<-` também informam o sentido da atribuição, que normalmente é da direita para a esquerda, assim como ocorre ao considerar o operador `=`. Quase sempre as atribuições são da esquerda para a direita, com exceção das situações em que invertemos os sentidos dos operadores `<-` e `<<-`, isto é, quando consideramos as variantes `-> ` e `->>`, respectivamente.
</div></div>\EndKnitrBlock{rmdobservation}

**Exemplo**:


```r
f <- function(){
   2 -> x
   x * 2 ->> x
   x
}

f(); x
```

```
## [1] 2
```

```
## [1] 4
```

### Avaliação preguiçosa

Tecnicamente, os argumentos de uma função são promessas [***promises***](https://cran.r-project.org/doc/manuals/R-lang.html#Promise-objects) e fazem parte do mecanismo de (***lazy evaluation***). Quando uma função é chamada, cada um de seus argumentos formais são vinculados à uma promessa. Dessa forma, cada promessa, para cada um dos argumentos, armazenam a expressão do argumento e um ponteiro para o ambiente ao qual a função foi chamada. Tais promessas não armazenam nenhum valor, até o momento em que o argumento seja necessário para a função. Sendo assim, (***promises***) trata-se de uma estrutura de dados. ***Promisses*** possuem:

   * Um **ambiente**: ambiente em que uma função é avaliada/invocada.
   * Uma **expressão**: uma expressão válida passada para um argumento de uma função;
   * Um **valor**: resultado da avaliação de uma expressão em um ambiente específico.

Em R, os argumentos de uma função são avaliados de forma preguiçosa (***lazy evaluation***), são apenas promessas, ou seja, só serão avaliados na necessidade de uso do parâmetro. Em outras palavras, um parâmetro poderá eventualmente nunca ser avaliado quando uma função é executada. Considere o código que segue:


```r
# A função f() tem o argumento x que
# não é utilizado.
f <- function(x){
   y <- 1
   y
}
f()
```

```
## [1] 1
```

Como é possível observar, a função `f()` possui `x` como argumento, argumento este que em nenhum momento é utilizado. Dessa forma, mesmo que `x` não esteja definido, não teremos como retorno um erro ao executar `f()`. Isso se deve ao fato de que argumentos de funções, em R, são avaliados de forma preguiçosa.

Um dos grandes benefícios da avaliação preguiçosa é a possibilidade que temos de atrasar a computação, de modo que um dos argumentos poderá conter cálculos intensivos que só será avaliado se necessário. Dessa forma, devido a possibilidade de uma função matemática poder ser passado como argumento à uma funçãom, que ventualmente pode ser algo custoso do ponto de vista computacional, [***lazy evaluation***](https://en.wikipedia.org/wiki/Lazy_evaluation) é o padrão da linguagem.


**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Como estamos a falar de argumeto de funções, destaco algo importante da linguagem R. Ao se utilizar o operador `<-` para realizar uma atribuição em uma chamada de função, a variável é ligada fora da função, ou seja, no ambiente em que a função é chamada, como mostra o exemplo que segue:

   **Exemplo**:
</div>\EndKnitrBlock{rmdimportant}

```r
y <- 0
f <- function(x){
   y <- 2
   x + 1
}
f(y <- 7)
```

```
## [1] 8
```

```r
y
```

```
## [1] 7
```

Perceba que fazer `f(y = 7)` retornará um erro, uma vez que R entende que estamos passando o valor `7` à um argumento `y` que não existe em `f()`. Note que `f(y <- 7)` é equivalente a escrever `f(x = y <- 7)` ou `f(x = (y = 7))`. Porém, ao utilizarmos o operador `<-`, além de passarmos os argumentos à `f()` estamos também criando os objetos à esquerda do operador fora da função.
</div>

### varargs: ... (dot-dot-dot)

Algo bastante útil e que torna flexível uma linguagem de programação é a possibilidade de escrever funções com quantidade variádicas de argumentos, isto é, funções [**varargs**](https://en.wikipedia.org/wiki/Variadic_function). Em R isso é possível especificando o argumento especial `...` (***dot-dot-dot***), ou **ponto-ponto-ponto**, em português.

Um uso comum do operador `...` é a possibilidade de passarmos argumentos adicionais para uma função que utilizamos em nossa implementação. Por exmeplo, considere o código abaixo:



```r
# Fixando uma semente para gerarmos sempre a mesma amostra.
set.seed(0)

# Gerando um conjunto de dados com distribuição normal padrão.
data <- rnorm(n = 100, mean = 0, sd = 1)
myhist <- function(x = data, ...){
  # Perceba o uso de ... em hist():
  result <- hist(x, ...)
  list(n = length(result$counts), counts = result$counts)
}

# A função myhist() não possuia a definição dos argumentos col,
# main, ylab e border.
myhist(x = data, col = rgb(1, 0.9, 0.8), main = "",
       ylab = "Frequência", border = NA)
```

<img src="r_files/figure-html/unnamed-chunk-47-1.png" width="384" style="display: block; margin: auto;" />

```
## $n
## [1] 10
## 
## $counts
##  [1]  1  2  8 15 26 19 14 12  1  2
```

A função `myhist()`, implementada acima, constroi um histograma com base em um vetor de dados passado como argumento à `x`, retornando uma lista com o número de classes e a quantidade de observações da amostra, em cada uma das classes. Note que `myhist()` possui apenas dois argumentos, `x` e `...`, respectivamente. O argumento especial `...` permite que `myhist()` herde todos argumentos da função `hist()`. Asim, muito embora a função `myhist()` não possui os argumentos `col`, `main`, `ylab`e `border` definidos formalmente, poderemos ascessar esses e os demais argumentos de `hist()` mesmo sem defini-los.

Nas situações em que desejarmos acessar os elementos passados à `...` por suas posições, poderemos fazer uso da notação especial `..1`, `..2`, etc. Considere o trecho de código que segue:


```r
f <- function(...){

   n <- ...length()
   if (n != 3)
      stop("A função deve ter exatamente 3 argumentos.")
   else
      for(i in 1:...length()){
         cat("O elemento ", i, " de \"...\" é: ", ...elt(i), "\n")
      }

   return(..1 * ..2 + ..3)
}
f(2, 3, 1)
```

```
## O elemento  1  de "..." é:  2 
## O elemento  2  de "..." é:  3 
## O elemento  3  de "..." é:  1
```

```
## [1] 7
```

Note que a função `f()` retorna o produto do primeiro com o segundo argumento e soma com o terceiro. Além disso, foram utilizadas as funções `...length()` que retorna o tamanho de `...` e `...elt(i)` que equivale à `..i`. A função `...elt(i)` nada mais é do que fazer `eval(paste0("..", n))`.

Como dito, uma das grandes vantagens do uso de `...` é a possibilidade de passarmos argumento de outras funções que estão sendo utilizadas pela função que estamos a implementar. O uso de funções **varargs** destacam-se também em situações em que fazemos uso de programação orientada à objeto por função genérica, sistema de orientação à objeto conhecido, em R, como sistema S3 de orientação à objeto e que estudaremos mais a frente. Considerando o sistema S3 de orientação à objeto, note que funções como `summary()` e `print()` podem ser utilizadas em diversas situações e que muito provavelmente terão argumentos distintos em cada uma dessas circunstâncias. A capacidade de uma função ter várias formas e se adequar a cada uma delas está fortemente relacionada com a definição de funções [**polimórficas**](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)), uma das principais características do paradigma de programação orientada à objeto e que está intimamente relacionadas com funções **varargs**, principalmente no sistema S3.

Perceba que diversas funções R são **varargs**, por exemplos, a função `sum()`. Note, no trecho de código abaixo, que a característica de ***lazy evaluation*** quando associada à uma função com um número arbitrário de argumentos poderá retornar algo equivocado e nenhum erro é dado para nos alertarmos de um possível problema:


```r
   sum(1:5, NA, narm = TRUE)
```

```
## [1] NA
```

Para o código acima, gostaríamos que o equívoco a respeito do nome correto do argumento (`na.rm`) não tivesse ocorrido. Aqui, nosso interesse seria fazer:


```r
   sum(1:5, NA, na.rm = TRUE)
```

```
## [1] 15
```


**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Um outro inconveniente de construir funções **varargs** além dos equívocos desarpesebidos quando erramos algum de seus arugmentos é que essas funções normalmente são um pouco mais complicadas de serem documentadas, visto que devemos ter um grande cuidado ao deixar claro como os argumentos serão substituídos e utilizados.

Esses problemas não são suficientes justificar um desaconselho do uso de funções **varargs**. Na verdade é muito importante a construção de funções **varargs** e você deve utilizar, sempre que puder e na medida da necessidade, uma vez que isto tornará suas funções bastante flexíveis.
</div></div>\EndKnitrBlock{rmdnote}

### Funções infixas

Para começarmos a falar de funções infixas (***infix***), os slogans abaixo, traduzidos para o português, poderão ser úteis para um melhor entendimento:

> "Para entender a computação em R, dois slogans são úteis:

> * Tudo o que existe é um objeto.
> * Tudo o que acontece é uma chamada de função."

> --- [**John M. Chambers**](https://en.wikipedia.org/wiki/John_Chambers_(statistician)), no artigo intitulado [***Object-Oriented Programming, Functional Programming and R***](https://projecteuclid.org/download/pdfview_1/euclid.ss/1408368569), *Statistical Science*, Vol. 29, 2014, p. 170.

Nas situações de funções que possuem dois argumentos, construir um operador infixo pode ser de grande utilidade. O exemplo abaixo mostra duas formas de somarmos dois termos utilizando a função \`+\` e o operador infixo `+`, respectivamente. Perceba que a segunda forma é mais conveniente que a primeira:


```r
x <- y <- 1

# Forma 1 (prefix):
`+`(x, y)
```

```
## [1] 2
```

```r
# Forma 2 (infix):
x + y
```

```
## [1] 2
```

Além dos operadores matemáticos `+`, `-`, `*` e `/` serem funções infixas, podendo também chamar de operadores infixos ou ***infix***, diversas outras funções são infixas, como por exemplo, `^`, `::`, `&`, `|`, `&&`, `||`, `<=`, `>=`, `<`, `>`, `==`, `!=`, `$`, `%%`, `%*%`, `%in%`, `<-`, `<<-`, entre diversas outras funções. O exemplo abaixo apreseta o uso de algumas dessas funções na forma prefixa:


```r
`<=`(1,3)
```

```
## [1] TRUE
```

```r
`^`(2,3)
```

```
## [1] 8
```

```r
x <- list(a = 1, b = 2)
`$`(x, a)
```

```
## [1] 1
```

Assim como existem diversas funções infixas em R previamente implementadas, também poderemos construir nossas funções infixas. Para tanto, basta considerarmos a notação `%nome%`, em que `nome` deverá ser substituído por um nome válido de função. Considere o código abaixo:


```r
`%+%` <- function(x, n){
   rep(x, times = n)
}

# Forma prefixa:
`%+%`("infix", 4)
```

```
## [1] "infix" "infix" "infix" "infix"
```

```r
# Forma infixa:
"infix" %+% 4
```

```
## [1] "infix" "infix" "infix" "infix"
```

### Função de substituição

Você muito provavelmente já deve ter feito uso de funções de substituição, como por exemplo, `names()`, `colnames()`, `rownames()`, entre outras funções. Essas são chamadas de funções de substituição devido ao comportamento que é expresso no código que segue:


```r
vetor <- c(1,2,3)
names(vetor) <- c("a", "b", "c")
x
```

```
## $a
## [1] 1
## 
## $b
## [1] 2
```

A função `names()`, para produzir o mesmo resultado do código acima, poderia ser invocada na foma que segue:


```r
vetor <- c(1,2,3)
`names<-`(x = vetor, value = c("a", "b", "c"))
```

```
## a b c 
## 1 2 3
```

Pelo código acima podemos perceber que as funções de substituição nada mais são que funções de dois argumentos, a saber `x` e `value`, respectivamente. Dessa forma, os valores passados à `value` modificam o objeto `x` que nesse caso são os nomes do objeto `vetor`.

**Exemplo**: Implementação da função de substituição `samenames()` que atribui o mesmo nome à todos elementos do vetor `x`.


```r
`samenames<-` <- function(x, value){
   if (length(value) != 1) stop("Um vetor de comprimento 1 deverá ser atribuído.")
   else{
      names(x) <- rep(value, times = length(x))
   }
   x
}
x <- 1L:10L
samenames(x) <- "a"
x
```

```
##  a  a  a  a  a  a  a  a  a  a 
##  1  2  3  4  5  6  7  8  9 10
```

Em situações em que a função de substituição necessita de mais argumentos além dos argumentos obrigatórios `x` e `value`, deveremos colocá-los entre os argumentos `x` e `value`. No exemplo do código abaixo introduzimos o argumento `rm.id` em que, se desejarmos, poderemos omitir algumas posições do vetor `x`:



```r
`samenames<-` <- function(x, rm.id = NULL, value){

  if (length(value) != 1) stop("Um vetor de comprimento 1 deverá ser atribuído.")
  else if (!is.null(rm.id) && is.numeric(rm.id)){
    x <- x[-rm.id]
    names(x) <- rep(value, times = length(x))
  }else{
    names(x) <- rep(value, times = length(x))
  }
  x
}
x <- 1L:10L
samenames(x) <- "a"
# Removendo a primeira e a décima posição de x.
samenames(x, c(1,10)) <- "a"
x
```

```
## a a a a a a a a 
## 2 3 4 5 6 7 8 9
```

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
A linguagem R possui diversos outros recursos, escritos em forma especial, que também são funções. Abaixo pontuarei alguns desses recursos, para que você tenha uma ideia, porém, existem mais:

   * `(x)` com representação prefixa dada por `` `(`(x) ``;
   * `x[i]` com representação prefixa dada por `` `[`(x, i) ``;
   * `x[[i]]` com representação prefixa dada por `` `[[`(x, i) ``;
   * `{x}` com representação prefixa dada por  `` `{`(x) ``;
   * `if(condicao)` com representação prefixa dada por `` `if`(condicao, se_verdade, se_falso) ``;
   * `for(variável in conjunto) ação` com representação prefixa dada por `` `for`(variável, conjunto, ação) ``;
   * `while(condição) ação`  com representação prefixa dada por `` `while`(cond, action) ``.
</div></div>\EndKnitrBlock{rmdobservation}

### Closures

Como já sabemos, uma utilidade comum de funções anônimas está em criar pequenas funções que não vale a pena nomear. Normalmente são funções pequenas que são passadas como argumento à outras funções, fornecendo assim menos ruídos visuais no código e nos livrando da necessidade de pensarmos em um bom nome para a função.

Um outro importante uso de funções anônimas está na necessidade [**closures**](https://en.wikipedia.org/wiki/Closure_(computer_programming)). O conceito de **closures** surgiu na década de 1960 para avaliação de expressões no [**$\lambda$-calculus**](https://en.wikipedia.org/wiki/Lambda_calculus) (um sistema formal na lógica matemática para representar a computação com base na abstração de funções) e teve sua primeira implementação computacional em 1970 como um recurso da linguagem de programação [**PAL**](https://en.wikipedia.org/wiki/PAL_(programming_language)). Com o passar dos anos, diversas linguagens de programação permitiram o uso de **closures**, um recurso de programação muito utilizado quando necessitamos criar funções escritas por outras funções:

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
**Closure** possui esse nome por se tratar de uma função que encerra o seu ambiente, passando seus parâmetros para o ambiente da função mais interna, função esta que será retornada e que executará o trabalho desejado.
</div></div>\EndKnitrBlock{rmdnote}

O trecho de código abaixo exemplifica o uso de **closure**, em que a função `potencia()` (função pai) poderá gerar novas funções de interesse, cujo trabalho será executado pela função anônima interna à função `potencia()`. Por exemplo, poderemos criar os objetos `quadrado` e `cubo` que serão as funções `quadrado()` e `cubo()`, respectivamente, sem a necessidade de implementar cada uma dessas funções.



```r
potencia <- function(expoente) {
   # Função anônima.
   function(x) {
      x ^ expoente
   }
}

# Criando as funções quandrado() e cubo().
quadrado <- potencia(2)
cubo <- potencia(3)

# Utilizando as funções criadas pela função potencia():
quadrado(2)
```

```
## [1] 4
```

```r
cubo(3)
```

```
## [1] 27
```

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Perceba que as funções `quadrado()` e `cubo()` não foram implementadas diretamente. Além disso, nesse caso, note essas funções retornadas aos objetos `quadrado` e `cubo` são funções que possuem `x` como argumento que era argumento da função anônima.
</div></div>\EndKnitrBlock{rmdimportant}


### Exercícios {-}

1. Quais são os três componentes de uma função?

2. Contrua o objeto `y` que retorne a saída abaixo:

    
    ```
    ##  [1]  1  2  3  4  5  6  7  8  9 10
    ## attr(,"att_1")
    ## [1] "Isso é um atributo"
    ```

3. Remova o atributo `att_1` do objeto `y` acima.

4. O que o código abaixo retorna? Explique. **Dica**: para certificar-se que esteja entendendo, tente prever sem executar a função.

    
    ```r
    f <- function(x){
       f <- function(x){
          f <- function(x){
             x * 3
          }
          f(x) * 2
       }
       f(x) + 1
    }
    f(7)
    ```

5. O que o código abaixo retorna? Explique. **Dica**: para certificar-se que esteja entendendo, tente prever sem executar a função.

    
    ```r
       x <- 1
       f <- function() {
          x <- 0
          x <<- x + 1
          x
       }
       f(); x
    ```


6. O que o código abaixo retorna? **Dica**: para certificar-se que esteja entendendo, tente prever sem executar a função.

    
    ```r
    f <- function(){
       y <- 0
       g <- function(){
          y <<- y + 1
       }
       list(rep(x = g(), times = y), rep(x = g(), times = y), rep(x = g(), times = y))
    }
    ```

7. Implemente a função `%+%` que concatena duas strings. Permita que, por meio do uso prefixo da função, o usuário possa informar o caractere que separa as duas strings. Abaixo encontra-se um exemplo do uso infixo da função.

    ```
    "Estatística" %+% "Computacional"

    ## [1] "Estatística Computacional"
    ```

8. Implemente a função segundo que trabalhe da seguinte forma:

    ```
       x <- 1:10
       segundo(x) <- 5
       x

       ## [1] 1 5 3 4 5 6 7 8 9 10
    ```

9. Implemente a função `troca()` que trabalhe da forma abaixo:

    ```
       x <- 1:10
       troca(x, 2) <- 7
       x

       ## [1] 1 7 3 4 5 6 7 8 9 10
    ```

9. Qual o retorno da função abaixo? Explique.

    
    ```r
    f <- function(y) {
        function(x) {
           x + y
        }
    }
    g <- f(1)
    g(x = 2)
    ```

10. Utilizando o conceito de **closure** e o operador `...` (**dot-dot-dot**), construa a função `cdf_expg(G)` que recebe como argumento uma função de distribuição (**qualquer**), seja ela denotada por $G$. A função `cdf_expg(G)` deverá retornar a função de distribuição $\mathrm{Exp}-G$ definida por 
$$F(x) = G^a(x),$$
com $a > 0$. Perceba que $F$ é uma nova distribuição de probabilidade com um parâmetro a mais ($a > 0$) e que possui a distribuição $G$ como caso particular quando $a = 1$. Por exemplo, se `cdf_weibull` é a implementação da distribuição Weibull, então `cdf_expg(G = cdf_weibull)` deverá retornar uma função que implementa a distribuição $\mathrm{Exp-Weibull}$. 

<!-- cdf_weibull <- function(alpha, beta, x){ -->
<!--   pweibull(q = x, shape = alpha, scale = beta) -->
<!-- } -->

<!-- cdf_expg <- function(G){ -->
<!--   function(x, a, ...){ -->
<!--     G(x, ...) ^ a -->
<!--   } -->
<!-- } -->

<!-- cdf_expweibull <- cdf_expg(G = cdf_weibull) -->

## Funcionais

Funcionais não são nada a mais que funções que recebe como argumento uma outra função como argumento e retorna um vetor como saída. O trecho de código que segue implementa o funcional `f()`, retornando um vetor como saída:


```r
# A função f() é um funcional.
f <- function(x, func) func(x)

# Passando uma função à f() por meio do argumento func.
# Foi passado à func uma função anônima.
f(x = c(1, 2, 7, 10), func = function(x) x + 1)
```

```
## [1]  2  3  8 11
```

Perceba que a função `f()` é um funcional, visto que `f()` recebe uma função por meio do argumento `func` e retorna um vetor como saída, que nesse caso é o vetor passado ao argumento `x` de `f()` acrescido de um. Considere agora o trecho que segue:


```r
f <- function() mean(runif(n = 10, min = 0, max = 1))
# A função loop() é um funcional.
loop <- function(x, func) {
   resultado <- NULL
   for (i in seq_along(x))
      resultado <- c(resultado, func())
   resultado
}

loop(x = 1:3, func = f)
```

```
## [1] 0.3702804 0.7174270 0.3805153
```

```r
loop(x = 1:7, func = f)
```

```
## [1] 0.5092227 0.4038002 0.5425011 0.5148392 0.2298425 0.3374357 0.3344574
```

A função `loop()` é um funcional que reproduz a função passada ao argumento `func` um quantidade qualquer de vezes. No exemplo acima, `loop(x = 1:3, func = f)` e `loop(x = 1:7, func = f)` reproduz `f()` 3 (três) e 7 (sete) vezes, respectivamente. Em situações em que você deseja reproduzir uma função ou aplicá-la à cada posição de um vetor ou lista e isso se repete por diversas partes do seu código, o uso de um funcional poderá deixar seu código mais limpo, sem a necessidade de escrever muitas estruturas de repetições. No exemplo acima, se em outra parte do código houvesse a necessidade de reproduzir `f()` 10 (dez) vezes, bastaria fazer `loop(x = 1:10, func = f)` ao invés de escrever novamente um laço com alguma estrutura de repetição.

Escrever estruturas de repetições, na forma acima, não é muito útil do ponto de vista de desempenho computacional, uma vez que não há melhoria no desempenho do código que seria obtido ao se implementar os loops sem o uso do funcional `loop()`. Nesse exemplo, toda vez que chamamos `loop()`, o que internamente está sendo feito é um loop utilizando a estrutura de repetição `for`. A melhor forma, em R, de se fazer uso de funcionais é considerar os que já estão implementados de forma consistente, utilizando linguagens mais eficientes, como, por exemplo, os funcionais de R escritos em C/C++ ou Fortran (códigos mais antigos) e que estão disponíveis no **R base** ou em pacotes suplementares. Fazer uso desses funcionais nos trará o benefício de escrever estruturas de repetições sem a necessidade de implementar essa estrutura toda vez que necessitarmos, além do benefício de substituir uma estrutura de repetição de R, que naturalmente são lentas, por funcionais que são muito mais eficientes.

> "Para se tornar significativamente mais confiável, o código deve se tornar mais transparente. Em particular, condições aninhadas e loops devem ser vistos com grande suspeita. Fluxos de controle complicados confundem os programadores. O código bagunçado geralmente esconde bugs."

> --- [**Bjarne Stroustrup**](https://pt.wikipedia.org/wiki/Bjarne_Stroustrup), criador da linguagem de programação [**C++**](https://pt.wikipedia.org/wiki/C%2B%2B).

### Funcionais do R Base

O pacote **base** da linguagem R (algumas vezes chamo de **R Base**) possui alguns funcionais que podem ser bastante úteis em diversas situações. Tentar evitar escrever estruturas de repetições por meio do uso de funcionais é uma prática útil e algo bastante comum em linguagens de programação com [**paradigma funcional**](https://en.wikipedia.org/wiki/Functional_programming) e em linguagens multiparadigmas, como é o caso da linguagem R.

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Poderá existir diversas situações que não poderemos escapar do uso de estruturas de repetições, no caso do R, das estruturas `for`, `while` e `repeat`. Porém, existem diversas outras situações que aquilo que encontra-se dentro do loop é uma estrutura bem definida que poderá ser envolvida em uma função e repetida por um funcional. Dessa forma, sempre procure checar se você poderá envolver em uma função o conteúdo que seria colocado no interior de uma estrutura de repetição. Passar esse conteúdo como uma função à um funcional poderá trazer benefícios ao seu código.
</div></div>\EndKnitrBlock{rmdobservation}

#### apply()

Trata-se de um funcional bastante conhecido em R, implementado no **R Base**. O funcional `apply()` é normalmente utilizado quando desejamos aplicar uma função em uma das dimensões de uma matriz, data frame ou tibble, sendo este último um estrutura de dados do pacote [**tibble**](https://tibble.tidyverse.org/). A estrutura tibble trata-se de uma releitura moderna de um data frame com um método `print()` aprimorado. Porém, não se preocupe, quase tudo que você sabe sobre data frame será válido para um objeto da classe **tbl**. A forma geral do funcional `apply()` é dada por:


```r
apply(X, MARGIN, FUN, ...)
```
em que: 

   * `X`: é a matriz/data frame ou tibble em que será aplicada uma função sobre seus elementos;
   
   * `MARGIN`: indica a dimensão em que a função irá ser aplicada. Se `MARGIN = 1` (padrão), temos que uma dada função será aplicada sobre as linhas de do objeto `X`. Fazendo `MARGIN = 1`, temos que uma dada função será aplicada sobre todas as colunas do objeto `X`;
   
   * `FUN`: função que iremos aplicar em uma das dimensões do objeto `X`. Dessa forma, o funcional `apply()` tomará cada linha ou coluna (a depender de `MARGIN`) como sendo o primeiro arugmento da função passada à `FUN`;
   
   * `...`: operador [**dot-dot-dot**][varargs: ... (dot-dot-dot)] discutido em tópicos anteriores. Isso permitirá que possamos acessar os argumentos da função passada à `FUN` passando estes argmento ao funcional `apply()`.
   
**Exemplo**: Aplicando a função `mean()` sobre linhas e colunas do objeto `M` (uma matriz). O uso do funcional `apply()` seria equivalente se `M` fosse um data frame ou uma tibble.


```r
# Construindo a matriz m de orden 5x5.
M <- matrix(data = 1:25, nrow = 5, ncol = 5)
# Aplicando a função mean() sobre cada linha de m.
apply(X = M, MARGIN = 1, mean)
```

```
## [1] 11 12 13 14 15
```

```r
# Aplicando a função mean() sobre cada coluna de m.
apply(X = M, MARGIN = 2, mean)
```

```
## [1]  3  8 13 18 23
```

#### lapply(), sapply() e vapply()

Os funcionais `lapply()`, `sapply()` e `vapply()` foi introduzido o mesmo tópico, visto que eles tem muito em comum. Tais funcionais permitem que venhamos aplicar uma função à elementos de um vetor ou elementos de uma lista. 

**Uso**:


```r
lapply(X, FUN, ...)

sapply(X, FUN, ..., simplify = TRUE)

vapply(X, FUN, FUN.VALUE, ...)
```

O funcional `lapply()` retorna uma lista do mesmo tamanho que `X`, em que cada elemento é o resultado da aplicação de `FUN` no elemento correspondente de `X`. Já o funcional `sapply()` é bastante semelhante ao funcional `lapply()`, sendo o retorno a diferença mais notável, visto que `lapply()` sempre retornará uma lista e `sapply()` retorna uma estrutura que melhor poderá comportar as informações, havendo uma espécie de simplificação da estrutura a ser retornada. Considere o trecho de código que segue


```r
# Criando um vetor double.
x <- list(c(1,7,4,3), c(1,2,3,6))
# A função f() retorna uma matrix de caracter.
f <- function(x){
   as.character(round(sin(x), digits = 2))
}

lapply(X = x, FUN = f)
```

```
## [[1]]
## [1] "0.84"  "0.66"  "-0.76" "0.14" 
## 
## [[2]]
## [1] "0.84"  "0.91"  "0.14"  "-0.28"
```

```r
sapply(X = x, FUN = f)
```

```
##      [,1]    [,2]   
## [1,] "0.84"  "0.84" 
## [2,] "0.66"  "0.91" 
## [3,] "-0.76" "0.14" 
## [4,] "0.14"  "-0.28"
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Perceba que para o exemplo acima, `lapply(X = x, FUN = f)` equivale a fazer `sapply(X = x, FUN = f, simplify = FALSE)`.
</div></div>\EndKnitrBlock{rmdnote}

Por sua vez, o funcional `vapply()` é bastante similar ao funcional `sapply()`, porém, podemos especificar os tipos de valor de retorno. Considere o trecho de código abaixo que mostra o uso da função `vapply()`. Perceba, no código de segue, que `FUN.VALUE` recebe como argumento o tipo esperado de retorno da função `f()` e o tamanho do vetor retornado ao aplicar a função `f()` à cada elemento da lista passada à `X`.


```r
# Criando um vetor double.
x <- list(c(1,7,4,3), c(1,2,3,6))
# A função f() retorna uma matrix de caracter.
f <- function(x){
  as.character(trunc(sum(x)))
}

# O retorno será uma matriz.
resultado <- vapply(X = x, FUN = f, FUN.VALUE = character(1))
resultado
```

```
## [1] "15" "12"
```

**Nota**: 

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
O funcional `vapply()` poderá dar um pouco mais de segurança quando comparado ao funcional `sapply()`, visto que poderemos especiticar o tipo de retorno esperado. Dessa forma, é de se esperar que a função `vapply()` poderá "reclamar" um pouco mais que a função `sapply()`. 
</div></div>\EndKnitrBlock{rmdnote}

#### Map(), mapply()

Considere a função `mp()` que recebe como argumento dois vetores de mesmo comprimento e que calcula a média ponderada do vetor passado ao argumento `x` considerando um vetor de pesos passado à `y`.


```r
mp <- function(x, y){
   # x é o vetor que desejamos calcular a média ponderada.
   # y é o vetor de pesos.
   if (length(x) != length(y)) 
      stop("O vetor x deve ter o mesmo comprimento do vetor de pesos y.")
   sum(x*y)/sum(y)
}
mp(x = c(4, 6.5), y = c(6, 4))
```

```
## [1] 5
```

Considerando algum dos funcionais apresentados anteriormente, poderemos facilmente aplicar `mp()` à todos elementos de uma lista de vetores com vetor de pesos fixos, como mostra o código abaixo:


```r
mp <- function(x, y){
   # x é o vetor que desejamos calcular a média ponderada.
   # y é o vetor de pesos.
   if (length(x) != length(y)) 
      stop("O vetor x deve ter o mesmo comprimento do vetor de pesos y.")
   # Média ponderada.
   sum(x*y)/sum(y)
}

valores <- list(c(7.3, 3.2, 1.5), c(8.4, 4.7, 5.1), c(10, 9.7, 9.6), c(8.5, 7.2, 7.7))
pesos <- c(5, 3, 2) # Pesos fixos.

# Usando lapply():
lapply(X = valores, FUN = mp, y = pesos)
```

```
## [[1]]
## [1] 4.91
## 
## [[2]]
## [1] 6.63
## 
## [[3]]
## [1] 9.83
## 
## [[4]]
## [1] 7.95
```

```r
# Usando sapply():
sapply(X = valores, FUN = mp, y = pesos, simplify = TRUE)
```

```
## [1] 4.91 6.63 9.83 7.95
```

```r
# Usando vapply():
vapply(X = valores, FUN = mp, y = pesos, FUN.VALUE = double(1))
```

```
## [1] 4.91 6.63 9.83 7.95
```

Ao contrário dos funcionais anteriores, em que apenas um dos argumentos da função varia, os funcionais `Map()` e `mapply()` permitirão que outros argumentos da função possa também variar. Por exemplo, considere uma pequena modificação do caso anterior, com a diferença de que o objeto `pesos` será uma lista de pesos. Esse problema poderá ser resolvido utilizando o funcional `Map()` e `mapply()`, como mostra o exemplo abaixo:


```r
mp <- function(x, y){
   # x é o vetor que desejamos calcular a média ponderada.
   # y é o vetor de pesos.
   if (length(x) != length(y)) 
      stop("O vetor x deve ter o mesmo comprimento do vetor de pesos y.")
   # Média ponderada.
   sum(x*y)/sum(y)
}

valores <- list(c(7.3, 3.2, 1.5), c(8.4, 4.7, 5.1), c(10, 9.7, 9.6), c(8.5, 7.2, 7.7))
pesos <- list(c(5, 3, 2), c(3, 6, 1), c(4, 4, 2), c(7, 1, 2)) # Pesos não fixados.
# Utilizando o funcional Map().
Map(f = mp, x = valores, y = pesos)
```

```
## [[1]]
## [1] 4.91
## 
## [[2]]
## [1] 5.85
## 
## [[3]]
## [1] 9.8
## 
## [[4]]
## [1] 8.21
```

```r
# Utilizando o funcional mapply().
mapply(FUN = mp, x = valores, y = pesos)
```

```
## [1] 4.91 5.85 9.80 8.21
```

**Importante**: 

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
   * O funcional `mapply()` funciona de forma bastante semelhante à `Map()`, retornando um vetor ao invés de uma lista.
   
   * A linguagem R possui um função para o cálculo de média ponderanda. Veja a documentação da função `weighted.mean()`. Implementamos a função `mp()` apenas para deixar claro que os funcionais se aplicam à qualquer função de R, incluindo as funções que implementamos.
</div></div>\EndKnitrBlock{rmdimportant}

### Funcionais do pacote purrr

O pacote [**purrr**](https://purrr.tidyverse.org/) aprimora o conjunto de ferramentas de programação funcional da linguagem R. Este pacote fornece um conjunto completo, consistente e eficiente de ferramentas para trabalhar com funções e vetores. O pacote **purrr** encontra-se no CRAN (***Comprehensive R Archive Network***) do R e você poderá instalar facilmente fazendo `install.packages("purrr")`. Se desejar, você poderá instalar a versão do pacote mantida no GitHub fazendo `devtools::install_github("tidyverse/purrr")`, nesse caso, será preciso ter instalado o pacote [**devtools**](https://github.com/r-lib/devtools).


<div class="figure" style="text-align: center">
<img src="images/logo_purrr.png" alt="Logo do pacote [**purrr**](https://purrr.tidyverse.org/) de autoria de [**Hadley Wickham**](https://github.com/hadley) (autor) e e [**Lionel Henry**](https://github.com/lionel-) (autor e mantenedor)." width="25%" />
<p class="caption">(\#fig:unnamed-chunk-82)Logo do pacote [**purrr**](https://purrr.tidyverse.org/) de autoria de [**Hadley Wickham**](https://github.com/hadley) (autor) e e [**Lionel Henry**](https://github.com/lionel-) (autor e mantenedor).</p>
</div>

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
As funções do pacote **purrr** são implementadas na linguagem C. Dessa forma, são funções tão eficientes quanto àquelas que são fornecidas pelos funcionais do R Base, com a vantagem de ser menos verbosas.
</div></div>\EndKnitrBlock{rmdnote}

#### map() e variantes

O funcional `map()` é a função principal do pacote **purrr**, em que recebe como primeiro argumento um vetor/lista,  uma função como segundo argumento e necessário, um conjunto de argumentos passado da função atribuida.

**Forma geral de uso**:


```r
map(.x, .f, ...)
map_int(.x, .f, ...)
map_dbl(.x, .f, ...)
map_lgl(.x, .f, ...)
map_chr(.x, .f, ...)
```
em que,

   * `.x`: é uma lista ou vetor atômico;

   * `.f`: uma função, fórmula (por exemplo `~ .x + 2`) ou um vetor/lista.

   * `...`: um conjunto adicional de argumentos que são mapeados para o objeto passada para o argumento `.f`;

**Exemplo**: Utilizando o funcional `map()` que aplica a função `sinal()` à cada elemento de um vetor atômico. A função irá retornar `"-"`, `"0"` ou `"+"`, a depender do valor passado à `x` em `f()`.


```r
sinal <- function(x){
   # Varificando a classe de x e parando a execução da função
   # se x não for um objeto da classe numeric.
   if (!is.numeric(x)) stop ("x deve ter a classe numérica.")

   if (x == 0) "0"
   else if (x > 0) "+"
   else "-"
}

x <- c(1.7, -2.01, 0, 12)
purrr::map(.x = x, .f = sinal)
```

```
## [[1]]
## [1] "+"
## 
## [[2]]
## [1] "-"
## 
## [[3]]
## [1] "0"
## 
## [[4]]
## [1] "+"
```

Perceba que o retorno de `map()` é uma lista assim como obteriamos ao utilizarmos o funcional `lapply()`. O exemplo acima poderia ser resolvido, com `lapply()`, fazendo `lapply(X = x, FUN = sinal)`. A grande vantagem do uso do funcional `map()` do pacote **purrr** é que podemos fazer uso de sufixos que nos ajudam na tarefa de converter o resultado para um vetor atômico do tipo desejado, utilizando alguma de suas variantes: `map_lgl()` (retorno de um vetor com elementos do tipo logical), `map_int()` (retorno de um vetor com elementos do tipo integer), `map_dbl()` (retorno de um vetor com elementos do tipo double) e `map_chr()` (retorno de um vetor com elementos do tipo character).

**Exemplo**: Utilizando `map_chr()` para obtenção de um vetor de caracteres como saída. Isso evito termos que efetuar `unlist()` para transformarmos uma lista em um vetor atômico.


```r
purrr::map_chr(.x = x, .f = sinal)
```

```
## [1] "+" "-" "0" "+"
```

Para o argumento `.f` do funcional `map()` bem como de seus variantes (`map_lgl()`, `map_int()`, `map_dbl()` e `map_chr()`), poderemos passar uma função anônima ou uma fórmula. Os três exemplos que seguem apresentam o uso do funcinal `map()` ou alguma de suas variantes, considerando funções com 1 (um), 2 (dois) ou 3 (três) argumentos. Independentemente de qual(is) varantiante(s) de `map()` for/forem utilizada(s) nos exemplos, o uso de todas as variântes são equivalentes.

**Exemplo (um argumento)**: Uso do funcional `map_int()` para uma função com um único argumento. Nesse exemplo, desejamos somar 1 à cada elemento do vetor atômico (vetor homogêneo) `x <- 1L:10L`. Note que, nesse exemplo, resolvemos o problema de somar o valor 1 (do tipo inteiro) aos valores de `x`, de 4 (quatro) formas distintas. Na primeira forma, definimos a função `soma1()` e passamos a função como argumento à `.f` do funcional `map_int()`. Na segunda forma, optou-se em passar uma função anônima para o argumento `.f`, uma vez que a função é curta e não necessitaríamos nos preocupar em atribuir um nome à ela. Nessa segunda forma, não haveria a necessidade da definição da função `soma1()`, uma vez que definimos a função diretamente no funcional, sem a necessidade de atribuição de um nome. Já na terceira e quarta forma, note que optamos em passar um objeto da classe **formula** (note o til, `~`). Como trata-se de uma função com um único argumento, podemos definir esse argumento por `.x` ou `.`.


```r
x <- 1L:10L
soma1 <- function(x) x + 1L
# Foma 1: Passando à .f uma função soma1().
purrr::map_int(.x = x, .f = soma1)
# Forma 2: Passando à .f uma função anônima.
purrr::map_int(.x = x, .f = function(x) x + 1L)
# Forma 3: Passando à .f uma formula.
purrr::map_int(.x = x, .f = ~ .x + 1L)
# Forma 4: Para funções com um único argumento, você poderá substituir
# .x na fórmula passada ao argumento .f por um "." (ponto).
purrr::map_int(.x = x, .f = ~ . + 1L)
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
É claro que poderiamos resolver o exemplo acima sem uso de funcional algum, uma vez que a linguagem R é vetorizada e poderiamos simplesmente fazer `x + 1L` para assim obtermos um vetor de interio. Porém, isso é um exemplo didático, em que o objetifo aqui é entender os funcionais do pacote **purrr** e não perdermos mais tempo com o entendimento da função passada ao funcional. Sempre tenha em mente que a função passada à `.f`, na maioria das vezes, não será tão simples a ponto de justificar resolver o problema sem o uso de um funcional.
</div></div>\EndKnitrBlock{rmdnote}

**Exemplo (dois argumentos)**: Uso do funcional `map()`, em que é aplicado a função `f()` sobre todos os elementos da lista `x`. O exemplo mostra que a função `map()` varia sobre os elementos do primeiro argumento `.x` e fixa o segundo argumento. Além disso, note que é possível passar uma função anônima ou uma fórmula ao argumento `.f` do funcional `map()`, assim como no exemplo anterior. Para o caso de passagem de uma fórmula, podemos utilizar `.` ou `.x` para se referir ao primeiro argumento de `f()` e `.y` para fazer referência ao segundo argumento.


```r
x <- list(c(1.1,4.07,3.76), c(7.1,2.2), 1:10)
y <- c(1,2,7,4,2)
f <- function(x, y) 2 * x + sum(sqrt(y))
# Forma 1: Passando a função f() para o argumento .f
# de map_dbl().
purrr::map(.x = x, .f = f, y = y)
# Forma 2: Passando uma função anônima de dois argumentos.
purrr::map(.x = x, .f = function(x, y) 2 * x + sum(sqrt(y)) , y = y)
# Forma 3: Utilizamos .x e .y em situações de funções com 2 argumentos.
purrr::map(.x = x, .f = ~ 2 * .x + sum(sqrt(.y)), .y = y)
# Forma 4: Aqui o x .x será substituido na ocorrência de "." (ponto).
purrr::map(.x = x, .f = ~ 2 * . + sum(sqrt(.y)), .y = y)
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Note que nesse exemplo não poderemos fazer uso das variantes do funcional `map()`. Isso se deve ao fato de `x` ser uma lista, o que implica que a função `f()` será aplicada à cada elemento da lista `x`. Sendo assim, esperamos que o retorno de `map()` será uma lista com a mesma quantidade de elementos de `x`.
</div></div>\EndKnitrBlock{rmdnote}


**Exemplo (três ou mais argumentos)**: Esse exemplo é muito parecido com o exemplo antrior (função `f()` com 2 (dois) argumentos). Aqui, temos que a função `f()` possui 3 (três) argumentos. Perceba porém, que ao se passar uma fórmula ao argumento `.f` do funcional `map()`, poderemos nos referir ao terceiro argumento com a notação `..3`.


```r
x <- list(1:3, 2:7, 8:10)
y <- 1:3
z <- c(2,3,5)
f <- function(x, y, z) x * y + 2 * z
# Forma 1: Passando a função f() para o argumento .f
# de map_dbl().
purrr::map(.x = x, .f = f, y = y, z = z)
# Forma 2: Passando uma função anônima de dois argumentos.
purrr::map(.x = x, .f = function(x, y, z) x * y + 2 * z , y = y, z = z)
# Forma 3: Utilizamos .x e .y em situações de funções com 2 argumentos.
purrr::map(.x = x, .f = ~ .x * .y + 2 * ..3, y = y, ..3 = z)
# Forma 4: Aqui o x .x será substituido na ocorrência de "." (ponto).
purrr::map(.x = x, .f = ~ . * .y + 2 * ..3, y = y, ..3 = z)
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Nas formas 3 e 4 do exercício acima, você poderá substituir `..3` por `z`, ou seja, considerar, por exemplo, `purrr::map(.x = x, .f = ~ .x * .y + 2 * ..3, y = y, z = z)` irá funcionar. Isso se deve ao fato do funcional `map()` ser uma função **vararg**, em que os argumentos adicionais (não pertencentes à `map()`) serão acrescentados na função passada ao argumento `.f` de `map()`.

**Se `f()` é uma função com `n` argumentos, você poderá referenciar os seus argumentos por `..1` (primeiro argumetno), `..2` (segundo argumento), `..3` (terceiro argumento), ..., `..n`, com `n` um número inteiro qualquer.**
</div></div>\EndKnitrBlock{rmdnote}

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
O uso de `.` para especificar o primeiro elemento de uma função passada como argumento à `.f` em um dos funcionais do pacote **purrr** poderá gerar conflitos em situações em que você esteja utilizando o pacote **magrittr** em que `.` tem um outro significado.
</div></div>\EndKnitrBlock{rmdobservation}

#### map2() e variantes

O funcional `map2()` tem grande utilidade em situações em que desejamos percorrer simultaneamente dois argumentos, isto é, quando temos que a função passada como argumento à `.f` possui dois argumentos e desejamos aplicar a função, par a par, sobre os elementos passados aos argumentos `.x` e `.y`, respectivamente. Em outras palavras, o uso do funcional `map2()` é útil em situações em que temos interesse de não deixar fixo o segundo argumento da função passada à `.f`. Assim como nas variantes do funcional `map()`, temos que as variantes do funcional `map2()` (`map2_int()`, `map2_dbl()` `map2_lgl()` e `map2_chr()`) ireão retornar um vetor com elementos do tipo referente ao sufixo utilizado.


**Forma geral de uso**:



```r
map2(.x, .y, .f, ...)
map2_int(.x, .y, .f, ...)
map2_dbl(.x, .y, .f, ...)
map2_lgl(.x, .y, .f, ...)
map2_chr(.x, .y, .f, ...)
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
O uso do funcional `map2()` é análago ao uso de `map()` e suas variantes, com a diferença que o segundo argumento não estará fixo.
</div></div>\EndKnitrBlock{rmdnote}

**Exemplo**: Uso da função `map2()` em que estão sendo somados, par a par, os elementos dos objetos `x` e `y`.


```r
x <- list(1:3, 1:2, 3:10)
y <- list(1:3, c(4,3), 5:12)
purrr::map2(.x = x, .y = y, .f = ~ .x + .y)
```

```
## [[1]]
## [1] 2 4 6
## 
## [[2]]
## [1] 5 5
## 
## [[3]]
## [1]  8 10 12 14 16 18 20 22
```

#### pmap() e variantes

Algo muito parecido com o funcional `Map()` e `mapply()`do **R Base** é o que podemos fazer com o funcional `pmap()` do pacote **purrr**. Analogamente ao que temos com `Map()` e `mapply()`, ao utilizar o funcional `pmap()` poderemos variar mais de um argumeto.

**Forma geral de uso**:


```r
pmap(.l, .f, ...)
pmap_int(.l, .f, ...)
pmap_dbl(.l, .f, ...)
pmap_lgl(.l, .f, ...)
pmap_chr(.l, .f, ...)
```

**Exemplo**: Uso do funcional `pmap()` variando, par a par, sobre elementos de duas listas (`x` e `y`) e um vetor (`z`).


```r
x <- list(1:3, 1:2, 3:10)
y <- list(1:3, c(4,3), 5:12)
z <- c(1, 2, 3)
purrr::pmap(.l = list(x, y, z), .f = ~ .x + .y + ..3)
```

```
## [[1]]
## [1] 3 5 7
## 
## [[2]]
## [1] 7 7
## 
## [[3]]
## [1] 11 13 15 17 19 21 23 25
```

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
O funcional `pmap()` poderá ser utilizado, de forma análoga ao exemplo acima, em situações em que a função passada ao argumento `.f` possa ter mais de três variáveis não fixadas. Porém, perceba que ao utilizar o funcional `pmap()`, nada impedirá que você tenha algumas dessas variáveis fixadas, se isso for de interesse. Esse fato também é válido para os funcionais `Map()` e `mapply()` do **R Base** e para o funcional `map2()` do pacote **purrr**.
</div></div>\EndKnitrBlock{rmdimportant}

**Exemplo**: Uso do funcional `pmap()` variando em duas listas (`x`, `y`) e um vetor `z`. Perceba que a quantidade de elementos nos objetos `x`, `y` e `z` é a mesma, ou seja, os objetos `x` e `y` são duas listas com dois vetores, respectivamente e `z` é um vetor com dois elementos.


```r
f <- function(x, y, z) x + y - z

x <- list(c(2,1,4), c(4,3,6,7,1))
y <- list(1:3, 1:5)
z <- c(1,1) # Vetor fixo.

purrr::pmap(.l = list(x, y, z), .f = f)
```

```
## [[1]]
## [1] 2 2 6
## 
## [[2]]
## [1]  4  4  8 10  5
```

#### invoke() e invoke_map()

A funcional `invoke()` é bastante semelhante ao funcional `do.call()` do **R Base**. Ambos os funcionais são úteis quando temos os argumentos de uma função em uma lista e posteriormente desejamos invocar uma função passando a lista de argumentos.

**Exemplo**: Passando a lista `runif_args` para a função `runif()` usando os funcionais do.call() (do **R Base**) e invoke (pacote **purrr**).


```r
set.seed(0) # Fixando uma semente.
# Lista de argumentos para passar à função runif().
runif_args <- list(n = 3, min = 0, max = 10)
# Usando do.call() do R Base.
do.call(what = runif, args = runif_args)
```

```
## [1] 8.966972 2.655087 3.721239
```

```r
# Usando invoke() do pacote purrr.
purrr::invoke(.f = runif, .x = runif_args)
```

```
## [1] 5.728534 9.082078 2.016819
```

Nas situações em que desejamos aplicar uma função à uma **lista de listas** de argumentos ou aplicar uma lista de argumentos à uma lista de funções, o funcional `invoke_map()` poderá ser de grande utilidade. O exemplo que segue mostra essas duas situações mencionadas.

**Exemplo**: 


```r
f1 <- function(valor, por) valor + por
f2 <- function(valor, por) valor - por
f3 <- function(valor, por) valor * por
f4 <- function(valor, por) valor / por

# Passando uma lista de listas de argumentos para a função f1.
purrr::invoke_map(.f = f1, .x = list(list(valor = 1, por = 1),
                                     list(valor = 2, por = 2), 
                                     list(valor = 7.1, por = 10)))
```

```
## [[1]]
## [1] 2
## 
## [[2]]
## [1] 4
## 
## [[3]]
## [1] 17.1
```

```r
# Passando uma lista de funções para a lista de argumentos passada 
# à .x do funcional invoke_map().
purrr::invoke_map(.f = list(f1, f2, f3, f4), .x = list(list(valor = 2, por = 2)))
```

```
## [[1]]
## [1] 4
## 
## [[2]]
## [1] 0
## 
## [[3]]
## [1] 4
## 
## [[4]]
## [1] 1
```


### Exercícios {-}

1. Considerando o data frame **iris** (150 observações e 5 variáveis), obtenha a média das variáveis quantitativas por meio do uso de um funcional.

2. O que o código abaixo faz? Reescreva o código abaixo, substitundo o loop `for()` pelo uso de um funcional. **Dica**: Utilize a função `sapply()`.

    
    ```r
    vetor <- 1L:10L
    f <- function(x){
       v <- c()
       for(i in seq_along(x)){
          v[i] <- x[i] + x[i + 1] 
       }
    
       # A função na.omit() remove ocorrências de NA 
       # no vetor passado como argumento.
       v <- na.omit(v) 
       attributes(v) <- NULL; v
    }
    ```

<!-- mydiff <- function(i, x){ -->
<!--    x[i] + x[i+1] -->
<!-- } -->

<!-- loop <- function() sapply(X = 1L:9L, FUN = mydiff, x = vetor) -->

3. Refaça o exercício anterior utilizando a função `vapply()`.

<!-- vetor <- 1L:10L -->
<!-- mysum <- function(i, x)  x[i] + x[i+1] -->
<!-- result <- vapply(X = 1:length(vetor), FUN = mysum, FUN.VALUE = double(1), x = vetor) %>%  -->
<!--                  na.omit  -->
<!-- attributes(result) <- NULL -->

4. Leia a descrição do funcional `accumulate()` do pacote **purrr** e entenda o código abaixo:

    
    ```r
      x <- list(c(3, 2, 4), c(5, 3), c(4, 2, 3))
      purrr::accumulate(.x = x, .f = ~ sum(.x) + .y)
    ```

5. Reescreva o código abaixo utilizando o funcional `accumulate()` do pacote **purrr**.

    
    ```r
    acumular <- function(x){
       vetor <- x[1]
       for(i in 2:length(x)){
          vetor[i] <- sum(vetor[i - 1]) + x[i]
       }
       vetor
    }
    ```
<!-- purrr::accumulate(.x = c(1, 2, 3), .f = ~ .x + .y) -->

6. Implemente a função `isnumeric(x)` que deverá recebe um data frame e retornar um vetor lógico informando `TRUE`, se a coluna é numerica ou `FALSE`, caso contrário. Implemente de três formas, tal que:

   * **Forma 1**: Implementar utilizando a estrutura de repetição `for()`;
   
   * **Forma 2**: Implementar utilizando o funcional `sapply()`;
   
   * **Forma 3**: Implementar utilizando o functional `vapply()`.

7. A função `unique()` quando aplicada à um vetor, retornará um outro vetor com os elementos não repetidos do vetor passado como argumento à `unique()`. Implemente a função `countdiff(x)` que recebe como argumento um vetor, matriz ou tabela (data frame), de forma que retorne a quantidade de elementos distintos no vetor ou nas colunas da matriz/tabala.

8. Considere o objeto `lista <- list(1:2, list(c(8, 7), c(1, 4)))`. Utilizando o funcional `map()`, obtenha a saída abaixo. **Dica**: 1 - Use `map()` dentro de `map()`. 2 - Ao final, utilize o comando `flatten()` do pacote **purrr**. A saída a baixo é nada mais que somar 1 em cada elemento da lista.

    
    ```r
      [[1]]
      [1] 2
    
      [[2]]
      [1] 3
    
      [[3]]
      [1] 9 8
    
      [[4]]
      [1] 2 5
    ```

<!-- lista <- list(1:2, list(c(8, 7), c(1, 4))) -->
<!-- map(.x = lista, ~ map(., .f = ~ .x + 1)) %>%  flatten -->

9. Por meio da documentação do funcional `map_if()` do pacote **purrr**, entenda o que o código abaixo faz:

    
    ```r
       x <- 1:10
       purrr::map_if(.x = x, .p = ~ .x %% 2 == 0, 
                     .f = ~ 2 * .x, .else = ~ .x + 1) %>% flatten_dbl()
    ```

10. Considere o objeto `lista` definido por `lista <- list(a = c(1, 3, 2), b = c(2, 3))`. Utilizando o funcional `map_if()`, multiplique os elementos pares por 2 de forma a obter a saída abaixo:

    
    ```r
    $a
    $a[[1]]
    [1] 1
    
    $a[[2]]
    [1] 3
    
    $a[[3]]
    [1] 4
    
    $b
    $b[[1]]
    [1] 4
    
    $b[[2]]
    [1] 3
    ```
   **Dica**: Tente construir algo como `map(.x = lista, .f = ~ map_if())`.

<!-- purrr::map(.x = lista, .f = ~ map_if(.x, .p = ~ .x %% 2 == 0 , .f = ~ .x * 2)) -->

11. A função `split()` divide um data frame em grupos de um fator. Por exemplo, faça `iris %$% split(., Species)`. Dado isso, considere o conjunto de dados **starwars** do pacote [**dplyr**](https://dplyr.tidyverse.org/) (`install.packages("dplyr")`) que possui várias descrições dos personagens de Star Wars. Obtenha a quantidade de personagens por espécies utilizando o funcional `map()`.

<!-- purrr::map(.x = split(starwars, starwars$species), .f = ~dim(.x)[1]) -->


## Sistema S3

S3 é o primeiro e mais simples sistema de [**Orientação à Objeto (OO)**](https://pt.wikipedia.org/wiki/Orienta%C3%A7%C3%A3o_a_objetos) da linguagem R. Por ser o primeiro sistema de OO da linguagem R, S3 é o sistema mais utilizado nos pacotes disponíveis no [**Comprehensive R Archive Network - CRAN**](https://cran.r-project.org/), além de ser o sistema de OO utilizado na implementação dos pacotes **base** (**R Base**) e no pacote **stats**, ambos pacotes disponíveis por padrão em qualquer instalação de R. Aliás, o **base** é o principal pacote de R, sendo este o pacote de define a linguagem R com suas funções básicas. A linguagem R permite o uso de outros sistemas de OO como o S4, RC e R6, sendo o sistema R6 disponível pelo pacote [**R6**](https://r6.r-lib.org/) o mais formal e disponível em forma de um pacote desenvolvido por [**Winston Chang**](https://github.com/wch). 

O S3 implementa um estilo de OO chamado OO de função genérica. Esse sistema é diferente da maioria das linguagens de programação com paradigma de OO, como, por exemplo, Java, C++, Ruby, Python e C#, que implementam o sistema de OO por transmissão de mensagens. Com a passagem de mensagens para um objeto, este determina qual método (função) irá chamar. Nessas linguagens, invocamos um método para um objeto fazendo algo como `objeto.metodo()`, em que `objeto` é um objeto qualquer pertencente à uma classe e `metodo()` é uma função qualquer disponível à objetos dessa classe. Por exemplo, você poderia ter algo como `M.inverse()` que calcularia a inversa do objeto `M` da classe `matrix`. Dessa forma, se o objeto `M` é assinado com uma classe, os métodos (funções) disponíveis para esse objeto estão encapsulados no interior do objeto. OO, em R, de forma mais próxima aos sistemas de linguagens OO tracionais é possível com o sistema R6 do pacote [**R6**](https://r6.r-lib.org/). Esse sistema é utilizado no pacote [**ggplot2**](https://github.com/tidyverse/ggplot2).

Ao contrário dos sistemas tradicionais de OO, no sistema de OO S3, os métodos não estão dentro (encapsulados) dos objetos. Esses são invocados por uma função genérica que é responsável por invocar o método correto. Considere o exemplo abaixo:

**Exemplo**: 


```r
vetor <- c(7, 1, 2, 3, 1.2, 4.4)
modelo <- lm(data = mtcars, formula = mpg ~ cyl + disp + wt)
# Calculando o sumário de um vetor.
summary(vetor)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    1.00    1.40    2.50    3.10    4.05    7.00
```

```r
# Obtendo o sumário de um modelo de regressão.
summary(modelo)
```

```
## 
## Call:
## lm(formula = mpg ~ cyl + disp + wt, data = mtcars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -4.4020 -1.4067 -0.4948  1.3471  6.0717 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 41.072990   2.839375  14.466 1.61e-14 ***
## cyl         -1.778054   0.606451  -2.932  0.00664 ** 
## disp         0.007275   0.011797   0.617  0.54243    
## wt          -3.623447   1.037898  -3.491  0.00161 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.595 on 28 degrees of freedom
## Multiple R-squared:  0.8325,	Adjusted R-squared:  0.8146 
## F-statistic: 46.39 on 3 and 28 DF,  p-value: 5.446e-11
```

Perceba que a função `summary()` atuou de formas distintas sobre os objetos `vetor` e `modelo` que pertencem às classes **numeric** e **lm**, respectivamente. A função `summary()` invocou o método para realizar o trabalho correto sobre o objeto em questão. Trata-se de uma função genérica (uma interface) responsável por invocar o método correto. Essa função estará associada à diversas outras funções. É a função genérica que irá despachar o método (função) correta para trabalhar com objeto em questão. Note que a função `summary()` (função genérica) é uma implementação muito simples. Veja o seu conteúdo abaixo:


```r
body(fun = summary)
```

```
## UseMethod("summary")
```

Para o exemplo acima, a função genérica `summary()` invocou os métodos `default()` e `lm` para trabalharem sobre os objetos `vetor` e `modelo`, respectivamente. Por exemplo, você poderia ter feito o papel da função genérica `summary()`, fazendo:


```r
vetor <- c(7, 1, 2, 3, 1.2, 4.4)
modelo <- lm(data = mtcars, formula = mpg ~ cyl + disp + wt)
# Calculando o sumário de um vetor.
summary.default(vetor)
# Obtendo o sumário de um modelo de regressão.
summary.lm(modelo)
```

Além dos métodos `default()` e `lm()` associados à função genérica `summary()`, diversos outros métodos podem ser despachado por `summary()`. Faça em um prompt de comando da linguagem R, por exemplo, `summary` + **Tab** para obter uma lista dos métodos disponíveis para a função genérica `summary()`. Uma outra forma mais eficiente de fazer isso é utilizando a função `methods()`, como mostra o código abaixo:


```r
# Listando todos os métodos associados 
# à função genérica summary().
methods(generic.function = summary) # or methods(generic.function = "summary")
```

```
##  [1] summary.aov                    summary.aovlist*              
##  [3] summary.aspell*                summary.check_packages_in_dir*
##  [5] summary.cohesiveBlocks*        summary.connection            
##  [7] summary.data.frame             summary.Date                  
##  [9] summary.default                summary.ecdf*                 
## [11] summary.factor                 summary.gexf*                 
## [13] summary.ggplot*                summary.glm                   
## [15] summary.hcl_palettes*          summary.igraph*               
## [17] summary.infl*                  summary.lm                    
## [19] summary.loess*                 summary.manova                
## [21] summary.matrix                 summary.mlm*                  
## [23] summary.nls*                   summary.packageStatus*        
## [25] summary.POSIXct                summary.POSIXlt               
## [27] summary.ppr*                   summary.prcomp*               
## [29] summary.princomp*              summary.proc_time             
## [31] summary.rlang_error*           summary.rlang_trace*          
## [33] summary.srcfile                summary.srcref                
## [35] summary.stepfun                summary.stl*                  
## [37] summary.table                  summary.tukeysmooth*          
## [39] summary.warnings               summary.XMLInternalDocument*  
## see '?methods' for accessing help and source code
```

Para saber se uma determinada função é genérica e em caso afirmavo saber qual método foi despachado, o uso do pacote [**sloop**](https://github.com/r-lib/sloop) poderá ser útil. O pacote encontra-se no CRAN e poderá ser instalado fazendo `install.packages("devtools")`. Considere o exemplo que segue:

**Exemplo**:


```r
x <- matrix(1L:4L, nrow = 2)

# Indica que print() é um objeto do sistema S3
# de OO e além disso, informa que trata-se de
# uma função genérica.
sloop::ftype(f = print)
```

```
## [1] "S3"      "generic"
```

```r
# A seta indica qual método está sendo utilizado para 
# imprimir o objeto x. Nesse caso, print(x) despacha
# o método default() associado à função genérica print().
sloop::s3_dispatch(print(x))
```

```
##    print.matrix
##    print.integer
##    print.numeric
## => print.default
```

### Classes

No sistema S3 não há uma definição formal de classe. Para definir um objeto como pertencente à uma determinada classe, bastará definir um atributo de classe ao objeto utilizando as funções `structure()` ou `class<-`(). O exempo que deixará claro como isso poderá ser feito:

**Exemplo**:


```r
# Fazendo list() tpertencer à uma classe qualquer
# de nome "any_class".
x <- structure(list(), class = "any_class")
class(x)
```

```
## [1] "any_class"
```

```r
# ou
x <- list()
class(x) <- "any_class"
class(x)
```

```
## [1] "any_class"
```

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Perceba que a classe de um objeto não é nada mais que um atributo do objeto, em que esse atributo tem o nome **class**. Faça, por exemplo `attributes(x)` para obter uma lista de atributos associados à um objeto. Você poderá incluir qualquer outro atributo ao objeto `x`, se for de seu interesse, porém, deverá existir apenas um atributo de nome **class** que controla a classe do objeto.
</div></div>\EndKnitrBlock{rmdimportant}

**Exemplo**: Você poderá determinar qual a classe de um objeto fazendo e perguntar se um objeto pertence à uma instância de classe, como mostra o código que segue:


```r
x <- list()
class(x) <- "any_class"
# Perguntando a classe do objeto x.
class(x)
```

```
## [1] "any_class"
```

```r
# Perguntando e o objeto x pertência à instância de 
# classe de nome any_class.
inherits(x, what = "any_class")
```

```
## [1] TRUE
```

### Criando funções genéricas

O trabalho de um S3 genérico é executar o envio do método, ou seja, encontrar a implementação específica para uma classe. O envio do método é realizado por `UseMethod()`. 

**Exemplo**: Veja que `print()` e `summary()` são funções genéricas, cuja a implementação faz uso da função `UseMethod()`.


```r
sloop::ftype(summary)
```

```
## [1] "S3"      "generic"
```

```r
sloop::ftype(print)
```

```
## [1] "S3"      "generic"
```

```r
# Corpo da função genérica summary().
body(summary)
```

```
## UseMethod("summary")
```

```r
# Corpo da função genérica print().
body(print)
```

```
## UseMethod("print")
```

A função `UseMethod()` usa dois argumentos: o nome da função genérica (obrigatório) e o argumento a ser usado para o método de envio (opcional). Se você omitir o segundo argumento, ele será despachado com base no primeiro argumento, que é quase sempre o que é desejado. 


**Exemplo**: Criando a função genérica `f()`. O método `default()` é um método auxiliar que será utilizado caso a classe o argumento passado à função `f()` pertença à uma classe que não há um método associado á função genérica `f()`. Perceba que `f(x)` fará uso do método `myclass()` e `f(y)` fará uso do método `default()`, uma vez que `y` não foi assinado com um objeto pertencente à classe **myclass**.


```r
f <- function(x) UseMethod("f")
# Função que trabalha com objeto da classe myclass.
f.myclass <- function(x) {
   warning("Foi executado o método myclass: mesmo que f.myclass(x)")
   print(x + 1)
}
f.default <- function(x){
   warning("Foi executado o método default: mesmo que f.default(x)")
   print(x)
} 
x <- y <- 1L:10L
class(x) <- "myclass"
f(x)
```

```
## Warning in f.myclass(x): Foi executado o método myclass: mesmo que
## f.myclass(x)
```

```
##  [1]  2  3  4  5  6  7  8  9 10 11
## attr(,"class")
## [1] "myclass"
```

```r
# Será executado o método default, uma vez que o objeto
# y não foi assinado com a classe myclass.
f(y)
```

```
## Warning in f.default(y): Foi executado o método default: mesmo que
## f.default(x)
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
# Checando se f é um objeto da classe S3 e se trata-se 
# de uma função genérica.
sloop::ftype(f)
```

```
## [1] "S3"      "generic"
```

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Perceba que utiliza `.` no nome de uma função não ocasionará problemas de conflito, mas poderá nos deixar com dúvidas, uma vez que não sabemos se o que está antes do ponto é uma função genérica e logo após o seu método ou se apenas trata-se de uma função que usa `.` no seu nome. Por exemplo, se olharmos apenas para `f.a()` não ficará claro se `f()` é uma função genérica e `a()` um método de `f()` ou se temos uma função comum de nome `f.a`. 
</div></div>\EndKnitrBlock{rmdobservation}

### Exercício {-}

1 - A função função `dim()` é uma função genérica? Explique. Em caso afirmativo, quantos métodos possui essa função?

2 - Explique o por quê da saída do código que segue:


```r
x <- 1L:10L
class(x) <- "test"
t(x)
```

```
## 
## 	One Sample t-test
## 
## data:  x
## t = 5.7446, df = 9, p-value = 0.0002782
## alternative hypothesis: true mean is not equal to 0
## 95 percent confidence interval:
##  3.334149 7.665851
## sample estimates:
## mean of x 
##       5.5
```
    
3 - Crie o método `print.conc(x, y, sep = "", ...)` para a função genérica `print()`. O método deverá concatenar dois objetos da classe **conc**. O método deverá funcionar da forma abaixo:


```r
str1 <- "Estudando" 
class(str1) <- "conc"
str2 <- "R"
print(x = str1, y = str2, sep = " ")
```

```
## [1] "Estudando"
## attr(,"class")
## [1] "conc"
```

```r
# [1] "Estudando R"
```

<!-- print.paste <- function(x, y, sep = "", ...){ -->
<!--   if (is.character(x) == FALSE || is.character(x) == FALSE) -->
<!--     stop("Os argumentos devem ser strings.") -->
<!--   paste(x, y, sep = sep, ...) -->
<!-- } -->
<!-- str1 <- "Pedro" -->
<!-- class(str1) <- "paste" -->
<!-- str2 <- "Rafael" -->
<!-- print(x = str1, y = str2)     -->

4 - Informe a saída do código abaixo. Explique!


```r
y <- 1
f <- function(x) {
   y <- 2
   UseMethod("f")
}
f.numeric <- function(x) y
f(10); f.numeric(7)
```

5 - Informe a saída do código abaixo. Explique!


```r
g <- function(x) UseMethod("g")

g.character <- function(x) paste("char", x)
g.numeric <- function(x) paste("num", x)
g.default <- function(x) "?"

g("1")
g(1)
g(TRUE)
```

6 - A função abaixo implementa o método `summary.character()`. O que esse método faz? Por que não foi preciso assinar o objeto `x`? Entenda o código:


```r
summary.character <- function(x){
  if (!inherits(x, what = "character")) stop("x must be of character type")  
  n_char <- nchar(x)
  vetor_chr <- strsplit(x = x, split = "")
  if (is.list(vetor_chr) == TRUE){
    list_factor <- purrr::map(.x = vetor_chr, .f = ~ as.factor(.x))
    n_diff <- purrr::map(.x = list_factor, .f = ~ length(levels(.x)))
  } else 
    n_diff <- length(levels(as.factor(vetor_chr)))
  
  list(nchr = n_char, ndiff = n_diff)
}
summary(x = c("aabb", "aaa"))
```

```
## $nchr
## [1] 4 3
## 
## $ndiff
## $ndiff[[1]]
## [1] 2
## 
## $ndiff[[2]]
## [1] 1
```

7 - Construa a função genérica `mydiag(x)` que recebe como argumento uma matriz ou tabela (data frame) que podem conter valores numéricos ou caracters, com o número de linhas é igual ao número de colunas. Depois, defina dois métodos, `mydiag.numeric()` e `mydiag.character()` que retorna a soma da diagonal principal do objeto passado à `x`. Para a matriz/tabela de caracteres, considere A/a como 1, B/b como 2, ..., Z/z como 26, respectivamente. **Dicas**: 1 - As função `tolower()` poderá ajudar a converter um caracter em letra maiúscila para minúscula. 2 - Para o caso de matriz/tabela com strings, considere apenas o primeiro caracter da string. Por exemplo:


```r
m1 <- matrix(1:4, 2, 2)
mydiag(m1)
# [1] 5
m2 <- matrix(c("casa", "a", "barco", "terra"), 2, 2)
mydiag(m2)
# [1] 23
```



    
