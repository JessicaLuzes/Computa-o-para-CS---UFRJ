Untitled
================

rm(list = ls())

``` r
#Instalando tidyverse
#install.packages("tidyverse")
#install.packages("janitor")
#install.packages("rio")
```

``` r
#Carregando pacotes no R
library("tidyverse")
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.2     ✓ dplyr   1.0.3
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library("janitor")
```

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library("rio")
```

``` r
#Abrindo banco de dados
url_fake_data <- "https://raw.githubusercontent.com/leobarone/ifch_intro_r/master/data/fake_data.csv"
## Dado CSV - 
##delim = ";" - Crie um objeto fake a partir do caminho(URL-data);
##O delimitador do arquivo CSV é o ponto e vírgula;
##read_delim - ler arquivos separados por ponto e vírgula...
```

``` r
##Obs: Import é um comando do rio...O rio simplifica os comandos!
##Alternativa para acionar um arquivo da internet:
fake2<-import(url_fake_data)

##Fake - tem 30 linhas e 13 variáveis...
```

``` r
fake <- read_delim(url_fake_data, delim = ";", col_names = T)
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   age = col_double(),
    ##   sex = col_character(),
    ##   educ = col_character(),
    ##   income = col_double(),
    ##   savings = col_double(),
    ##   marriage = col_character(),
    ##   kids = col_character(),
    ##   party = col_character(),
    ##   turnout = col_character(),
    ##   vote_history = col_double(),
    ##   economy = col_character(),
    ##   incumbent = col_character(),
    ##   candidate = col_character()
    ## )

``` r
##Agrupando com filter e pull
##Filter - subconjunto
#Pull - Lista os valores
fake %>% filter(sex=="Male")
```

    ## # A tibble: 15 x 13
    ##      age sex   educ    income savings marriage kids  party  turnout vote_history
    ##    <dbl> <chr> <chr>    <dbl>   <dbl> <chr>    <chr> <chr>  <chr>          <dbl>
    ##  1    35 Male  No Hig…  8214.   5944. Yes      1     Socia… No                 0
    ##  2    43 Male  High S…  4620.  14576. No       0     Indep… Yes                4
    ##  3    38 Male  Colleg…  6463.  14364. No       0     Indep… No                 1
    ##  4    33 Male  Colleg…  2826.  14922. Yes      0     Indep… No                 0
    ##  5    41 Male  High S…  6540.   5419. No       0     Indep… Yes                4
    ##  6    40 Male  Colleg…  2686.  34982. No       0     Socia… Yes                4
    ##  7    37 Male  Colleg…  4180.  15083. Yes      0     Socia… No                 0
    ##  8    34 Male  Colleg…  4537.  35374. Yes      0     Conse… No                 2
    ##  9    33 Male  Colleg…  2202.   4867. Yes      3 or… Indep… Yes                4
    ## 10    43 Male  No Hig…  2300.  14801. Yes      0     Socia… Yes                4
    ## 11    35 Male  Colleg…  2930.  15012. Yes      0     Socia… Yes                1
    ## 12    29 Male  High S…  3018.   5104. Yes      0     Indep… Yes                4
    ## 13    38 Male  High S…  2880.   4785. No       0     Conse… Yes                4
    ## 14    37 Male  High S…   509.   4936. Yes      2     Indep… Yes                2
    ## 15    23 Male  High S…  2724.  15116. No       0     Conse… Yes                0
    ## # … with 3 more variables: economy <chr>, incumbent <chr>, candidate <chr>

``` r
fake %>% filter(sex=="Female")
```

    ## # A tibble: 15 x 13
    ##      age sex    educ   income savings marriage kids  party  turnout vote_history
    ##    <dbl> <chr>  <chr>   <dbl>   <dbl> <chr>    <chr> <chr>  <chr>          <dbl>
    ##  1    37 Female Colle… 2595.   14842. Yes      0     Indep… No                 4
    ##  2    26 Female No Hi… 2167.   24904. Yes      0     Indep… Yes                0
    ##  3    36 Female Colle… 4072.   25399. No       1     Socia… No                 2
    ##  4    29 Female High … 2219.    5118. No       1     Indep… No                 4
    ##  5    42 Female Colle…  448.   14148. No       0     Indep… No                 0
    ##  6    25 Female Colle… 1407.   14756. Yes      0     Indep… Yes                4
    ##  7    35 Female High …   43.7   4203. Yes      0     Conse… Yes                4
    ##  8    35 Female High …  267.    5162. No       0     Indep… No                 4
    ##  9    28 Female Colle… 6696.   45351. Yes      0     Socia… Yes                0
    ## 10    32 Female High …  524.    4640. No       0     Socia… Yes                0
    ## 11    29 Female High …  653.    4718. No       2     Conse… No                 3
    ## 12    30 Female Colle… 6404.    4897. No       3 or… Socia… No                 0
    ## 13    32 Female High …  875.    4885. Yes      0     Conse… Yes                3
    ## 14    35 Female High … 4035.   24970. Yes      1     Indep… No                 4
    ## 15    32 Female High … 2109.    4872. No       0     Indep… Yes                0
    ## # … with 3 more variables: economy <chr>, incumbent <chr>, candidate <chr>

