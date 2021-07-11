# Pattern Matching

## Pattern matching esatto

### Pattern matching con automi
Prima si costruisce tabella transizioni dell'automa per il pattern con la funzione:
$$
\delta(j, \sigma) : \{0 \dots m \} \times \Sigma \rightarrow \{0 \dots m \}
$$

con $m$ uguale alla lunghezza del pattern.

$$
\delta(j, \sigma) = j + 1 \iff j < m \land P[j+1] = \sigma
$$


$$
\delta(j, \sigma) = k \iff P[j+1] \neq \sigma \lor j = m 
$$
$$
k = |B(P[i,j] \sigma)|
$$




### KMP

### Bayeza-Yates e Gonnet

## Pattern matching approssimato

### Wu-Manber

## Text indexing

### Suffix array

### BWT

### Ricerca esatta con FM-index

