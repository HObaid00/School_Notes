## Definition
Att X är binomialfördelad betecknas 
$$\Large
X \sim Bin(n,p) \quad \text{där} \quad n \in \mathbb{Z}^+ 
\quad \text{och} \quad p \in (0,1)
$$
En fördelning med enbart $Sant \ | \ Falskt$ eller enbart två val.

## Värderum
$$\Large
S = \{0, 1, \dots, n\}
$$

## Täthetsfunktion 
$$\Large
p(k) = \binom{n}{k} p^k (1−p)^{k} 
$$

## Väntevärde & Varians
$$\Large
E(X) = np $$
$$\Large V(X) = np(1−p)$$
$$\Large D(X) = \sqrt{np(1-p)}$$
## Oberoende Variabler
Ifall 
$$\Large
X \sim Bin(m, p), \quad Y \sim Bin(n, p)
$$
Då blir det sammanlagda:
$$\Large
X + Y \sim Bin(m+n, p)
$$

## Satser

#### 1. Flera Oberoende Variabler
Ifall variablerna 
$$\Large
X_1, X_2, \dots, X_n $$
är oberoende
$$\Large 
S = \sum_{i=0}^n X_i \quad X_i =  
\begin{cases}  
1 \ \text{med sannolikhet } p \\
0 \ \text{med sannolikhet } 1- p
\end{cases}
\quad(\text{dvs } X \sim Bern(p) )
$$

> På så vis kan varje binomialfördelad variabel S ses som en summa av n Bernoullifördeleade variabler

> Extersom $E(X_i) = p$ och $V(X_i) = p(1-p)$ är enligt CGS 
> 

$$\Large
S \in N (np, \sqrt{np(1-p)})
$$
Dock är 
$$\Large
P(S \le k) \= \Phi (\frac{k+ \frac{1}{2} - np}{\sqrt{np(1-p)}})
\quad
\text{(halvkorrektion)}
$$

## Fördelnings Figure

![[Pasted image 20260418193713.png|697]]