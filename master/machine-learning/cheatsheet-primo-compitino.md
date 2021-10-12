# Cheatsheet 1 compitino

- Cardinalità spazio delle istanze:

$$
|X| = \Pi|A_i| \\
\text{con Ai attributo}
$$

- Cardinalità spazio dei concetti:

$$
|C| = 2^{|X|}
$$

- Cardinalità spazio delle ipotesi, semanticamente:

$$
|H|_{sem} = 1 + \Pi(|A_i| +1)
$$

1 fuori produttoria rappresenta l'ipotesi più specifica:se un'ipotesi ha almeno 1 attributo vuoto è uguale a qualsiasi altra ipotesi con 1 attributo vuoto
+1 dentro la produttoria per contare anche i ?



- Cardinalità spazio delle ipotesi, sintatticamente:
  
  $$
  |H|_{sem} = \Pi(|A_i| +2)
  $$

+2 per contare sia ? che simbolo vuoto



- Entropia di una variabile X:
  
  $$
  H[X] = - \sum p_i * log_2p_i
  $$
  
* Entropia condizionata pt1
  
  $$
  H[T|X=x_i] = -\sum P_{T|X}(t_j, x_i)*log_2(P_{T|X}(t_j, x_i)) 
  $$
- Entropia condizionata p2
  
  $$
  H[T|X] = \sum P(x)*H(T|X=x)
  $$

- Information Gain
  
  $$
  IG[T|X] = H[T] - H[T|X]
  $$
  
  
