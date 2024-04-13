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

- ### Repartitia Poisson, problema cu gandaci

$X$~Pois $(\lambda)\\
P(X=0)$

```r
# Problema cu gandaci
# X e v.a. ce modeleaza nr de gandaci ce vor aparea intr-o zi
# stiind ca in medie apar lambda gandaci intr-o zi
lambda <- 40
# P(X=0)
# Vom folosi o repartitie Poisson(lambda)
dpois(0, lambda)
# P(X=1)
dpois(1, lambda)

plot(0:100, dpois(0:100, lambda), col="magenta")

# In practica, pentru anumite valori ale repartitiei poisson si binomiala
# se poate face repartitia cu repartitia normala
```

### Repartitia exponentiala

$X$ ~ Exp $(\lambda)$

$f(x) = \begin{cases}\lambda \cdot e^{-\lambda x}, x > 0 \\
0 \text{ in rest}\end{cases}\\
E(X) = \displaystyle\frac{1}{\lambda}\\
Var(X) = \displaystyle\frac{1}{\lambda^2}$

$E(X) = \lambda\\
Var(X) = \lambda$

```r
lambda <- 3.14

t <- seq(0.0001, 10, 0.001)
plot(t, dexp(t, lambda), col="magenta", type="l")
# plot(t, dexp(t, lambda), col="magenta", type="l", xlim=c(2,3), ylim=c(0, 0.01))
abline(v=1/lambda, col="blue")

# Calculati probabilitatea ca X <= 1/lambda

print(integrate(dexp, 1/lambda, Inf, rate=lambda)$value)

# Calculati raportul dintre probabilitatile ca x sa ia 
# o valoare mai mare decat media
# respectiv mai mica decat media

# prima abordare (cu calcul integral)
dupa_medie <- integrate(dexp, 1/lambda, Inf, rate=lambda)$value
inainte_de_medie <- integrate(dexp, 0, 1/lambda, rate=lambda)$value
print(dupa_medie/inainte_de_medie)

# a doua abordare (cu calcul probabilistic direct)
# P(X > 1 / lambda) / P(X <= 1 / lambda)
inainte_de_medie <- pexp(1/lambda, lambda)
dupa_medie <- 1 - inainte_de_medie

print(dupa_medie/inainte_de_medie)
```

## Probleme

### Problema 1

Durata necesară(exprimată ȋn ore) pentru reparaţia unei maşini este o variabilă aleatoare
repartizată exponenţial de parametru λ=1/3. Determinaţi:
a) Probabilitatea ca reparaţia să dureze mai mult de 3 ore
b) Probabilitatea ca reparaţia să dureze 12 ore ştiind că reparaţia durează mai mult de 9 ore

$P(a < X \le b) = F(b) - F(a)$

```r
# a)

lambda <- 1/3
print(1 - pexp(1/lambda, lambda))

# b)
prob_noua_ore <- 1-pexp(9, rate=lambda)
epsilon <- 10^(-6)
prob_doispe_ore <- pexp(12 + epsilon, rate=lambda) - pexp(12 - epsilon, rate=lambda)
print(prob_doispe_ore / prob_noua_ore)
```

### Problema 2

Gigel este chemat ȋn instanță pentru a recunoaște paternitatea asupra copilului Lucicăi. Acesta
se apară invocȃnd că nu poate fi tatăl copilului ȋntrucȃt a părăsit țara cu 290 de zile ȋnainte de
nașterea copilului și a revenit ȋn țară cu 240 de zile ȋnainte de nașterea copilului. Un expert
depune marturie ȋn cadrul procesului și afirmă că durata sarcinii unei femei este o variabilă
aleatore a cărei repartiție poate fi aproximată cu repartiția normală de medie 270 și dipersie
100. Ce va decide instanța?

$X$ - durata sarcinii Lucicai
$P((X>290) \cup (X \le 240)) = \\
= P(X > 290) + P(X \le 240) = \\
= 1 - P(X \le 290) + P(X \le 240) = \\
= 1 - F(290) + F(240)$ 

$X$~Norm$(270, 100)$

```r
lambda = 270

# in R al doilea parametru este radical din dispersie (radical din 100 = 10)
print(1 - pnorm(290, lambda, 10) + pnorm(240, lambda, 10))
```

### Repartitia geometrica
Implementarea din R foloseste o repartizare diferita (numara esecurile pana la primul succes).

### Repartitia Poisson
