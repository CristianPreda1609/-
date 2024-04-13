# Variabile aleatoare

$\Omega \rightarrow K$

Variabile aleatoare: 
 - discrete
    - functia de masa ($f$)
    - functia de repartitie ($F$)
    - repartitia
 - continue
    - functie densitate de probabilitate ($f$)
    - functie de repartitie ($F$)
    - repartitia

$X(\Omega)$ - multimea tuturor valorilor pe care le poate lua valoarea aleatoare

## Cazul discret

Repartitia unei variabile discrete se poate arata in forma urmatoare:


$A = \begin{pmatrix} 1 & 2 & 3  \\ \frac{1}{2} & \frac{1}{3} & \frac{1}{6}\\ \end{pmatrix}$

$f:\mathbb{R} \rightarrow \mathbb{R}, f(x) = \begin{cases}\frac{1}{2}, x= 1\\ \frac{1}{3}, x=2\\ \frac{1}{6}, x=3 \\ 0 \text{ in rest}\end{cases}$

$P(x) = P(X \le x)$ - cumulative distribution function (CDF)

$F(x) = \displaystyle\sum_{x_i \le x}^x f(x_i)$

## Cazul continuu

$P(X=x) = 0\\
P(X\in(x - \epsilon, x + \epsilon)) = \displaystyle\int_{x-\epsilon}^{x+\epsilon} f(x) dx$

Functia de probabilitate evaluata intr-un punct nu da o probabilitate. Valorile sale pot fi si mai mari decat 1.

$F(x) = \displaystyle\int_{-\infty}^x f(t) dt$

### Repartitia uniforma

Daca am $X$ repartizat uniform pe $\{1,2, \dots ,n\}$

$X: \begin{pmatrix}1&2&3& \dots & n\\ \frac{1}{n} & \frac{1}{n} & \frac{1}{n} & \dots & \frac{1}{n}\end{pmatrix}$


### Repartitia Bernoulli 

$p$ - probabilitatea de succes

Modeleaza un eveniment in care ai doar doua stari - esec si succes.

$X: \begin{pmatrix}0 & 1 \\ 1-p & p\end{pmatrix}$

### Repartitia binomiala

Repartitia binomiala numara cate succese am obtinut dintr-un numar prestabilit de incercari ($n$), incercarile fiind independente intre ele si avand aceeasi probabilitate de succes ($p$).

$X_1, X_2, \dots, X_n$ independente ~Bern($p$)

$X = \displaystyle\sum_{i=1}^n X_i$ ~Binom($n, p$)

### Repartitia hipergeometrica (Hyper)
- $N$ - cate bile am
- $n_1$ - cate bile vreau sa am deodata
- $n$ - cate extrageri

### Repartitia geometrica
Implementarea din R foloseste o repartizare diferita (numara esecurile pana la primul succes).

### Repartitia Poisson
