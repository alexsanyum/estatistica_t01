# Estatística GA030 - Trabalho 01
Alex Fabricio Sánchez Yumbo\
Programa de Pós-Graduação em Modelagem Computacional\
Laboratorório Nacional de Computação Científica\
Data: Novembro 2023

1. Após abordamos a Lei dos Grandes Números e o Teorema do Limite Central, chegamos a um ponto crucial do curso: a estimação de parâmetros (desconhecidos) associados à distribuição de probabilidade de uma variável aleatória.\
A presente trabalho tem como objetivo a fixação das ideias introduzidas até aqui. Para isso, utilizaremos dados armazenados em quatro arquivos, que contêm amostras de diferentes variáveis aleatórias, conforme Tabela 1.

<div align="center">
  <strong>Tabela 1.</strong> Descrição das variáveis aleatórias. 
</div>

|Variaveil                  |  Arquivo  | Distribuição |
|:----------------------------|:-------------|:----------------|
|$`Q\backsim\mathbb{N}(3,3) `$    |  _data1q.dat_ |      Normal  |
|$` X\backsim\mathbb{U}[0,6] `$    |  _data1x.dat_ |     Uniforme     |
|$` Y\backsim\mathbb{E}(0.333) `$  |  _data1y.dat_ |    Exponencial   |
|$` T\backsim\mathbb{Y}(10,0.30) `$|  _data1t.dat_ |     Binomial     |

**(a)** Dado que conhecemos a distribuição de probabilidades de cada variável aleatória e os parâmetros que as caracterizam (Tabela 1), calcule a expectância e a variância (teóricas) de cada uma delas, usando as definições que vimos em aula.

Todas as equações para el cálculo de expectância e variância são definidas na seguinte tabela.

<div align="center">
  <strong>Tabela 2.1:</strong> Equações de expectância e variância para as diferentes distribuições. 
</div>


| Normal $`\mathbb{N}(\mu,\sigma^2)`$ | Uniforme $`\mathbb{U}[a,b]`$             | Exponencial $`\mathbb{Y}(\gamma)`$       | Binomial $`\mathbb{B}(N, p)`$ |
|-------------------------------------|------------------------------------------|------------------------------------------|-------------------------------|
| $`E[N] =\mu`$                       | $`E[\mathbb{U}] = \frac{a+b}{2}`$        | $`E[\mathbb{Y}] = \frac{1}{\gamma}`$     | $`E[\mathbb{B}] = Np`$        |
| $`V[N] =\sigma^2`$                  | $`V[\mathbb{U}] = \frac{(b-a)^{2}}{12}`$ | $`V[\mathbb{Y}] = \frac{1}{\gamma^{2}}`$ | $`E[\mathbb{B}] = Np(1-p)`$   |

Com nas equações definidas, podemos calcular os valores de expectância e variância teóricos de cada variável aleatória. Os cálculos são mostrados abaixo.
<div align="center">
  <strong>Tabela 2.2.</strong> Valores de expectância e variância teóricas para as variáveis aleatórias. 
</div>


| Variável |Distribuição |      Expectância     |             Variância           |
|----------|:-----------|:---------------------:|:-------------------------------:|
| Q        |Normal      | $`3`$                 | $`3`$                           |
| X        |Uniforme    | $`\frac{0+6}{2} = 3`$ | $`\frac{(6-0)^{2}}{12}= 3`$     |
| Y        |Exponencial | $`\frac{1}{1/3} = 3`$ | $`\frac{1}{{1/3}^{2}}= 9`$      |
| T        |Binomial    | $`10\times0.30 = 3`$  | $`10\times0.30 (1-0.30) = 2.1`$ |

---

**(b)** Utilize o R (ou outro programa) para ler cada arquivo e calcule estimativas para a média e a variância do conjunto de dados (usando todos os dados disponíveis nos arquivos). Em seguida, compare com os resultados obtidos no exercício anterior. Faça comentários.

Os dados foram lidos e analisados em Python usando nas bibliotecas ```numpy``` e ```pandas```. Os cálculos de mádia e variâncias foram feitos com os métodos ```.mean()``` e ```.var(ddof=1)``` onde ddof especifica os graus de liberdade. Quando ddof=1, no método calcula na variância amostral. Os valores estimados são mostrados e comparadas na tabela 3.

<div align="center">
  <strong>Tabela 3.</strong> Médias e variâncias teóricas e estimadas. 
</div>

