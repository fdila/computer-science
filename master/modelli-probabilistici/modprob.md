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