``` r
##Income=renda
##Saber a média do subgrupo...
fake %>% filter(sex=="Male") %>% pull(income)
```

    ##  [1] 8213.8103 4619.9733 6463.0189 2826.0615 6540.1966 2686.4806 4180.4665
    ##  [8] 4537.2010 2202.3451 2300.4241 2929.6419 3017.9495 2879.7574  508.5993
    ## [15] 2724.1537

``` r
##Saber a média de renda dos homens...
fake %>% filter(sex=="Male") %>% pull(income) %>% mean()
```

    ## [1] 3775.339

``` r
##E pode comparar com as mulheres...
fake %>% filter(sex=="Female") %>% pull(income) %>% mean()
```

    ## [1] 2301.018

``` r
##Summarise
  ###Opera com as qtts dentro das colunas..
  ###Nova coluna chamada média_homem...
  ###Temos que observar que nossa variável de agrupamento só tem 2 grupos: homens e mulheres (sexo biológico)
  ###Numa estrutura de países não funciona devido a quantidade, com 18 no total...

fake %>% filter(sex=="Male") %>% 
         summarise(media_homens=mean(income))
```

    ## # A tibble: 1 x 1
    ##   media_homens
    ##          <dbl>
    ## 1        3775.

``` r
###Nova coluna chamada média_homem...
```

``` r
fake %>% filter(sex=="Female") %>% 
   summarise(media_mulheres=mean(income))
```

    ## # A tibble: 1 x 1
    ##   media_mulheres
    ##            <dbl>
    ## 1          2301.

``` r
### Mas esta informação pode ser atribuída a uma niva coluna...
### A sugestão é para países com mais de uma dezena, utilizamos group_by...
### Média - Soma de todos os valores (no caso, aqui, a renda) dividido pela quantidade de pessoas...
### Pode ser a soma das linha qualificadas como mulheres, ou a soma dos sexos...
###Função é a média
###?summarise

?summarise
```

``` r
#Contagem da qtt de indivíduos do sexo masculino e feminino

fake %>%
   group_by(sex) %>%
   summarise(media_renda = n_distinct(income))
```

    ## # A tibble: 2 x 2
    ##   sex    media_renda
    ## * <chr>        <int>
    ## 1 Female          15
    ## 2 Male            15

\#Obs: n = n\_distinct - conta a qtt de linhas, qtt de observações…
\#Contagem dos grupos -

fake %\>% group\_by(sex) %\>% summarise(media\_renda =
n\_distinct(income))

\#Contagem de observações em cada grupo:

fake%\>% count(sex)

#### 

fake %\>% group\_by(sex) %\>% summarise(media\_renda = min(income))

\#Se a mediana é muito diferente da média, agente sabe que os valores
têm concentração nos vaores pequenos ou grandes… \#No caso, aqui, a
mediana é próxima da média indicando que existe simetria nos grupos…

fake %\>% group\_by(sex) %\>% summarise(mediana\_renda = median(income))

#### 

fake %\>% group\_by(sex) %\>% summarise(media\_renda = mean(income),
stdev\_renda = sd(income), media\_idade = mean(age), soma\_eleicoes =
sum(vote\_history))

# Como países que têm mais de uma dezena, utilizamos group by…

fake %\>% group\_by(sex, candidate) %\>% summarise(media\_renda =
mean(income))

\#Sumários estatísticos \#Média fake %\>% group\_by(sex) %\>%
summarise(media = mean(income))

\#Desvio padrão fake %\>% group\_by(sex) %\>% summarise(desvpad =
sd(income))

\#Mediana fake %\>% group\_by(sex) %\>% summarise(mediana =
median(income))

\#Quantis fake %\>% group\_by(sex) %\>% summarise(quantil\_10 =
quantile(income, probs = 0.1), quantil\_25 = quantile(income, probs =
0.25), quantil\_75 = quantile(income, probs = 0.75), quantil\_90 =
quantile(income, probs = 0.9))

\#Contagem e soma fake %\>% group\_by(sex) %\>% summarise(contagem =
n(), soma = sum(age))

\#Removendo NAs fake %\>% group\_by(sex) %\>% summarise(media =
mean(income, na.rm = TRUE))

\#Construindo uma tabela como objeto fake %\>% group\_by(sex, candidate)
%\>% summarise(media\_renda = mean(income)) %\>%
pivot\_wider(names\_from = sex, values\_from = media\_renda)

\#Criando variáveis com os sumários estatísticos fake2 \<- fake %\>%
group\_by(sex) %\>% mutate(renda\_grupo = mean(income))

view(fake2)

\#Ordenando os dados fake %\>% arrange(age)

fake %\>% arrange(-age) \#ordem decrescente

fake %\>% arrange(-age, vote\_history) \#combinando variáveis

fake %\>% group\_by(candidate) %\>% summarise(media\_renda =
mean(income)) %\>% arrange(media\_renda) \#candidato por média de renda
do eleitor

fake %\>% arrange(age) %\>% slice(1:10)

fake %\>% arrange(age) %\>% slice(25:n()) fake2 \<- fake %\>%
group\_by(sex) %\>% mutate(renda\_grupo = mean(income)) %\>% ungroup()
\#desligando o “group\_by”