||Média teórica 	|Variância teórica 	|Média estimada 	|Variância estimada 	|Diferença de médias 	|Diferença de variâncias|
|-----|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
|data1q|    3.0     |3.0    |3.001631   |2.999812   |-0.001631   |0.000188|
|data1x| 	3.0 	|3.0 	|3.000080   |3.006318   |-0.000080   |-0.006318|
|data1y| 	3.0 	|9.0 	|3.002258   |9.044840   |-0.002258   |-0.044840|
|data1t| 	3.0 	|2.1 	|3.003012   |2.105371   |-0.003012   |-0.005371|

Al ter amostras do 500000 de cada variável aleatória, espera-se que os valores calculados se assemelham muito aos valores reais. Ainda os valores aproximados não são exatamente iguais aos teóricos, vemos que eles apenas diferem por três decimais na majoria de casos para nas mádias e variâncias, a excepção da variância do set de dados data1y onde na variância difere dor dois decimais. 

---

**(c)** Construa os histogramas com as frequências relativas de cada uma das variáveis, verificando se estes são condizentes com os modelos teóricos (Tabela 1).

Nos histogramas foram construídos com na função ```histplot()``` da biblioteca ```seaborn``` especificando no parâmetro ```stat = 'density'``` que gera no histograma a partir de na frequência relativa dos dados. No caso do data1t, que vem de uma variável aleatória discreta, foi especificado ```stat = 'proportion'```. Os histogramas se mostram na Figura 1.

![Histogramas](plots/histograms_datasets.png)
<div align="center">
  <strong>Figura 1.</strong> Histogramas das frequências relativas das variáveis aleatórias. 
</div>


Na Figura 1, nos podemos observar os histogramas de todos os sets de dados, onde nas linhas magentas representam na expectância e variância teóricas, e as linhas petras os valores estimados. Las linhas azuis mostram nas respectivas funções de densidade de probabilidade. Na caso do data1t, os pontos azuis representam na função massa de probabilidade.

Observamos que todos os histogramas se ajustam a sus PDFs, médias e variâncias teóricas. Como era de esperar, em todos os gráficos nas médias e variâncias teóricas y estimadas se sobrepõem entre si. No caso de dataset1q, vemos que no histograma tem uma forma gaussiana simétrica, característica de uma distribuição normal. Para na distribuição uniforme, o histograma mostra uma frequência quase constante em el intervalo de valores de 0 a 6, o que se ajusta a seu PDF teórico. No conjunto de dados datasety, este solo contem valores positivos, onde na frequência decresce ao longo do eixo x, o que se ajusta a uma distribuição exponencial com $`\gamma = 1/3`$. Finalmente, no data1t vemos que no histograma só tem barras nos valores inteiros. Este comportamento é esperado, já que os dados vêm de uma distribuição binomial que é uma variável discreta.

Com isto, nos podemos confirmar na hipótese de que cada set de dados vêm de nas distribuições especificadas na Tabela 1.

---

**(d)** Considere cada uma das amostras das variáveis aleatórias, contidas nos arquivos, e suas diferentes distribuições de probabilidade. Tome amostras aleatórias de tamanho $n (n=5,10,50)$ de cada uma das variáveis aleatórias e construa as variáveis aleatórias (estatísticas):

- média amostral:\
$`\overline{W}_{n} = \frac{1}{n}\sum_{i=1}^{n}W_{i}`$

- variância amostral:\
$`S_{W_{n}}^{2}= \frac{1}{n-1}\sum_{i=1}^{n}(W_{i} - \overline{W}_{n})^2`$

onde $`W = Q,X,Y`$ ou $`T`$. Use 10000 amostras simples (pontos amostrais) para gerar as variáveis aleatórias médias amostral e variância amostral. Obs.: Lembre-se das características que as amostras aleatórias devem ter. Apresente o código.

Na função ```construc_rand_var()``` permite gerar _m_ pontos amostrais para um set de dados, e um valor de n específico. Na função utiliza no bucle for para (1) tomar n valores aleatórios do set de dados como um numpy array, (2) calcular na média e a variância amostral usando os métodos ```.mean()``` e ```.var(ddof = 1)```, (3) e salvar os valores calculados em um dicionário.


