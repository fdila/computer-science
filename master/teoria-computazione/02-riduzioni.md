# Riduzioni polinomiali

## Descrizioni problemi

### 3-SAT
In input ho una formula booleana $\phi$ in forma normale congiunta (CNF), ovvero con congiunzione $\land$ tra le clausole. Una clausola è un $\lor$ di letterali, ovvero di variabili booleane $x_i$ oppure $\lnot x_i$. Nello specifico in 3-SAT ho 3 letterali. In output ho se la forma è soddisfacibile o meno.


### Indipendent set

L'indipendent-set di un grafo non orientato è un sottoinsieme $I \subseteq V$ tale che $\forall u,v \in I (u,v) \notin E$.
Il problema ind-set, nella sua versione di ottimo, è quello di trovare l'indipendent-set di cardinalità massima di un grafo non orientato.
Nella sua versione di decisione si ha il parametro $k$ intero e si cerca se esiste un ind-set di cardinalità uguale a $k$. L'indipendent-set di cardinalità massima può essere usato come "certificato".

### Vertex cover

### Set cover

### Clique

### TSP

### Ciclo hamiltoniano

## Riduzioni tra i problemi

La riduzione è la trasformazione dell'input di $w$ in $A$, in un input $f(w)$ per $B$ in tempo polinomiale. La risposta di $B$ con con input $f(w)$ è la stessa che $A$ dà con input $w$.
Si dice che $A$ si riduce polinomialmente a $B$ e si scrive:

$$
A \le_p B
$$

se $\exists f$ tale che:

$$
w \in L_A \iff f(w) \in L_B
$$

e $f(w)$ è calcolabile in tempo polinomiale.

### 3-SAT $\le_p$ ind-set

Possiamo dire che $\phi$ è soddisfacibile sse $G_{\phi}$ ha un indipendent-set di cardinalità $k = |\phi|$, con $|\phi|$ pari al numero delle clausole della formula.
Costruisco quindi un grafo che ha come un vertice per ogni letterale della clausola. Collego i 3 letterali della clausola ottenendo un triangolo detto "gadget" (che rappresenta la clausola), e collego ogni letterale con il suo negato.

### vertex-cover $\le_p$ ind-set

### set-cover $\le_p$ vertex-cover

### Clique $\le_p$ 3-SAT

### HML $\le_p$ TSP
