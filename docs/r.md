# R - miscelânea e tópicos avançados

Nesse ponto será assumido que você realizou os passos de [**revisão**][Sugestões de passos para revisão da linguagem R] da linguagem R sugeridos, bem como resolveu os [**exercícios propostos**][Exercícios propostos]. Considerá-los é de grande importância para que você consiga assimilar os conceitos apresentados nesse [**Capítulo**][R - miscelânea e tópicos avançados].

Esse [**Capítulo**][R - miscelânea e tópicos avançados] visa apresentar algumas miscelâneas a respeito da linguagem de programação R, bem como, alguns tópicos mais avançados de programação em R. O termo "**avançado**" utilizado aqui não necessariamente tem correlação com dificuldade de entendimento. Aqui utilizo esse termo para abordar assuntos que normalmente eram pouco discutidos em livros mais antigos da linguagem R e que atualmente vem ganhando destaques em livros e discussões mais recentes na internet. Na verdade, a maioria dos conceitos que serão abordados são de fácil compreensão, porẽm ajudarão os programadores em R a construir códigos mais robustos e mais flexíveis. Alguns desses assuntos que serão abordados e divididos em subseções são:

  1. Pipe %>%
  
  2. Funções: 
    
     - Funcionais
    
     - Closures
    
     - dot-dot-dot, ..1 e etc
     
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
<img src="images/logo_magrittr.png" alt="Logo do pacote [**magrittr**](https://github.com/tidyverse/magrittr) com frase ***Ceci n'est pas une pipe*** ([**ouça a pronuncia**](https://upload.wikimedia.org/wikipedia/commons/1/1f/Fr-Ceci-n-est-pas-une-pipe.ogg)), mesmo frase que acompanha pintura ***La trahison des images*** de [**René Magritte**](https://pt.wikipedia.org/wiki/Ren%C3%A9_Magritte)." width="25%" />
<p class="caption">(\#fig:unnamed-chunk-2)Logo do pacote [**magrittr**](https://github.com/tidyverse/magrittr) com frase ***Ceci n'est pas une pipe*** ([**ouça a pronuncia**](https://upload.wikimedia.org/wikipedia/commons/1/1f/Fr-Ceci-n-est-pas-une-pipe.ogg)), mesmo frase que acompanha pintura ***La trahison des images*** de [**René Magritte**](https://pt.wikipedia.org/wiki/Ren%C3%A9_Magritte).</p>
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

**Exercício**: Resolva os itens abaixo utilizando o operador `%>%` do pacote matrittr. 

  - `as.character(log(cos(sin(pi))))`

  - `round(var(seq(from = 1, to = 10, by = 0.5)), digits = 1)`
  
  - `summary(anova(lm(mpg ~ wt, data = mtcars)))`
  
  - `summary(lm(dist ~ log(accel), data = na.omit(attenu)))`
  
Nem sempre desejamos introduzir o que está a esquerda do operador `%>%` como primeiro agumento daquilo que está à sua direita. Para isso, poderemos fazer uso do caracter `.` (ponto). Esse caracter irá designar em qual posição será introduzido o objeto à esquerda de `%>%` na função à sua direita. Por exemplo, a expressão `x %>% f(a, b = .)` fará com que `x` à esqueda de `%>%` seja substituído no lugar do caracter `.`, ou seja, `x` é passado como argumento à `b`, segundo argumento de `f`.

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


Um outro operador útil disponível no pacote magrittr é o operator ***tee***, denotado por `%T>%`. Esse operador funciona de forma muito parecida com o operador `%>%`, exceto pelo fato de que ele irá retornar o conteúdo do lado esquedo e **não** o resultado da operação do seu lado diretio. 

O uso do operador `%T>%` não é tão comum. Normalmente a frequência de uso do operador `%>%` é muito maior. Porém, veja que não é possível resolver o exemplo que segue utilizando apenas o operador `%>%`.

**Exemplo**: Pelo que entendemos do operador `%>%`, não faz nenhum sentido o código abaixo:


```r
# Fixando uma semente.
set.seed(0) 
rnorm(1000L) %>% hist(., main = "Histograma Qualquer", xlab = "x",
                      ylab = "Frequência") %>% mean 
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
                       ylab = "Frequência") %>% mean 
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
Normalmente esse operador é útil quando a função a direita não possui argumento de dados. Por exmeplo, se o objetivo fosse calcular uma regressão linear simples com essas variáveis, poderíamos fazer:
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
```