```python
def construc_rand_var(dataset,n,m):
    
    xbar_values = {'means':[],
                   'vars':[]}

    # loop to repeat the process m times getting m means and variances
    for i in range(m):
        
        # Get the n values of the dataset
        sub_sample = random.choices(dataset,k=n)  
        sub_sample = np.array(sub_sample)
        
        #Calculate mean and variance through numpy 
        sub_mean = sub_sample.mean()
        sub_var = sub_sample.var(ddof = 1)
        
        #Save values in a dictionary
        xbar_values['means'].append(sub_mean)  
        xbar_values['vars'].append(sub_var)
    return xbar_values
```

Além de isso, na função ```construct_n_rand_var()``` permite usar na função anterior para uma lista de valores de n (i.e n = [5,10,50]), retornando dois dataframes (uno para cada variável aleatória) onde cada coluna corresponda a um valor de n.

```python
def construct_n_rand_var(dataset, n_list, m):

    means_n = {}
    vars_n = {}

    # loop to itarete over all elements of the n_list
    for n in n_list:
        # Getting m random points for a especific n
        rnd_vrbl = construc_rand_var(dataset,n,m)  
        
        # Save mean and varincia in a dictionary 
        col_name = 'n=' + str(n)    # Set the name column as n=5,10,50
        means_n[col_name] = rnd_vrbl['means']
        vars_n[col_name] = rnd_vrbl['vars']

    # Convert dictionaries into dataframes
    df_means = pd.DataFrame(means_n)
    df_vars = pd.DataFrame(vars_n)
    
    return df_means, df_vars
```

No seguinte código mostra no uso de nas funções.

```python
# Define n list and m value
n = [5,10,50]
m = 10000

# Get random variables for data1q
mean_rv_dataq, var_rv_dataq = construct_n_rand_var(datasets['data1q'], n, m)

```

---

**(e)** Usando o código da questão anterior, construa os histogramas de frequências das variáveis aleatórias **média amostral** e **variância amostral**, para os diferentes valores de $`n`$ e compare com as distribuições teóricas esperadas para estas variáveis. Faça isso para as variáveis (Q, X, T e Y).

As duas funções mostradas no literal (d) foram usadas para gerar os 10000 pontos para cada variável aleatória em cada set de dados. Além de isso, de acordo no teorema de limite central, nas médias amostrais se aproximam a una distribuição normal $`\mathbb{N}(\mu,\sigma^{2}/n)`$. Nestas distribuições teóricas foram construídas com na biblioteca ```scipy.stats``` que tem na função ```.norm.pdf(x, mean, std)``` que permite construir na PDF de una distribuição normal em um array X com média e desvio padrão específicos. Esses valores foram obtidos da Tabela 2.2. 


![Histograma_Qn](plots/Qn_statistics.png)
<div align="center">
  <strong>Figura 2.</strong> Frequências relativas das médias e variâncias amostrais obtidas da variável Q para n = 5, 10, 50.
</div>
<img src = 'plots/Xn_statistics.png'>
<div align="center">
  <strong>Figura 3.</strong> Frequências relativas das médias e variâncias amostrais obtidas da variável X para n = 5, 10, 50.
</div>
<img src = 'plots/Yn_statistics.png'>
<div align="center">
  <strong>Figura 4.</strong> Frequências relativas das médias e variâncias amostrais obtidas da variável Y para n = 5, 10, 50.
</div>
<img src = 'plots/Tn_statistics.png'>
<div align="center">
  <strong>Figura 5.</strong> Frequências relativas das médias e variâncias amostrais obtidas da variável T para n = 5, 10, 50. 
</div>


---

**(f)** Que tipo de distribuição as médias amostrais apresentam? Justifique com a teoria (_Teorema do Limite Central_) o resultando, apontando as hipóteses básicas. 

O teorema do limite central (TLC) estabelece que na suma do $`n`$ variaveis independentes e identicamente distribuídas se aproxima a uma distribuição normal. No teorema também nos disse que na média de esa suma $`\overline{X}`$ (média amostral), se aproxima a  $`\mathbb{N} (\mu, \sigma^{2}/ n)`$. Também define no caso da variância amostral $`S^{2}`$,tem uma expectância igual a de variáveis originais E$`[S^{2}] = \sigma^2`$. Se tomarmos como hipótese de que o TLC é certo, nós deveríamos poder comprovar estas definições de média e variância amostral empiricamente. Nós fizemos isto neste trabalho, onde construímos médias e variâncias amostrais a partir de diferentes distribuições conhecidas.

