# Modelli Probabilistici per le Decisioni

## Richiami di statistica

$P(A \lor B) = P(A) + P(B) - P(A\land B)$

$P(A \land B) = P(A|B)*P(B) = P(B|A)*P(A)$

$P(A|B) = (P(B|A)*P(A))/P(B)$

## Reti bayesiane

Una rete bayesiana è un DAG in cui i nodi rappresentano gli eventi e gli archi i rapporti di causalità tra essi.

Ogni Rete Bayesiana costituisce una descrizione completa del dominio che rappresenta e pertanto ogni elemento della distribuzione di probabilità congiunta può essere calcolato a partire dall'informazione contenuta nella rete.

**Formula di fattorizzazione della distribuzione congiunta di probabilità**:

$$
P(x_1,\dots,x_n) = \prod^n_{i = 1} P(x_i | parents(X_i))
$$

**Chain rule**:

$$
P(x1,\dots,x_n) = \prod^n_{i = 1} P(x_i | x_{n-1}, \dots, x_1)
$$

Formula di fattorizzazione e chain rule sono equivalenti a patto che $Parents(x_i) \subseteq {x_{i-1}, \dots, x_1}$

**Markov Blanket**: dato un nodo la sua markov blanket è data dai suoi genitori, dai suoi figli e dai genitori dei suoi figli.

Un nodo è condizionalmente indipendente dai nodi restanti data la conoscenza della sua markov blanket.

**D-separazione**: X e Z sono d-separate da un insieme E di variabili con evidenza sse   ogni cammino non orientato da X e Z è bloccato.

Un cammino è bloccatp sse vale una delle 3 condizioni:

1. Lungo il cammino esiste una variabile V tale che appartiene all'insieme E delle variabili con evidenza e gli archi che collegano V al cammino sono "tail to tail"
   
   ![](img/dsep1.png)

2. Esiste una variabile V lungo il cammino tale che appartiene all'insieme E delle variabili con evidenza e gli archi che collegano V al cammino sono "tail to head"
   
   ![](img/dsep2.png)

3. Esiste una variabile V sul cammino tale che NON appartiene all'insieme E delle variabili con evidenza, nessuno dei suoi discendenti appartiene all'insieme E delle variabili con evidenza e gli archi che collegano V al cammino sono "head to head"
   
   ![](img/dsep3.png)

## Generazione di numeri casuali

**MCM (moltiplicative congruential method)**

$$
x_n = ax_{n-1} \\


0 \leq x_n \leq m
$$

$x_0$ valore iniziale (seed)

$a, m$ interi positivi opportunamente scelti

**LCM (linear congruential method)**:

$$
x_n = (ax_{n-1} + c) \bmod m
$$

$x_0$ valore iniziale

$a, c, m$ opportunamente scelti

$a, c \geq 0;  m> x_0, c , a$

**D-RNG**: Per generare variabili discrete uso la distribuzione cumulativa. Ordino le probabilità in ordine decrescente, estraggo numero casuale e confronto.

**Metodo acceptance-rejection:**

TODO

## Reti bayesiane (inferenza approssimata)

**Algoritmo campiona priori** (per inferenza su reti senza variabili con evidenza)

![](img/campiona-priori.png)

**Campionamento con rigetto (rejection sampling)** (per inferenza su reti con variabili con evidenza): è l'algoritmo campiona priori, quando estraiamo un sample non consistente con l'evidenza scartiamo quel sample. Ovviamente ciò implica molti calcoli inutili all'aumentare delle variabili con evidenza.

**Likelihood weighting**: fissa i valori delle variabili con evidenza e genera campioni solo per i nodi restanti. Inoltre pesa in modo differente i vari eventi, il peso di ogni evento è il likelihood che l'evento associa all'evidenza.

- il meccanismo di likelihood weighting utilizza tutti i campioni generati 

- all’aumentare del numero di nodi con evidenza la performance degrada in quanto molti dei campioni estratti avranno un peso infinitesimale; la stima sarà interamente dipendente da pochissimi campioni con peso comunque piccolo.

$$
P(A = true | E) = \frac{\sum_{s_i:A=true} W_{si}}{\sum_{s_i} W_{si}}
$$

Algoritmo:

- estraggo un campione casuale per le variabili di cui non ho evidenza

- calcolo la probabilità delle variabili con evidenza dati i genitori  e moltiplico: questo è il peso associato al sample.

**Markov Chain Monte Carlo**

Algoritmo:

- Genero casualmente il primo set (escluse le variabili con evidenza)

- Ad ogni step calcolo la probabilità di una variabile senza evidenza a partire dal set di variabili calcolato allo step precedente, usando la sua markov blanket

$$
P(x | MB(X)) = \alpha \cdot P(x | Parents(X)) \cdot \prod_{y \in Children(x)} P(y|Parents(y))
$$

- estraggo un numero casuale e vedo il valore che assume la variabile

- loop a partire da step 2 per n volte

## Catene di Markov




