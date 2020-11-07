# Cheatsheet sistemi embedded

## Formule segnali analogici

**Precisione**: $rangeSegnale/2^{nbit}$

**Range dinamico/SNR**: $6*nbit$

## Formule scheduling

### EDF

I task con deadline assoluta più vicina hanno priorità maggiore

**Test schedulabilità EDF**: $\sum_{i=1}^n \frac{C_i}{T_i} \le 1$

(test necessario e sufficiente)

### Rate monotonic

I task con periodo più piccolo hanno priorità maggiore

**Test schedulabilità (iperbolico) RM**:  $\prod^n_{i=1} (U_i + 1) \le 2$ 

(test sufficiente ma non necessario)

### Deadline monotonic

Deadline relativa e periodo non coincidono, i task con deadline relativa più piccola hanno priorità maggiore.

**Test schedulabilità per DM**

Ordiniamo i task per deadline relativa. Test:

$$
\forall i : 1 \le i \le n \quad C_i + I_i \le D_i
$$

dove I_i è la misura dell'interferenza relativa al task i-esimo, e può essere calcolata come la somma del processing time di tutti i task a priorità maggiore rilasciati prima di D_i:

$$
I_i = \sum_{j=1}^{i-1} ceiling(\frac{D_i}{T_j})C_j
$$

Notiamo che questo test è sufficiente ma non necessario per garantire la schedulabilità del task set.
