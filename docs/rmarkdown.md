# Relatório Markdown em R

Uma das tarefas mais importantes e frequentes na vida de um estatístico refere-se à construção de documentos (relatórios, manuais, etc). A construção desses documentos é algo que demanda tempo, uma vez que, por exemplo, temos que escrever a respeito das metodologias estatísticas consideradas e justificar o seu uso, organizar as informações obtidas de um modelo estatístico e interpretá-las, tabular os resultados de algumas simulação, escolher o formato de saída do documento e escrever de forma clara e robusta os resultados obtidos (muitos que irão ler seu documento não são estatísticos). Um pouco dessa rotina encontra-se no diagrama a baixo:

<div class="figure" style="text-align: center">
<!--html_preserve--><div id="htmlwidget-1dd8e509afcef60f585a" style="width:700px;height:600px;" class="DiagrammeR html-widget"></div>
<script type="application/json" data-for="htmlwidget-1dd8e509afcef60f585a">{"x":{"diagram":"\ngraph TD\n\nA((fa:fa-database DADOS))-->B((R))\nB-->C(ORGANIZAÇÃO DOS DADOS)\nD(ESCOLHA DAS METODOLOGIAS)\nC-->|Implementar|E((R))\nD-->|Implementar|E\nE-->F(ORGANIZAÇÃO DOS RESULTADOS)\nF-->|Frequente|G((Documento))\n\nstyle A fill:#ffe5cc\nstyle B fill:#ffe5cc\nstyle C fill:#ffe5cc\nstyle D fill:#ffe5cc\nstyle E fill:#ffe5cc\nstyle F fill:#ffe5cc\nstyle G fill:#ffe5cc\n"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
<p class="caption">(\#fig:diagramafluxo)Fluxo de trabalho - organização dos dados, escolhas das metodologias, implementações e edição de documento.</p>
</div>
 
Como descrito no diagrama \@ref(fig:diagramafluxo), o processo de construção de um relatório é um processo frequente, uma vez que você muito provavelmente, em alguma empresa, irá deparar-se com documentos em que deverão ser atualizados, dia após dia. Por exemplo, você poderá vir a trabalhar em uma empresa em que diariamente terá que enviar relatório(s) ao seu chefe ou para um grupo de pessoas. Por exemplo, em muitas situações, esse(s) documentos(s) poderão possuir um layout predefinido, onde serão apenas alterados os resultados/retornos obtidos por suas funções implementadas em [**R**](https://www.r-project.org). Ou seja, estamos considerando o caso em que você diariamente tem o mesmo relatório com diferentes estatísticas (indicadores descritivos, resultados inferenciais, etc). Com o [**R**](https://www.r-project.org) e o [**Markdown**](https://daringfireball.net/projects/markdown/), bem como utlizando outras ferramentas disponíveis para programadores de [**R**](https://www.r-project.org), você poderá automatizar, ao máximo, o processo de construção documentos. 

Por tratar-se de uma comunidade grande e que envolve muitos estatísticos, a comunidade de [**R**](https://www.r-project.org) vem constantemente desenvolvendo ferramentas de interesse para quem trabalha com estatística e aprendizado estatístico. Muitas dessas ferramentas são disponibilizadas na forma de pacotes, no [**CRAN**](https://cran.r-project.org/web/packages/index.html) (**The Comprehensive R Archive Network**), bem como no [**GitHub**](https://github.com/). Isso mostra a grande flexivilidade de [**R**](https://www.r-project.org) e o quanto essa linguagem se adapta às necessidades de um estatístico ou à quem for de interesse a análise de dados. Você poderá programar em qualquer linguagem, porém, programar em [**R**](https://www.r-project.org) tornará sua vida de progamador/estatístico mais fácil, caso o seu seu interesse esteja em resolver problemas estatísticos e/ou que envolvam aprendizado estatístico, denominado por muitos de [**machine learning** (**aprendizado de máquina**)](https://pt.wikipedia.org/wiki/Aprendizado_de_m%C3%A1quina).

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Nada impedirá que você venha trabalhar com problemas não estatísticos em [**R**](https://www.r-project.org). [**R**](https://www.r-project.org) é uma linguagem elegante, flexível e que permite se comunicar com diversas outras linguagens de programação.
</div></div>\EndKnitrBlock{rmdobservation}

Como mostra o diagrama \@ref(fig:diagramafluxo), a linguagem [**R**](https://www.r-project.org) está no meio de importantes etapas de um estudo. O estatístico poderá utilizar o [**R**](https://www.r-project.org) para organizar os dados, implementar as metodologias estatísticas adotadas no estudo e se quiser, poderá utilizar o [**R**](https://www.r-project.org) para construir o relatório. 


Note que no diagrama \@ref(fig:diagramafluxo), descrevemos a linguagem [**R**](https://www.r-project.org) como uma ferramenta que está presente entre quase todos os passos na construção dos resultados de um estudo. Integrando o [**Markdown**](https://daringfireball.net/projects/markdown/) com a linguagem [**R**](https://www.r-project.org), você fará com que o [**R**](https://www.r-project.org) esteja presente entre todos os processos do estudo, o que certamente trará grande flexibilidade (possibilidades) às suas análises. Assim, seu fluxo de trabalho passará de \@ref(fig:diagramafluxo) para \@ref(fig:diagramafluxor) otimizando assim, as suas análises.

<div class="figure" style="text-align: center">
<!--html_preserve--><div id="htmlwidget-58f0fb952f20bbf92cf3" style="width:780px;height:670px;" class="DiagrammeR html-widget"></div>
<script type="application/json" data-for="htmlwidget-58f0fb952f20bbf92cf3">{"x":{"diagram":"\ngraph TD\n\nA((fa:fa-database DADOS))-->B((R))\nB-->C(ORGANIZAÇÃO DOS DADOS)\nD(ESCOLHA DAS METODOLOGIAS)\nC-->|Implementar|E((R))\nD-->|Implementar|E\nE-->F(ORGANIZAÇÃO DOS RESULTADOS)\nF-->G((R))\nG-->|R com Markdown|H((Documento))\n\nstyle A fill:#ffe5cc\nstyle B fill:#ffe5cc\nstyle C fill:#ffe5cc\nstyle D fill:#ffe5cc\nstyle E fill:#ffe5cc\nstyle F fill:#ffe5cc\nstyle G fill:#ff8900\nstyle H fill:#ffe5cc\n"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
<p class="caption">(\#fig:diagramafluxor)Linguagem [**R**](https://www.r-project.org) entre todos os fluxos de trabalho de um estudo estatístico. Destaque para o uso de [**R**](https://www.r-project.org) para a construção de um relatório.</p>
</div>

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Esse material que você está lendo agora mostra um pouco do que você consegue fazer com o [**R**](https://www.r-project.org) + [**Markdown**](https://daringfireball.net/projects/markdown/) utilizando algumas ferramentas (pacotes) disponíveis para o [**R**](https://www.r-project.org). As ferramentas que integram [**R**](https://www.r-project.org) com [**Markdown**](https://daringfireball.net/projects/markdown/) são bem integradas com a IDE de programação [**RStudio**](https://www.rstudio.com/), o que facilita um pouco o trabalho de edição.
</div></div>\EndKnitrBlock{rmdnote}

## Markdown

[**Markdown**](https://daringfireball.net/projects/markdown/) é uma linguagem de marcação desenvolvida em 2004 por [**John Gruber**](https://en.wikipedia.org/wiki/John_Gruber) com a colaboração de [**Aaron Swartz**](https://en.wikipedia.org/wiki/Aaron_Swartz). [**Markdown**](https://daringfireball.net/projects/markdown/) é uma linguagem muito leve e diponível sob os termos de uma licença de código aberto no estilo BSD.

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Algo curioso com relação a linguagem [**Markdown**](https://daringfireball.net/projects/markdown/) é que o seu lançamento inicial se deu em 19 de março de 2004 e o seu último lançamento (versão 1.0.1) foi em 17 de dezembro do mesmo ano. A versão 1.0.1 do [**Markdown**](https://daringfireball.net/projects/markdown/) possui apenas **18 KB**.
</div></div>\EndKnitrBlock{rmdnote}

</br>

<div class="figure" style="text-align: center">
<img src="images/logo_markdown.png" alt="Logo da linguagem de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) utilizada para conversão de texto em [**HTML**](https://pt.wikipedia.org/wiki/HTML)." width="40%" />
<p class="caption">(\#fig:logomarkdown)Logo da linguagem de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) utilizada para conversão de texto em [**HTML**](https://pt.wikipedia.org/wiki/HTML).</p>
</div>

</br>


**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Arquivos em [**Markdown**](https://daringfireball.net/projects/markdown/) devem possuir a extensão **.md**.
</div></div>\EndKnitrBlock{rmdimportant}

</br>

A linguagem [**Markdown**](https://daringfireball.net/projects/markdown/) faz com que a tarefa de construir páginas em [**HTML**](https://pt.wikipedia.org/wiki/HTML) seja algo bem mais fácil e prazeroso. Sinceramente, você não estaria lendo esse material se eu tivesse que escrever todo esse conteúdo diretamente em [**HTML**](https://pt.wikipedia.org/wiki/HTML). Para entender um pouco do que estou falando, logo abaixo você encontrará dois exemplos do mesmo texto escrito utilizando as linguagens de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) e [**HTML**](https://pt.wikipedia.org/wiki/HTML), respectivamente. Ambos nos levarão ao mesmo resultado de uma página em [**HTML**](https://pt.wikipedia.org/wiki/HTML). Note como é mais claro e limpo o código em [**Markdown**](https://daringfireball.net/projects/markdown/) em comparação ao código em [**HTML**](https://pt.wikipedia.org/wiki/HTML).

</br>

**Texto escrito utilizando Markdown**:

```markdown
# Seção

Escrevendo alguma coisa nessa minha seção.

## Subseção

Escrevendo alguma coisa nessa minha subseção.

Outra linha.

Colocando texto em itálico _texto em itálico_ ou *texto em itálico*, em negrito 
**texto em negrito** e destacando um código `f <- function() ...`.

Criando uma linha horizontal:

---

Listando itens:

  * R é Open Source
  * R é uma ótima linguagem de progrmação
  * Estatísticos em todo o mundo usam R
  * R é utilizado por grandes empresas para análise de dados e em aprendizagem de máquina.

---

Enumerando itens:

  1. R Agro
  2. R é Tec
  3. R é Pop
  4. R é Tudo

---

Um bom curso de estatística computacional utilizando R poderá ser encontrado em [**Estatística Computacional**](https://prdm0.github.io/aulas_computacional).

![Logo da linguagem de programação R.](https://www.r-project.org/logo/Rlogo.png "icon")

Lembre-se:

> Batatinha quando nasce, esparrama pelo chão. 
> Se você não aprender em R irá sofrer de montão.

> --- Autor desconhecido, 2019.

<strong>Se eu desejar, poderei utilizar código HTML</strong>.
```

**Texto escrito utilizando HTML**:

```html
<h1>Seção</h1>

<p>Escrevendo alguma coisa nessa minha seção.</p>

<h2>Subseção</h2>

<p>Escrevendo alguma coisa nessa minha subseção.</p>

<p>Outra linha.</p>

<p>Colocando texto em itálico <em>texto em itálico</em> ou <em>texto em itálico</em>, em negrito 
<strong>texto em negrito</strong> e destacando um código <code>f &lt;- function() ...</code>.</p>

<p>Criando uma linha horizontal:</p>

<hr />

<p>Listando itens:</p>

<ul>
<li>R é Open Source</li>
<li>R é uma ótima linguagem de progrmação</li>
<li>Estatísticos em todo o mundo usam R</li>
<li>R é utilizado por grandes empresas para análise de dados e em aprendizagem de máquina.</li>
</ul>

<hr />

<p>Enumerando itens:</p>

<ol>
<li>R Agro</li>
<li>R é Tec</li>
<li>R é Pop</li>
<li>R é Tudo</li>
</ol>

<hr />

<p>Um bom curso de estatística computacional utilizando R poderá ser encontrado em <a href="https://prdm0.github.io/aulas_computacional"><strong>Estatística Computacional</strong></a>.</p>

<p><img src="https://www.r-project.org/logo/Rlogo.png" alt="Logo da linguagem de programação R." title="icon" /></p>

<p>Lembre-se:</p>

<blockquote>
  <p>Batatinha quando nasce, esparrama pelo chão. 
Se você não aprender em R irá sofrer de montão.</p>

<p>--- Autor desconhecido, 2019.</p>
</blockquote>

<p><strong>Se eu desejar, poderei utilizar código HTML</strong>.</p>
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Os códigos apresentados acima, utilizando as linguagens de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) e [**HTML**](https://pt.wikipedia.org/wiki/HTML), irão nos levar aos mesmos resultados. Para observar o resultado, clique [**aqui**](files/example_html.html).

É claro que o [**HTML**](https://pt.wikipedia.org/wiki/HTML) produzido ainda é bem simples e "rústico", lembrando um pouco das páginas do início da popularização da internet. Mas calma, utilizando as ferramentas corretas e que estão disponíveis em [**R**](https://www.r-project.org), poderemos produzir texto como esse que você está lendo agora.

A boa notícia é que você não precisará alterar em nada o código escrito em [**Markdown**](https://daringfireball.net/projects/markdown/) para obtenção de uma saída mais agradável. Você apenas precisará associá-lo à ferramenta correta dispiníveis em [**R**](https://www.r-project.org). 
</div></div>\EndKnitrBlock{rmdnote}

Antes de conversarmos a respeito das ferramentas disponíveis, em [**R**](https://www.r-project.org), para a construção de saídas em HTML mais atraentes, precisaremos entender melhor a sintaxe do [**Markdown**](https://daringfireball.net/projects/markdown/). A seção que segue é dedicada ao entendimento da sintaxe do [**Markdown**](https://daringfireball.net/projects/markdown/).

### Sintaxe

Entender a sintaxe de Markdown é algo interessante por alguns motivos. Elencarei três deles abaixo:

1. A sintaxe de [**Markdown**](https://daringfireball.net/projects/markdown/) é fácil e não requer uma grande curva de aprendizado;
  
2. Seus documentos podem ser facilmente compartilhados dentro de uma empresa ou grupo de pessoas. Seu relatório em HTML poderá estar hospedado utilizando algum serviço e as pessoas poderão acessar o conteúdo clicando em um link. Por exemplo, não haverá a necessidade de compartilhar arquivos por e-mail ou em dispositivos de armazenamento. Você não precisará levar esse arquivo com você, caso tenha acesso à internet;
  
3. [**Markdown**](https://daringfireball.net/projects/markdown/) poderá ser utilizado em vários lugares, e não apenas em conjunto com o [**R**](https://www.r-project.org). Por exemplo, você poderá utilizar o [**Markdown**](https://daringfireball.net/projects/markdown/) no GitHub ou no [**Stack Overflow**](https://stackoverflow.com), site este de perguntas e respostas que é muito útil no aprendizado de programação. Por sinal, aconselho que você crie uma conta e venha utilizado o [**Stack Overflow**](https://stackoverflow.com) para fazer peguntas de programação em [**R**](https://www.r-project.org). Há uma comunidade grande de programadores de [**R**](https://www.r-project.org) no [**Stack Overflow**](https://stackoverflow.com). 

    No [**Stack Overflow**](https://stackoverflow.com) você não poderá fazer perguntas genéricas. Se você tiver com problemas em algum código, construa um exemplo do código resumido e explique detalhadamente o seu problema e o que deseja obter. Assim, você terá grandes chances de sua pergunta ser respondida de forma eficiente, cordial e sem correr o risco de ter a sua pergunta apagada por algum moderador.
      
    **Nota**:

    \BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
    Por falar em [**Stack Overflow**](https://stackoverflow.com), a equipe do [**Stack Overflow**](https://stackoverflow.com) utiliza o [**R**](https://www.r-project.org) e o [**RStudio**](https://www.rstudio.com/) em suas análises. Veja um depoimento     [**aqui**](https://www.rstudio.com/about/customer-spotlight/increasing-the-impact-of-data-at-stack-overflow/).
    </div></div>\EndKnitrBlock{rmdnote}

Utilizar o [**Markdown**](https://daringfireball.net/projects/markdown/) com o [**R**](https://www.r-project.org) dentro do [**RStudio**](https://www.rstudio.com/) é algo interessante e fácil. Porém, para aprender a sintaxe, consideraremos essa [**ferramenta**](https://daringfireball.net/projects/markdown/dingus). Por ela, você poderá testar rapidamente o que o que irá aprender.

#### Parágrafo, cabeçalho e bloco de códigos 

Um parágrafo em Markdown é constrído por uma ou mais linhas de textos separadas por uma ou mais linhas em branco.

</br>

**Escrevendo três parágrafos em Markdown**:


```markdown
Aqui estou criando meu primeiro parágrafo em Markdown. Espero que eu
possa aprender o markdown e assim venha obter sucesso na minha
carreira como estatístico. Darei um espaço abaixo:

Aqui é o meu segundo parágrafo. Só passando para lembrar que R
é uma ótima linguagem de programação. Abaixo colocarei 2 espaços:
  
  
"Qualquer um pode, com algum estudo, escrever códigos que o
computador enteda. Bons programadores esvrevem códigos que
os humanos  entendam." - Alguém, 5 mil anos a.C.
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

</br>

**Acrescendando um cabeçalho**:

Você poderá utilizar uma sequencia do caracter `=` para iniciar uma seção. Analogamente, utilizando o caracter `-` você poderá criar uma subseção. 


```markdown
Um texto com parágrafos soltos
==============================

Aqui estou criando meu primeiro parágrafo em Markdown. Espero que eu
possa aprender o markdown e assim venha obter sucesso na minha
carreira como estatístico. Darei um espaço abaixo:

Aqui é o meu segundo parágrafo. Só passando para lembrar que R
é uma ótima linguagem de programação. Abaixo colocarei 2 espaços:
  

Um programador que não organiza o seu código deveria morrer mais cedo
---------------------------------------------------------------------
  
"Qualquer um pode, com algum estudo, escrever códigos que o
computador enteda. Bons programadores esvrevem códigos que
os humanos  entendam." - Alguém, 5 mil anos a.C.
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

**Importante**: 

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
É importante dizer que esse comportamento poderá veriar de uma ferramenta que suporta a sintaxe de [**Markdown**](https://daringfireball.net/projects/markdown/) para outra. Com o uso frequente de alguma dessas ferramentas, você irá familiarizar-se com algumas possíveis divergências.
</div></div>\EndKnitrBlock{rmdimportant}

</br>

#### Seções/subseções aninhadas

Podemos utilizar sequências do caracter `#` para criar seções aninhadas. O código acima poderia ser alterador por:


```markdown
# Um texto com parágrafos soltos

Aqui estou criando meu primeiro parágrafo em Markdown. Espero que eu
possa aprender o markdown e assim venha obter sucesso na minha
carreira como estatístico. Darei um espaço abaixo:

Aqui é o meu segundo parágrafo. Só passando para lembrar que R
é uma ótima linguagem de programação. Abaixo colocarei 2 espaços:
  

## Um programador que não organiza o seu código deveria morrer mais cedo

"Qualquer um pode, com algum estudo, escrever códigos que o
computador enteda. Bons programadores esvrevem códigos que
os humanos  entendam." - Alguém, 5 mil anos a.C.
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

De uma forma geral, tem-se:


```markdown
# Seção
## Subseção
### Subsubseção
#### Subsubsubseção
...
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

</br>

#### Bloco de Frases

É possível criar, por meio do caracter `>` frases em bloco. Por exemplo, com a ferramenta que utilizo para a construção desse material, temos abaixo três frases utilizando três níveis de blocos.

> Primeiro nível de bloco.

> > Segundo nível de bloco.

> > > Terceiro nível de bloco.


```markdown
> Primeiro nível de bloco.

> > Segundo nível de bloco.

> > > Terceiro nível de bloco.
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**. 

</br>

#### Dando ênfase

É possível que venhamos dar ênfase à um trecho de um texto. Isso é feito utilizando `*` (asterisco), `_` (subilinhado/underscore), `**` (duplo asterisco) ou `__` (duplo subilinhado/underscore). Essas combinações de caracteres devem envolver o texto a ser destacado e fazem:

1. `*` (asterisco): Deixa o texto envolvido em *itálico*. Isso é feito fazendo
    
    ```markdown
    *texto em itálico*
    ```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

2. `_` (sublinhado/underscore): Faz o mesmo que `*`, isto é, deixa o texto envolvido em _itálico_.
    
    ```markdown
    _texto em itálico_
    ```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

3. `**` (duplo asterisco): Deixa o texto envolvido em **negrito**.
    
    ```markdown
    **texto em negrito**
    ```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

4. `__`(dublo subilinhado/underscore): Faz o mesmo que envolver o texto por `**`, isto é, deixa o texto envolvido em __negrito__.
    
    ```markdown
    __texto em negrito__
    ```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.
    
    O código abaixo faz uso do que aprendemos até aqui: 
    
    ```markdown
    # Um texto com parágrafos soltos
    
    Aqui estou criando meu primeiro parágrafo em **Markdown**. Espero que eu
    possa aprender o markdown e assim venha obter sucesso na minha
    carreira como estatístico. Darei um espaço abaixo:
    
    _Aqui é o meu segundo parágrafo_. Só passando para lembrar que R
    é uma ótima linguagem de programação. __Abaixo colocarei 2 espaços__:
      
    
    ## Um programador que não organiza o seu código deveria morrer mais cedo
    
    *"Qualquer um pode, com algum estudo, escrever códigos que o
    computador enteda. Bons programadores esvrevem códigos que
    os humanos  entendam."* - **Alguém**, _5 mil anos a.C_.
    ```
    > --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

</br>
   
#### Listando Itens

Em seu texto, é possível que tenha o intenresse de listar itens de forma não ordenada. Isso é possível utilizando os caracteres `*`, `+` ou `-`. Considere o exemplo:


```markdown
   * Meu primeiro item;
   * Meu segundo item;
   * Meu terceiro item.
        
   ou
        
   + Meu primeiro item;
   + Meu segundo item;
   + Meu terceiro item.
        
   ou ainda
        
   - Meu primeiro item;
   - Meu segundo item;
   - Meu teceiro item.
```

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Você poderá intercambiar os caracteres `*`, `+` e `-`. Ou seja, você poderá fazer:
  </div>\EndKnitrBlock{rmdnote}

```markdown
* Meu primeiro item;
+ Meu segundo item;
- Meu terceiro item.
```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**..
</div>

</br>

#### Enumerando Itens

As vezes necessitamos de itens dispostos segundo uma ordem. Você poderá ordenar os itens utilizando um número seguido de um ponto. Considere o exemplo abaixo:


```markdown
1. Meu primeiro item enumerado;
2. Meu segundo item enumerado;
3. Meu terceiro item enumerado.
```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Os itens enumerados ou não enumerados podem ser formados por parágrafos. Você deverá colocar 4 (quatro) espaços para iniciar um parágrafo de um respectivo item. Considere o código abaixo:
  
</br>
  </div>\EndKnitrBlock{rmdnote}

```markdown
1.    Aqui é o meu primeiro item.
     
      Aqui é um novo parágrafo do meu primeiro item.

2.    Aqui é o meu segundo item.
     
      Aqui é um novo parágrafo do meu segundo item.

3.    Aqui é o meu terceiro item.
     
      Aqui é um novo parágrafo do meu terceiro item.
```

Essa mesma regra vale para os itens não enumerados. Considere o código abaixo:


```markdown
*     Aqui é o meu primeiro item.
     
      Aqui é um novo parágrafo do meu primeiro item.

*     Aqui é o meu segundo item.
     
      Aqui é um novo parágrafo do meu segundo item.

*     Aqui é o meu terceiro item.
     
      Aqui é um novo parágrafo do meu terceiro item.
```
> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.
</div>

</br>

#### Criando Links

</br>

A linguagem de marcação Markdown te permite inserir links no meio do seu texto. Markdown suporta dois estilos de inserção de links. São eles:

  1. **Link não resumido**: As vezes temos o interesse de deixar claro, em nosso texto, qual o endereço completo de um e-mail ou site. Por exemplo, considere o texto do exemplo abaixo:

     **Exemplo 1**: Se você precisar, acesse o <http://www.de.ufpb.br/> do Departamento de Estatística da UFPB. Também, em caso de necessidade, você poderá mandar um e-mail para mim. Meu e-mail é <pedro.rafael.marinho@gmail.com>.

     A forma geral para a construção de links não resumido é `<link>`. Para obtermos o retorno acima, devemos fazer:

     
     ```markdown
         Se você precisar, acesse o <http://www.de.ufpb.br/> do Departamento de Estatística da UFPB. Também, em caso de necessidade, você poderá mandar um e-mail para mim. Meu e-mail é <pedro.rafael.marinho@gmail.com>.
     ```

  2.  **Link resumido**: Trata-se do link que é substituido por um texto sugestivo ao seu conteúdo. Trata-se de uma forma de se construir um link sem a necessidade expor todo o caminho/endereço (froma resumida). Por exemplo, considere o texto do exemplo abaixo:

      **Exemplo 2**: Se você precisar, acesse o [**site**](http://www.de.ufpb.br/) do Departamento de Estatística da UFPB. Também, em caso de necessidade, você poerá mandar um [**e-mail**](mailto:pedro.rafael.marinho@gmail.com) para mim.

      A forma geral para construção de links resumido (sugestivos) é `[testo do link](link)`. Por exemplo, o exemplo cima poderá ser obtido pelo código abaixo:

      
      ```markdown
          Se você precisar, acesse o [**site**](http://www.de.ufpb.br/) do Departamento de Estatística da UFPB. Também, em caso de necessidade, você poerá mandar um [**e-mail**](mailto:pedro.rafael.marinho@gmail.com) para mim.
      ```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

</br>

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Em se tratando de link resumido, para linkar corretamente um e-mail com o programa de envio e recebimento padrão instalado no computador, você deverá utilizar a expressão `mailto:` antes da definição do e-mail ao qual deseja linkar com o programa. Por exemplo:
</div>\EndKnitrBlock{rmdnote}

```markdown
[e-mail](mailto:pedro.rafael.marinho@gmail.com)
```
</div>

</br>

Se você desejar, você poderá ter uma lista enumerada de links ao final do arquivo e invoca-los, por sua numeração, no corpo do seu texto. Considere o texto do exemplo que segue:

**Exemplo**: "**Adoro programar** utilizando a linguagem [**R**](https://www.r-project.org). Para uma melhor experiência, considere programar utilizando a IDE [RStudio](https://www.rstudio.com/products/RStudio/). Programar em [R](https://www.r-project.org) com o [**RStudio**](https://www.rstudio.com/products/RStudio/) torna a tarefa de programar ainda mais agradável. Mais agradável ainda é saber que a linguagem [R](https://www.r-project.org) possui um grande número de [*pacotes*](https://cloud.r-project.org/web/packages/available_packages_by_date.html) para trabalhar com estatística."

Um solução, com o que já aprendemos de Markdown, para esse exemplo acima, poderia ser:

**Solução 1**:


```markdown
"**Adoro programar** utilizando a linguagem [**R**](https://www.r-project.org).
Para uma melhor experiência, considere programar utilizando a IDE
[RStudio](https://www.rstudio.com/products/RStudio/). Programar em [R](https://www.r-project.org) com o [**RStudio**](https://www.rstudio.com/products/RStudio/)
torna a tarefa de programar ainda mais agradável. Mais agradável
ainda é saber que a linguagem [R](https://www.r-project.org) possui
um grande número de [*pacotes*](https://cloud.r-project.org/web/packages/available_packages_by_date.html) para trabalhar com estatística."
```

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

**Solução 2**


```markdown
"**Adoro programar** utilizando a linguagem [**R**][1].
Para uma melhor experiência, considere programar utilizando a IDE
[RStudio][2]. Programar em [R][1] com o [**RStudio**][2]
torna a tarefa de programar ainda mais agradável. Mais agradável
ainda é saber que a linguagem [R][1] possui
um grande número de [*pacotes*][3] para trabalhar com estatística."

[1]: https://www.r-project.org                                                "R"
[2]: https://www.rstudio.com/products/RStudio/                                "RStudio"
[3]: https://cloud.r-project.org/web/packages/available_packages_by_date.html "packages"
```
</br>

> --- Teste [**Aqui**](https://daringfireball.net/projects/markdown/dingus) ou salve o código em um arquivo com extensão **.md** e, no RStudio, faça **Ctrl + Shift + K**.

</br>

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Note que o exemplo acima poderá ser útil em situações que que repetimos linkamos uma palavra ao longo de todo o texto. Nesses casos, a linkagem considerando a numeração dos links poderá ser menos cansativa.
</div></div>\EndKnitrBlock{rmdnote}

#### Inserindo figuras no texto

Se você trabalha com estatística muito provavelmente sente corriqueiramente a necessidade de introduzir, em um texto, gráfico(s) e imagen(s) que explica(m) um resultado obtido ou que nos auxilia(m) à etender um detarminado problema. A sintaxe de inserção de figuras é muito semelhante à sintaxe de inserção de [links][Criando Links].

**Exemplo**: Suponha que desejamos inserir o logo da linguagem de programação [**R**](https://www.r-project.org), na forma abaixo:

</br>


<center>
![](https://www.r-project.org/logo/Rlogo.png){eight="100px" width="100px"} </br>
Figura: Logo da linguagem de programação **R** obtido em [**aqui**](https://www.r-project.org/logo/Rlogo.png).
</center>

</br>

A Figura acima poderá ser inserida na forma que segue:


```markdown
<center>
![](https://www.r-project.org/logo/Rlogo.png){height="100px" width="100px"} </br>
Figura: Logo da linguagem de programação **R** obtido em [**aqui**](https://www.r-project.org/logo/Rlogo.png).
</center>
```

</br>

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Poderá ser que a depender de onde você esteja testando esse código, a expressão `{height="100px" width="100px"}` não venha funcionar. Além disso, não se preocupe com o alinhamento da imagem nem com outros pormenores. Com pouco esforço e utilizando as ferramentas necessárias de R, tudo se ajustará. O objetivo aqui é apenas expor o básico da sintaxe de Markdown.

Você poderá achar estranho algumas sintaxes acima. Abaixo esclareço todas elas:

  * `<center>` ... `</center>`: Essas expressões faz com que tudo o que está envolvido entre elas sejam centralizados na página em HTML que será gerada. Essas expressões também poderá ser útil para centralizar textos.

  > **Exemplo**: Reproduza o exemplo que segue:
</div>\EndKnitrBlock{rmdobservation}
  > > 
  > > ```markdown
  > >    <center>
  > >    Envolver algum texto entre `<center>`e
  > >    </center>
  > > 
  > >    <center>
  > >    fará com que tudo que esteja envolvido seja centralizado.
  > >    </center>
  > > ```

  * `</br>`: Trata-se de um expressão de HTML responsável por pular uma linha. Essa expressão poderá ser utilizada em qualquer lugar do seu código escrito em Markdown.


  * `{height="100px" width="100px"}`: Essa expressão é utilizada para definirmos as dimensões da imagens, a ser inserida, nesse caso em pixels, altura e largura, respectivamente.
</div>


#### Exercícios {-}

1. Construa um código em Markdown que retorne a saída abaixo:

    **R** é um ambiente de software livre para computação estatística e gráficos. Ele compila e é executado em uma ampla variedade de plataformas **UNIX**, **Windows** e **MacOS**. Para fazer o download do **R**, escolha o seu espelho **CRAN** (_Comprehensive R Archive Network_) preferido.

2. Modifique o código em Markdown utilizado no exercício anterior para que forneça:

    [**R**](https://www.r-project.org/) é um ambiente de software livre para computação estatística e gráficos. Ele compila e é executado em uma ampla variedade de plataformas **UNIX**, **Windows** e **MacOS**. Para fazer o download do [**R**](https://www.r-project.org/), escolha o seu espelho **CRAN** ([_**C**omprehensive **R** **A**rchive **N**etwork_](https://cloud.r-project.org/web/packages/available_packages_by_date.html)) preferido.

3. Construa o código em Markdown que forneça uma saída próxima a da imagem abaixo:

    ![](images/ex_markdown_01.png)

4. Forneça o código Markdown para a obtenção do resultado que segue:

    1. **Aqui é o item 1**:

       1. Subitem 1
       2. Subitem 2
       3. Subitem 3

    2. **Aqui é o item 2**:

       + Subitem 1
       + Subitem 2
       + Subitem 3

    3. **Aqui é o item 3**:

       1. Subitem 1
          + Subsubitem 1
          + Subsubitem 2
       2. Subitem 2
          1. Subsubitem 1
          2. Subsutitem 2

</br>

5. Forneça o código Markdown que retore o resultado que segue:

    1. **Aqui é o item 1**:

       1. Eu serei um programador de [**R**](https://www.r-project.org/). Eu prometo de sempre serei fiel, na                alegria e na tristeza, até que a morte           nos separe...

          Além dos votos acima, abaixo segue **dois** motivos para você apresender a programar em                            [**R**](https://www.r-project.org/):

          - Se você não programar, você não irá passar na disciplina. =(

            > ***Acho que o motivo acima é suficiente***.

          - R é uma linguagem legal.

       2. ***[**R**](https://www.r-project.org/) tem vários                                                                  [pacotes](https://cloud.r-project.org/web/packages/available_packages_by_date.html)***:


    2. > Mais algumas coisas **...** :

       > > Bla bla bla bla bla bla bla bla **...**

       + > > > Bla Bla
       + > > > > **...**

       Se tudo der errado, mande um email para **<jesus@aomeudeus.com>** com o título: "**Estou Chegando**".

6. Considere o a imagem desse [**link**](https://www.rstudio.com/wp-content/uploads/2018/10/RStudio-Logo-flat.svg). Crie um arquivo Markdown de modo a ser inserido a imagem com dimensões 50 por 50 pixels centralizada no HTML resultante após a compilação. O resultado que você deverá obter é o que segue:

<center>
![](https://www.rstudio.com/wp-content/uploads/2018/10/RStudio-Logo-flat.svg){eight="250px" width="250px"}</br>
**Figura**: Importando o logo do [**RStudio**](https://www.rstudio.com/) figura qualquer.
</center>

## R Markdown

Se você chegou à esse ponto da leitura, muito provavelmente deverá estar se perguntando sobre muitas coisas. Algumas dessas perguntas poderiam ser:

   1. Como referenciar um texto ou figura?
   2. E se eu quiser colocar figuras lado a lado?
   3. Como incorporar fórmulas matemáticas no corpo do texto?
   4. Como colocar referências no texto?
   5. É possível incorporar tabelas?
   <!-- 6. ~~Eu irei conseguir me formar? O que eu estou fazendo aqui?~~ -->

As respostas à estas perguntas não foram respondidas por serem bastante inconveniente ou mesmo impossível de respondê-las utilizando a linguagem [**Markdown**](https://daringfireball.net/projects/markdown/). A linguagem [**Markdown**](https://daringfireball.net/projects/markdown/) é bastante simples e útil para muitos casos. Aliás, na maior parte do tempo estamos utilizando a sintaxe de [**Markdown**](https://daringfireball.net/projects/markdown/), sendo que algumas vezes é que nós nos deparamos com com algumas dessas necessidades.

Visando atender à diversas exigências, entre elas as que estão enumeradas acima, houve a necessidade de se extender a sintaxe do [**Markdown**](https://daringfireball.net/projects/markdown/) em [**R**](https://www.r-project.org). Essas necessidades corriqueiras são atendidas pelo pacote [**rmarkdown**](https://cran.r-project.org/web/packages/rmarkdown/index.html) que disponibiliza ao usuário o [**R Markdown**](https://rmarkdown.rstudio.com/). O pacote [**rmarkdown**](https://cran.r-project.org/web/packages/rmarkdown/index.html) foi criado por [**Yihui Xie**](https://yihui.name/en/about/), PhD em estatística e que atualmente trabalha como engenheiro de software na [**RStudio, Inc**](https://www.rstudio.com/). Yihui Xie atualmente mantem diversos pacotes em R em seus [**repositórios**](https://github.com/yihui) no GitHub.

<div class="figure" style="text-align: center">
<img src="images/logo_rmarkdown.png" alt="Logo do pacote [**rmarkdown**](https://cran.r-project.org/web/packages/rmarkdown/index.html) - permite programadores [**R**](https://www.r-project.org) extender a sintaxe de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) utilizando [**R Markdown**](https://rmarkdown.rstudio.com/)." width="25%" />
<p class="caption">(\#fig:unnamed-chunk-35)Logo do pacote [**rmarkdown**](https://cran.r-project.org/web/packages/rmarkdown/index.html) - permite programadores [**R**](https://www.r-project.org) extender a sintaxe de marcação [**Markdown**](https://daringfireball.net/projects/markdown/) utilizando [**R Markdown**](https://rmarkdown.rstudio.com/).</p>
</div>

Como dito anteriormente, para fazer uso de [**R Markdown**](https://rmarkdown.rstudio.com/) será necessário o uso do pacote [**rmarkdown**](https://cran.r-project.org/web/packages/rmarkdown/index.html). Esse pacote, por sua vez, trabalha sobre duas importantes ferramentas. São elas:

1. [**knitr**](https://yihui.name/knitr/): Um [**pacote**](https://cran.r-project.org/web/packages/knitr/index.html) também criado por Yihui Xie e que hoje possui diversos colaborados.  O pacote [**knitr**](https://yihui.name/knitr/) permite converter um texto escrito em R Markdown (arquivo com extensão **.Rmd**) para Markdown (arquivo com extensão **.md**). Em 2012, o pacote **knitr** já permitia com algumas linguagens de marcação, entre as mais importantes destacam-se a linguagem LaTeX e HTML. Apenas em 2015 é que foi introduzido o **R Markdown** (arquivos com extensão **.Rmd**), uma vez que o Markdown tinha se mostrado ser um formato de documento popular e bastante utilizado pela comunidade.

2. [**Pandoc**](https://pandoc.org/): Um "canivete suíço" escrito utilizando a linguagem de programação [**Haskell**](https://www.haskell.org/) e que permite converter textos escritos em uma linguagem de marcação para outra. Muito embora você não precisa utilizar diretamente os comandos do Pandoc quando fizer uso do pacote rmarkdown, você poderá instalar facilmente o Pandoc em seus sistema operacional e utilizar o Pandoc para converter arquivos **.tex** (TeX) em **.docx** (DOCX, formato relacionado com a ferramenta Microsoft Word), **.md** (Markdown) em **.pdf** (PDF), **.tex** (LaTeX) para **.md** (Markdown), entre diversas outras conversões. Maiores detalhes a repseito das possíveis conversões você encontrará [**aqui**](https://pandoc.org/demos.html).

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Com o **R Markdown** teremos a nossa disposição diversas ferramentas e ainda poderemos usufruir da simplicidade do **Markdown**.
</div></div>\EndKnitrBlock{rmdnote}

O funcionamento geral e interações entre o pacote **rmarkdown** com o pacote **knitr** e o **Pandoc** poderão ser resumidos com diagrama abaixo:

<div class="figure" style="text-align: center">
<!--html_preserve--><div id="htmlwidget-808d7f733efbe5c3bfbc" style="width:800px;height:400px;" class="DiagrammeR html-widget"></div>
<script type="application/json" data-for="htmlwidget-808d7f733efbe5c3bfbc">{"x":{"diagram":"\ngraph TD\n\nA((.Rmd))-->|knitr|B((.md))\nB-->|Pandoc|C((.html))\nB-->|Pandoc|D((.pdf))\nB-->|Pandoc|E((.epub))\nB-->|Pandoc|F((.odt))\nB-->|Pandoc|G((.docx))\nB-->|Pandoc|H((.tex))\nB-->|Pandoc|I((outros))\n\nstyle A fill:#ffe5cc\nstyle B fill:#ffe5cc\nstyle C fill:#ffe5cc\nstyle D fill:#ffe5cc\nstyle E fill:#ffe5cc\nstyle F fill:#ffe5cc\nstyle G fill:#ffe5cc\nstyle H fill:#ffe5cc\nstyle H fill:#ffe5cc\n"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
<p class="caption">(\#fig:diagramaRmd)Funcionamento do pacote **rmarkdown** que permite trabalharmos com arquivos .Rmd e sua interação com o **knitr** e **Pandoc** na converção para formatos intermediários.</p>
</div>

Como podemos observar no diagrama \@ref(fig:diagramaRmd), o pacote **knitr** é responsável por converter o arquivo **.Rmd** que contém códigos em **R Markdown** para um arquivo **.md** que contém código em **Markdown** puro. Depois, o Pandoc irá agirar sobre o aquivo **.md** e irá converter para o formato desejado, em que por padrão, o formato é **.html**. A conversão para HTML é de longe a mais utilizada, uma vez que trata-se de um formato que facilita o compartilhamento do seu conteúdo, sendo possível, por exemplo, hospedar os HTMLs gerados em um servidor para o acesso de qualquer lugar, desde que se tenha um browser e uma conecção com uma rede de internet.

O pacote **knitr** também incorpora algumas funcionalidades quando estamos trabalhando com **R Markdown**, em que a mais importante delas é a possibilidade de incorporar e avaliar pedaços (**chuncks**) de códigos R dentro do documento, isto é, dentro do arquivo **.Rmd**. Essa é uma grande funcionalidade que nos permitirá fazer duas coisas importantes:

1. Utilizar funções de R para plotagem de gráficos;
2. Incorporar retornos de funções no interior do relatório;

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Acima listei apenas duas funcionalidades de julgo como mais importantes do pacote **knitr**, além, é claro, de converter arquivos **R Markdown** para arquivos em **Markdown** puro.

Uma outra funcionalidade do pacote **knitr** que vale a pena ser destacada aqui, é a possibilidade de utilizar uma de suas função para incorporá figuras previamente salvas (os formatos mais populares de imagens são suportados) e controrar seu tamanhol, título, alinhamento bem como outras características de interesse.
</div></div>\EndKnitrBlock{rmdnote}

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Tudo que você aprendeu a respeito de **Markdown** continuará valendo para arquivos **R Markdown** (arquivos com extensão **.Rmd**).
</div></div>\EndKnitrBlock{rmdimportant}

Antes de iniciarmos as próximas seções a respeito do **R Markdown**, certifique-se que você possue o **rmarkdown** e o **knitr** instalados. Muito provavelmente esses pacotes juntamente com o Pandoc já estarão instalados, caso você esteja utilizando o RStudio.

Em todos os exemplos que seguem nas seções que seguem, no **RStudio**, acesse as opções *File*, *New File* e *R Markdown*, respectivamente, para criar um novo arquivo **R Mardown** (arquivo com extensão **.Rmd**). Você também poderá utilizar as teclas de atalho **Ctrl + Shift + N** para criar um arquivo com extensão **.R** e no momento de salvar mude a extensão do arquivo para **.Rmd**.

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Você poderá compilar o código de **R Markdown** de três formas:

  1. Utilizando, no RStudio, a combinação das teclas de atalho **Ctrl + Shift + K**;
  2. Clicando no ícone do pacote **knitr**;
  3. Utilizando a função `rmarkdown::render(input = "arquivo.Rmd")`. Será criado no diretório de trabalho o arquivo       **arquivo.html**.
</div></div>\EndKnitrBlock{rmdnote}
