# Versionamento de código

<img src="images/versoes_git.png" width="65%" style="display: block; margin: auto;" />

Na estatística, a todo momento estamos editando documentos, como por exemplo códigos, artigos, relatórios, aulas, apresentações, livros, entre outros. Nesse processo de edição dos mais variádos documentos, quase sempre sentimos a necessidade de versionar o conteúdo, uma vez que se não houver um versionamento e se desejarmos voltar à um estado de edição anterior, estariamos sobre uma tarefa extremamente difícil ou mesmo impossível, a depender do número de passos anteriores ao qual desejamos voltar.

Quando não dominamos nenhum sistema de controle de versão, normalmente o que fazemos para ter a possibilidade de voltar para uma dada versão de edição é armazenar diversas cópias do projeto em diretórios distintos. Versionar dessa forma pode servir quando temos poucas versões, proém, mesmo assim é comum os desarranjos e atrapalhos ao se tomar conta de diversos diretórios. Quando se domina um sistema de controle de versão evitamos esse tipo de problema, uma vez que continuaremos trabalhando sobre um mesmo diretório que terá seus estados modificados quando solicitado, isto é, será possível voltar para a distribuição de arquivos e conteúdos anteriores, mesmo se nesse processo de edição alguns arquivos foram deletados, renomeados ou fortemente modificados.


**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Não se preocupe se você voltar à estados anteriores e desistir. Você poderá retornar à estados mais recentes (incluindo o último) sem nenhum problema. **Deixe o trabalho sujo com um sistema de versionamento**.  

Além disso, para nós estatísticos que vivemos codificando e constantemente alterando códigos de programação, versionar de forma eficiente é algo crucial.
</div></div>\EndKnitrBlock{rmdimportant}

## Git

