# Prerequisiti di computazione

Macchina di Turing ragionano in binario, ho in input una stringa di 0 e 1 e in output ho un bit, si ha la funzione:

$$
f : \{0,1\}^* \rightarrow 0,1
$$

Definiamo $L\pi$ come un linguaggio di decisione, il cui risultato è binario (accetto/non accetto)

Una TM deterministica $M$, con $T: \mathbb{N} \rightarrow \mathbb{N}$ funzione calcolabile dalla TM, accetta $L\pi$ in tempo $T(n)$ se $\forall x$ con $|x| = n$, $M$ accetta $x$ in $T(n)$ mosse o configurazioni.

Un problema di decisione $\pi$ riceve in input un'istanza $x$ e restituisce $1$ se l'istanza appartiene al linguaggio o $0$ se non appartiene. $L\pi$ contiene quindi tutti gli input per cui $\pi$ dà in output $1$.

La funzione associata al problema si chiama $f\pi$ e, dato un input, restituisce $1$ sse l'input appartiene a $L\pi$.

La **classe P** è definita come la classe dei linguaggi di decisione accettati in tempo $T(n) = cn^p, p \in \mathbb{N}, p \neq 0$  da una macchina di Turing deterministica. P è una classe di problemi di decisione.

Si definisce che $L\pi$ è accettato da una TM in tempo $T(n)$ se $\exists T : \mathbb{N} \rightarrow \mathbb{N}$ calcolabile da TM e $\forall x \in L\pi, |x| = n$ la TM accetta $x$ e risponde 1 al più di $T(n)$ mosse di calcolo.

Per il modello della macchina RAM si parla invece di problemi di decisione, quindi, a differenza della TM, oltre ad accettare gli input che appartengono a $L\pi$, rifiuta quelli che non appartengono.
Possiamo ottenere la stessa cosa usando una macchina di Turing TM che accetta il linguaggio e una macchina di Turing complementare che risponde yes se la stringa non appartiene al linguaggio.

È dimostrabile che se $L\pi$ è accettabile in tempo polinomiale allora nello stesso tempo è anche decidibile.