Nas médias amostrais (Figura 2-5, parte superior) se pode observar que todos os histogramas tem uma forma Gaussiana característica de uma distribuição normal. Vemos que na média teórica de variáveis aleatórias (Tabela 2.2) é muito próxima à média estimada para os dados do histograma (vemos uma sobreposição para as linhas pretas e megantes) cumprindo com o TLC para no caso de na média amostral. No caso do $\overline{Y}_{n}$ (Figura 4), vemos que para o $n=5$, ela ainda tem uma forma Gaussiana, ela não se ajusta completamente a na distribuição teórica. Isto se deve a que os dados do $Y$ vêm de uma distribuição exponencial onde os dados são assimétricos à izquierda. Esta assimetria pode causar que a média amostral con $n=5$ não se assemelha completamente a na normal esperada. Ao aumentar o tamanho de $`n`$, vemos que os dados se aproximam cada vez mais na distribuição teórica. O TLC estabelece que o $`n`$ debe ser suficientemente grande. No caso de $Y$, vemos que "o grande" varia em cada caso.Contrário a o caso das médias amostrais, na variância amostral não tem um padrão claro.

Em os histogramas da $`S^{2}`$ (Figura 2-5) se observa um comportamento distinto em cada caso. Para de $n=5$, na variância amostral tem um comportamento distinto em cada variável aleatória. Para $\overline{Y}$, no histograma se assemelha a uma distribuição exponencial, enquanto $\overline{X}$ tem uma forma mais simétrica. No caso da $`S^{2}`$ para $\overline{T}$, ele não tem uma forma definida. Somente com $n=50$, todos os histogramas se parecem a uma normal. Ainda elas não têm um patrón definido, vemos que na média estimada do os dados e próxima a na variancia teorica, e dezir, E$`[S^{2}] = \sigma^2`$ se cumple.

No caso que $W$ e uma normal, $`S^{2}`$ tem uma distribuição conhecida. Na aula se mencionou que para este caso $`[\frac{n-1}{\sigma ^{2}}]S^{2}`$ tem uma distribuição de $`\chi ^{2}`$ con $`n-1`$ grados de liberdade. Na Figura 6 mostra os histogramas para os valores de $n=5,10,50$ conjuntamente con na PDF do $`\chi ^{2}`$ correspondiente. Vemos que, em efeito, os histogramas se ajustam a na distribuição teórica. Vemos também que a medida que $`n`$ aumenta, na forma de $`\chi ^{2}`$ se parece a uma distribuição normal. 


<img src = 'plots/chi2_hist.png'>

**Figura 6.** Frequencias relativas $`[\frac{n-1}{\sigma ^{2}}]S^{2}`$ para nas variancias amostrails do $`\overline{Q}_{n}`$. 

Hemos visto que para o caso da média amostral esta se aproxima a uma normal onde na média e na mesma que nas distribuições originais, e para o caso da variância amostral, na expectância de estas é igual a variância original, com isso podemos verificar que o TLC se cumpre.

---

**(g)** Compare os histogramas, para os diferentes valores de $`n`$, e discuta os resultados.

O TLC estabelece que para o caso de média amostral, está se ajusta a $`\mathbb{N} (\mu, \sigma^{2}/ n)`$. E dezir, a medida que aumenta $`n`$, na média se mantém e a variância diminui. Isto se pode comprovar em todos os casos. E nas Figuras 2-5 (parte superior), podemos observar que a média que $`n`$ aumenta, a variância vai diminuindo. De fato, a variância diminui tanto que para os histogramas de $`n=50`$ elas não se ressaltam já que elas se aproximavam muito ao valor da média que não permite distinguirla. Esta observação nos permite confirmar a teoria de o TLC. À medida que $`n`$ cresce, temos maior probabilidade  de tomar valores tão próximos de na média real.
O TLC nos permite ver que não importa na distribuição original de dados, se temos um número grande de realizações/amostras/pontos, nos podemos aproximar nos á na média e variância original de os dados ainda sem conhecer como eles são realmente. No enunciado **(f)** vimos que o conceito do $`n`$ grande cambia de acordo a na complexidade de os dados. Para os casos de $`\overline{Q}_{n}`$, $`\overline{X}_{n}`$, e $`\overline{T}_{n}`$, com $`n=5`$ as médias amostrais se aproximava a na normal teórica, mientras que para $`\overline{Y}_{n}`$, esta se aproxima mejor con $`n=50`$. O TLC sempre se cumprirá à medida que $`n`$ aumenta, cuan "grande" deve ser dependerá de cada caso. 