Visando ajudar o desenvolvedor na tarefa de versionamento de projetos/códigos, a ferramenta [**git**](https://git-scm.com/) foi desenvolvida, escrita utilizando a linguagem C, por [**Linus Torvalds**](images/linus_torvalds.jpg) (criador do Linux) e [**Jun Hamano**](images/ju_hamano.jpeg), um engenheiro de sofware japonês. No [**git**](https://git-scm.com/), cada diretório de trabalho é um repositório com histórico completo das versões e não depende de acesso à um servidor ou rede central. Essa é uma das características que torna o git uma ferramenta rápida, além, é claro, de ser escrito em C, que reduz a sobrecarga de tempos de execução que é algo normalmente comum em linguagens de nível superior.

Inicialmente essa ferramenta visava ajudar os desenvolvedores do kernel do Linux na tarefa de versionar, de forma eficiente, as mudanças no kernel que antes eram versionadas por meio do [**BitKeeper**](http://www.bitkeeper.org/), um software proprietário desenvolvido pela  BitMover Inc, Califórnia. Isso era um dilema entre os desenvolvedores do Linux, uma vez que ao contrário do [**BitKeeper**](http://www.bitkeeper.org/), o Linux é conhecido por suas [**iniciativas Open Source**](https://opensource.org/). À época, o projeto Linux tinha acesso gratuito ao [**BitKeeper**](http://www.bitkeeper.org/). Porém, com a acusação de programadores do kernel Linux estarem utilizando engenharia reversa, o acesso gratuito foi removido. 


Além do git, atualmente existem algumas ferramentas para versionamento de códigos. Entre tais ferramentas, enumero duas:

1. [**mercurial**](https://www.mercurial-scm.org): Trata-se de um sistema de versionamento, assim como o git, com [**iniciativas Open Source**](https://opensource.org/). Na internet é fácil encontrar diversos comparativos, em que muitos usuários citam como uma de suas vantagens a facilidade. O [**mercurial**](https://www.mercurial-scm.org) é o sistema de versionamento mais popular na plataforma de hospedagem de código fonte [**Bitbucket**](https://bitbucket.org/product/) que não é tão popular quanto o [**GitHub**](https://github.com/) e o [**GitLab**](https://about.gitlab.com/); 
  
2. [**subversion**](http://subversion.apache.org/): Trata-se de um sistema de versionamento distribuido sobre os termos da [**Apache License**](https://pt.wikipedia.org/wiki/Licen%C3%A7a_Apache) e que foi desenvolvido pela [**Apache Software Foundation**](https://pt.wikipedia.org/wiki/Apache_Software_Foundation).


Por se tratar do sistema de versionamento mais amplamente utilizado (mais popular) em versionamentos locais e remotos (a exemplo do [**GitHub**](https://github.com/) e [**GitLab**](https://about.gitlab.com/) que são plataformas de hospedagem de código, em que é possível facilmente enviar códigos versionados usando git), trataremos  apenas do uso do [**git**](https://git-scm.com/).

**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
A ferramenta [**git**](https://git-scm.com/) poderá ser facilmente instalada em Linux/Unix, Windows e macOS. Clique [**aqui**](https://git-scm.com/downloads) e faça o download da versão desejada e instale em seu sistema operacional. Há diversos vídeos na internet ensinando a configurar o [**git**](https://git-scm.com/) em sistemas Windows. 
</div></div>\EndKnitrBlock{rmdnote}

Após a instalação do [**git**](https://git-scm.com/) em seu sistema operacional, abaixo listarei algumas funções interessantes para o uso do [**git**](https://git-scm.com/) via o prompt de comando (terminal). O terminal ao qual você deverá trabalhar com o git é algo parecido com as imagens abaixo:

<div class="figure" style="text-align: center">
<img src="git_files/figure-html/unnamed-chunk-4-1.png" alt="A imagem mais a esquerda refere-se ao terminal bash no linux e a mais a direita refere-se terminal bash instalado no Windows para o uso do git. Essas imagens são meramente ilustrativas e poderão variar um pouco a depender do sitema operacional." width="768" />
<p class="caption">(\#fig:unnamed-chunk-4)A imagem mais a esquerda refere-se ao terminal bash no linux e a mais a direita refere-se terminal bash instalado no Windows para o uso do git. Essas imagens são meramente ilustrativas e poderão variar um pouco a depender do sitema operacional.</p>
</div>

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
  
Para usuários de sistemas operacionais baseados em Arch Linux, por exemplo, usuários do [**Manjaro Linux**](https://manjaro.org/), a instalação do [**git**](https://git-scm.com/) é bastante fácil. No terminal do Linux, basta fazer: </br></br>
  </div>\EndKnitrBlock{rmdobservation}

```shell
sudo pacman -S git 
```
  
Caso você tenha optado em utilizar alguma distribuição GNU/Linux que não é derivada do Arch, muito provavelmente você não seguiu as considerações da distribuição Linux sugeridas na Seção [**Algumas distribuições**][Algumas distribuições], em que sugiro o uso do [**Manjaro Linux**](https://manjaro.org/) ou de distribuições GNU/Linux derivadas do [**Arch**](https://www.archlinux.org/). Dessa forma, busque na distribuição GNU/Linux escolhida o comando para a instalação do [**git**](https://git-scm.com/).

> **Nota**: Se você está utilizando alguma distribuição GNU/Linux baseada em Debian/Ubuntu, você poderá instalar o [**git**](https://git-scm.com/) fazendo `sud apt-get install git`. Outros a respetio da instalação do git poderão ser encontrados [**aqui**](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Instalando-o-Git).

No Linux, o [**terminal bach**](https://pt.wikipedia.org/wiki/Bash), que é instalado por padrão, será o terminal que utilizaremos o [**git**](https://git-scm.com/). Não há nenhuma necessidade de utilização de termais complementares. No [**terminal bach**](https://pt.wikipedia.org/wiki/Bash), para facilitar, você pode chamar simplesmente de "terminal do linux" é onde configuramos o sistema operacional, instalamos programas, removemos programas, programamos, compilamos, **utilizamos o git**, etc. É incrível a flexibilidade e a quantidade de coisas que podemos fazer no terminal do Linux.

Usuários do sistema operacional Windows poderão instalar facilmente o [**git**](https://git-scm.com/) considerando o executável fornecido [**aqui**](https://gitforwindows.org/index.html). Se o seu sistema for 64 bits, vá ao final da página e faça o download do arquivo **Git-x-64-bit.exe**, em que **x** dá lugar a versão do [**git**](https://git-scm.com/).

Para esses usuários, durante o processo de instalação, no passo ***Adjusting your PATH environment***, é importante selecionar a última opção, conforme a imagem abaixo: 

<img src="images/git_windows_opcao.png" width="55%" style="display: block; margin: auto;" />

Após a instalação do [**git**](https://git-scm.com/), em seu sistema operacional, abra o terminal e execute o comando `git --version`. Em caso de retorno da versão instalada do [**git**](https://git-scm.com/), muito provavelmente a instalação ocorreu corretamente.
</div>


Após instalar corretamente o git, a primeira coisa que você precisa fazer é configurar o seu nome de usuário e endereço de e-mail. Isso é de grande importância, uma vez que cada commit (compromentimento), a informação do usuário que fez alguma atualização do documento/projeto é utilizada. Ou seja, trata-se de uma espécie de "carimbar" o autor da modificação. Sendo assim, no terminal, faça:


```shell
git config --global user.name "seu nome ou sigla"
git config --global user.email seu_email
```


**Nota**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
A configuração acima só precisará ser realiazada uma única vez, uma vez que foi utilizado a opção `--global` no momento de definir o usuário e senha. Além disso, você sempre poderá realizar essas configurações, sem a necessidade de instalar novamente o git, caso deseje trocar o nome do usuário e e-mail utilizado.
</div></div>\EndKnitrBlock{rmdobservation}

Após instalar e configurar corretamente o git em seu sistema operacional, considere os comandos enumerados e descritos abaixo:

  1. 

  2.

  3.

  4.
  

## GitHub

(**conteúdo visto em sala de aula**)

