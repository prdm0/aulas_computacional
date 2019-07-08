--- 
knit: "bookdown::render_book"
title: "ESTATÍSTICA COMPUTACIONAL"
subtitle: "Disciplina ministrada à alunos do bacharelado em estatística da UFPB"
author: "**Docente**: Prof. Dr. Pedro Rafael Diniz Marinho <br/> **E-mail**: <pedro.rafael.marinho@gmail.com> / <pedro@de.ufpb.br>"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
always_allow_html: yes
bibliography: [book.bib, packages.bib]
biblio-style: apalike
url: 'https://prdm0.github.io/aulas_computacional/'
github-repo: prdm0/aulas_computacional
link-citations: yes
colorlinks: yes
fontsize: 13pt
monofont: "Source Code Pro"
description: "Disciplina de Estatística Computacional - Departamento de Estatística"
---

# Início {-}

**Última atualização**: 08/07/2019 <br/>
**Departamento de Estatística (UFPB)**: <http://www.de.ufpb.br/> 

---

<p align="center">
<img src="images/logo_livro.png" width="220" height="350"/>
</p>

---

**Licença**

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Licença Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />O material <span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Estatística Computacional</span> do <a xmlns:cc="http://creativecommons.org/ns#" href="https://prdm0.github.io/aulas_computacional/" property="cc:attributionName" rel="cc:attributionURL">Prof. Pedro Rafael. D. Marinho</a> está licenciado com uma Licença <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons - Atribuição-NãoComercial-CompartilhaIgual 4.0 Internacional</a>. Isso quer dizer:

1. Você tem o dirieto de copiar e redistribuir o material em qualquer suporte ou formato;

2. Você tem o direito de remixar, transformar e criar a partir deste material;

3. Você deve dar crédito apropriado, fornecer um link para a licença e indicar se foram feitas alterações. Você pode fazê-lo de qualquer maneira razoável, mas de nenhuma maneira que sugira  que o licenciador endossa você ou seu uso;

4. Você não poderá utilizar o material para fins comerciais;

5. Se você remixar, transformar, ou criar a partir do material, tem de distribuir as suas contribuições sob a mesma licença que o original. Sendo assim, não poderá aplicar termos jurídicos ou medidas de caráter tecnológico que restrinjam legalmente outros de fazerem algo que a licença permita. 

**Maiores detalhes a respeito da licença em**: <https://creativecommons.org/licenses/by-nc-sa/4.0/>.

**Observação**:

\BeginKnitrBlock{rmdobservation}<div class="rmdobservation"><div class=text-justify>
Os códigos que estão presentes nesse material estão sobre os termos [**GNU General Public License**](https://www.gnu.org/licenses/gpl-3.0.pt-br.html) ($\geq 3$, versão três ou superior). Assim, o leitor poderá fazer uso de qualquer código desse material em seus projetos, pacotes, desde que cite a fonte. Além disso, todas as imagens utilizadas nesse material são de uso livre e não comercial.

**Na barra superior desse material você poderá encontrar um ícone para download das minhas aulas de R. Trata-se de um Portable Document Format (PDF) que contém minhas aulas de R. O material das aulas está sujeito a mesma licença desse material. Você é livre para utilizar e remixar, desde que referencie o autor e o [**Departamento de Estatística**](http://www.de.ufpb.br/) da [**UFPB**](https://www.ufpb.br/). Além disso, você deverá deixar claro quais foram as modificações realizadas.**
</div></div>\EndKnitrBlock{rmdobservation}

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Esse material está sob constante aprimoramento e sugestões poderão ser enviadas para o repositório do [**GitHub**](https://github.com/prdm0/aulas_computacional) que hospeda este conteúdo. 

Uma vez que o material está sendo mantido e versionado no [**GitHub**](https://github.com/prdm0/aulas_computacional), as alterações podem ser realizadas diretamente no arquivo fonte do projeto, bastando clicar no ícone em formato de um lápis, no canto superior esquerdo desta página, ou das páginas em que se desejam sugerir alterações, como correções de palavras, mudanças de parágrafos, alteração de códigos, melhoramento de exemplos, inclusão de novos exemplos, etc. As alterações serão bem vindas e serão acatadas (incorporadas ao arquivo orignal) na medida que forem julgadas como sendo convenientes.
</div></div>\EndKnitrBlock{rmdimportant}

**Nota**: 

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Para que seja possível propor alterações é necessário que você saiba utilizar o [**git**](https://git-scm.com/)/[**GitHub**](https://github.com/prdm0/aulas_computacional) e tenha realizado um fork do trabalho em sua conta do [**GitHub**](https://github.com/prdm0/aulas_computacional). Apreder a utilizar o [**git**](https://git-scm.com/)/[**GitHub**](https://github.com/prdm0/aulas_computacional) poderá ser muito útil (dentro da academia ou fora dela), uma vez que você saberá versionar seus códigos, artigos e trabalhos em geral.
</div></div>\EndKnitrBlock{rmdnote}
