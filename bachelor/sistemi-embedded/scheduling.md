# Scheduling

## Vista generale

**Real Time:** sistema deterministico e predicibile, che reagisce agli eventi entro un tempo prestabilito (deadline)

Un task real time può essere:

- Hard: se il risultato è prodotto dopo la deadline ha conseguenze catastrofiche

- Firm: se il risultato è prodotto dopo la deadline diventa inutile, ma non causa danni.

- Soft: se il risultato è prodotto dopo la deadline è ancora un pochino utile, anche se causa una degradazione delle performance

Requisiti di un sistema real time:

- Timeliness; rispetta costraint di tempo

- Predicibile

- Efficiente

- Robusto

- Tollerante ai fault

- Mantenibile

### Avere un sistema predicibile

Uno degli aspetti fondamentali de sistemi RT è la prevedibilità: tutti gli aspetti non-deterministici del sistema devono essere eliminati, esclusi o ridotti al minimo al fine di permettere l'analisi statica dei tempi di esecuzione del sistema. Alcuni dei fattori che contribuiscono al non-determinismo sono:

- DMA: il dma ruba cicli al processore in modo non deterministico.

- Cache: a seconda di hit/miss cambiano i tempi di esecuzione, e non si può sapere a priori quante hit/miss ci saranno.

- Interrupt: vari modi per gestirle (3 approcci)

- Syscalls: devono aderire a precisi standard temporali: ogni sezione del sistema che non può essere interrotta potrebbe introdurre un ritardo aleatorio, pertanto anche le chiamate di sistema devono essere pre-emptable.

- Semafori: possono causare inversione di priorità

- Gestione della memoria: in generale nei sistemi RT si tende ad evitare la
  paginazione dinamica, per eliminare i ritardi dovuti alle page fault, e a partizionare la memoria insegmenti di dimensione predefinita.

## Concetti base

Una schedule è l'assegnamento dei task al processore, in modo che ogni task sia eseguito fino ad essere finito.

Una schedule è fattibile se tutti i task possono essere completati tenendo conto di un set di costraint specificati

Un set di task è schedulabile se esiste almeno un algoritmo che produce una schedule fattibile.

### Tipi di costraint dei task

- Timing

- Relazioni di precedenza

- Mutua esclusione su risorse condivise

#### Timing costraints

Costraint tipica è la _deadline_ ovvero il tempo in cui il processo deve essere completato. Se la deadline è relativa al tempo di arrivo del task è una deadline relativa, se è specificata rispetto al tempo 0 è assoluta. 

Classificazione deadline come primo capitolo.

Un task è caratterizzato da:

- Tempo di arrivo: tempo al quale il task diventa ready pre l'esecuzione. è anche chiamato request time o release time ed è indicato con $r_i$

- Computation time $C_i$ tempo necessario per eseguire il task

- Absolute deadline $d_i$

- Relative deadline $D_i$

- Start time $s_i$ tempo al quale il task comincia l'esecuzione

- Finishing time $f_i$ tempo al quale il task finisce l'esecuzione

- Response time $R_i$ differenza tra finishing time e request time

- Criticality: parametro che indica le conseguenze di non rispettare la deadline (hard, firm, soft)

- Value $v_i$ importanza relativa del task rispetto agli altri task del sistema

- Lateness: $L_i = f_i - d_i$ delay tra il completamento rispetto alla deadline. Se negativo abbiamo rispettato la deadline

- Tardiness $E_i = max(0,L_i)$  tempo in cui task sta attivo dopo la deadline

- Laxity o Slack time $X_i = d_i - a_i - C_i$ tempo massimo che il task può essere rimandato dall'attivazione per essere completato entro la deadline

Inoltre un task può essere _periodico_ o _aperiodico_

Periodico significa che il task è una sequenza infinita di attività identiche, chiamate istances o jobs, attivati costantemente ad una certa frequenza. Il tempo di attivazione della prima istanza di un task periodico è chiamato fase.

I task aperiodici consistono in una sequenza infinita di jobs, ma la loro attivazione non avviene ad una frequenza fissa. Un task  aperiodico dove i job consecutivi sono separati da un tempo minimo sono chiamati sporadici.

#### Precedence costraints

In alcune applicazioni dei task dipendono da altri task, in questi casi i task possono essere descritti tramite un DAG dove specifichiamo la precedenza dei task.

#### Resource costraints

Una risorsa può essere una struttura dati, un set di variabili, un'area di memoria, i registri di una periferica etc. Una risorsa usata da un singolo processo è privata, una risorsa usata da più processi è condivisa. 

Per mantenere la consistenza dei dati due processi non possono usare la stessa risorsa contemporaneamente. 

Si usano meccanismi di sincronizzazione come i semafori.

### Definizione dei problemi di scheduling

Abbiamo un set di task, un set di processori e un set di risorse. Possiamo specificare le relazioni di precedenza dei task, e i timing costraint associati ai task. Scheduling è il problema di assegnare i processori e le risorse ai task in modo da completare i task rispettando i costraint. È un problema NP-completo.

#### Classificazione degli algoritmi di scheduling

- Preemptive vs Non-preemptive
  
  - Negli algoritmi preemptive un task può essere interrotto in qualunque momento per eseguire un altro task
  
  - Negli algoritmi non preemptive quando un task inizia è eseguito fino alla fine

- Static vs Dynamic
  
  - Gli algoritmi statici sono quelli in cui lo scheduling è basato su parametri fissi, assegnati ai task prima della loro attivazione
  
  - Gli algoritmi dinamici sono quelli un cui le decisioni di scheduling sono basate su parametri dinamici che possono cambiare con l'evoluzione del sistema

- Off-line vs Online
  
  - Un algoritmo di scheduling è usato off-line se è eseguito su un intero task set prima che i task vengano attivati. La schedule generata in questo modo è salvata e eseguita successivamente da un dispatcher.
  
  - Un algoritmo di scheduling è usato online se le decisioni di scheduling sono prese ogni volta che un nuovo task entra nel sistema o quando un task running finisce

- Optimal vs Heuristic
  
  - Ottimo se minimizza una funzione di costo definita sul task set. Se non è definita una funzione di costo e l'unico problema è trovare una schedule fattibile un algoritmo è detto ottimale se è in grado di trovare una schedule fattibile (se questa esiste)
  
  - Euristico se è guidato da una funzione euristica nel prendere decisioni di scheduling. Un algoritmo euristico tende verso l'optimal schedule ma non garantisce che sarà trovato.

**Guarantee based algorithms**

La fattibilità di una schedule deve essere garantita in anticipo, prima di eseguire i task. In questo modo se un task critico non può essere schedulato entro la deadline il sistema ha tempo di eseguire un'azione alternativa e cercare di non rompere tutto catastroficamente.

Per garantire la fattibilità della schedule il sistema deve pianificare le azioni guardando nel futuro e assumendo il caso peggiore.

Nei sistemi statici, dove il task set è fissato e conosciuto a priori, l'attivazione dei task può essere precalcolata offline e salvata in una tabella che contiene tutti i task garantiti messi in ordine. 

Nei sistemi dinamici i task possono essere creati a runtime, quindi la garanzia deve essere fatta online ogni volta che un task è creato.

Se abbiamo un set di cui abbiamo già garantito la fattibilità dobbiamo verificare che unendo questo set con un nuovo task appena creato venga rispettata la fattibilità della schedule. In caso contrario il nuovo task viene rigettato per non mandare in overload il sistema, e per evitare il domino effect (ovvero quando viene introdotto il nuovo task questo causa che tutti gli altri task non rispettino le loro deadline).

**Best-effort algorithms**

In alcune real-time applications fallire le deadline causa solo una perdita di performance. In questi casi possiamo utilizzare un approccio best-effort.

Un algoritmo di questo tipo ci prova a fare una schedule che rispetti le deadline, ma non garantisce di trovare una schedule fattibile. 

#### Metriche per la valutazione di performance

Per valutare gli algoritmi di scheduling real time dobbiamo usare criteri diversi dai criteri standard.

- Average response time: $1/n \sum_{i=1}^n (f_i - a_i)$

- Total completion time: $\underset{i}{max}(f_i) - \underset{i}{min}(a_i)$

- Weighted sum of completion times: $\sum_{i=1}^n w_if_i $

- Maximum lateness: $\underset{i}{max}(f_i - d_i)$

- Maximum number of late tasks: $ \sum_{i=1}^n miss(f_i)$

Può essere definita una funzione di utilità dei task in funzione del tempo.

### Anomalie di scheduling

//esistono (se cambio dei costraint dei task, ad esempio riducendoli, posso rompere lo scheduling e ritrovarmi in condizioni peggiori)

## Scheduling di task aperiodici

Gli algoritmi sono definiti in base alle caratteristiche con 3 campi:

- Tipo di macchina su cui verranno schedulati i task (monoprocessore, multiprocessore, sistema distribuito...)

- Caratteristiche di task e risorse (preemptive, presenza di vincoli di precedenza, etc)

- Criterio di ottimalità (misura della performance) da seguire nella schedule

### Algoritmo di Horn

Definito su monoprocessore, è preemtive e usa L_max come misura di performance

**Teorema di Horn** Dato un set di n task indipendenti con tempi di arrivo arbitrari, un algoritmo che ad ogni istante esegue il task con la deadline assoluta più bassa tra tutti i task ready è ottimale rispetto alla minimizzazione della massima lateness.

#### EDF optimality

Se esiste una schedule fattibile per un set di task, EDF riesce a trovarla. Si può inoltre dimostrare che EDF minimizza la massima lateness. 

#### EDF Guarentee

Quando i task hanno attivazione dinamica e il tempo di arrivo non è conosciuto a priori il guarantee test deve essere fatto dinamicamente, ogni volta che un nuovo task entra nel sistema. 

Se abbiamo un set di task già guaranteed e arriva un nuovo task, per accettare il nuovo task dobbiamo garantire che l'unione con il set sia schedulabile.

Supponiamo che i task siano ordinati in modo che $J_1$ sia il task con la earliest deadline. Sia $c_i$ il tempo rimanente di esecuzione del task i-esimo nel caso peggiore. Quindi al tempo t, il tempo di fine nel caso peggiore del task i-esimo si può calcolare come:

$$
f_i = \sum_{k=1}^{i} c_k(t)
$$

Quindi la schedulabilità è garantita dalle seguenti condizioni

$$
\forall i = 1...n \sum_{k=1}^i c_k(t) \le d_i
$$

Notando che $f_i = f_{i-i} + c_i(t)$ il dynamic guarantee test può essere effettuato in $\Omicron (n)$

### Scheduling con costraint di precedenza

Trovare una schedule ottimale per un set di task con costraint di precedenza è in generale NP-hard. Ci sono però algoritmi ottimali in grado di risolvere il problema in tempo polinomiale se possiamo assumere dei fatti sui task. 

#### EDF con costraint di precedenza

Il problema di schedulare un set di task con costraint di precedenza e attivazioni dinamiche può essere risolto in tempo polinomiale solo se i task sono preemptable. Possiamo modificare il set di task dipendenti in un nuovo set di task indipendenti modificando adeguatamente i parametri di timing dei task. Dopo di che possiamo schedulare il nuovo set con EDF. Le trasformazioni assicurano che il set iniziale sia schedulabile e che i costraint siano rispettati se e solo se il nuovo set è schedulabile. In pratica, i release times e le deadline sono modificate in modo che ogni task non può iniziare prima del suo predecessore e non può preemptare i suoi successori.

**Modifiche ai release times**

La regola per modificare i tempi di release è basata sulla seguente osservazione.

Dati due task a e b, tali che a è immediato predecessore di b, allora in ogni schedule valida che rispetta i costraint di precedenza devono essere soddisfatte le seguenti condizioni

$$
s_b \ge r_b \\
s_b \ge r_a + C_a


$$

Possiamo dire che il release time di b è uguale a $max(r_b, r_a + C_a)$

L'algoritmo che modifica i tempi di release può essere implementato in $\Omicron (n^2)$ ed è descritto dai seguenti passi:

1. Per ogni nodo iniziale del grafo delle precedenze $r^*_i = r_i$

2. Selezioniamo un task $J_i$ tale che il suo release time non è stato modificato ma il release time dei suoi immediati predecessori è stato modificato. Se non esiste esci.

3. Set $r^*_i = max(r_i, max(r^*_h + C_h : J_h \rightarrow J_i))$

4. Torna allo step 2

**Modifiche alle deadline**

La regola per modificare le deadline è basata sulla seguente osservazione Dati due task $J_a, J_b \space con \space J_a \rightarrow J_b $ devono essere soddisfatte le seguenti condizioni:

$$
f_a \le d_a \\
f_a \le d_b - C_b
$$

La deadline $d_a$ può essere quindi sostituita dal minimo tra i due

$$
d^*_a = min (d_a, d_b - C_b)
$$

L'algoritmo che modifica le deadline può essere implementato in $\Omicron  (n^2)$ ed p espresso dai seguenti step:

1. Per ogni nodo terminale del grafo delle precedenze $d^*_i = d_i$

2. Selezioniamo un task $J_i$ tale che la sua deadline non è stata modificata ma la deadline dei  suoi immediati successori sia stata modificata. Se il task non esiste esci

3. Set $d^*_i = min(d_i, min(d^*_k - C_k : J_i \rightarrow J_k))$

4. Ritorna allo step 2.

## Scheduling di task periodici

In un'applicazione real time esistono spesso task da ripetere ad una data frequenza. Bisogna garantire che ogni istanza periodica sia attivata regolarmente alla frequenza giusta e completata entro la deadline.

Introduciamo 3 algoritmi: Rate Monotonic, EDF, e Deadline Monotonic. 

Introduciamo la seguente notazione:

- $\Gamma$ denota il set di task periodici

- $\tau_i$ denota un task periodico generico

- $\tau_{i,j}$ denota la j-esima istanza del task i-esimo

- $r_{i,j}$ è il release time della j-esima istanza del task i-esimo

- $\Phi_i$ denota la fase del task i-esimo. è la release time della prima istanza del task i-esimo

- $D_i$ è la deadline relativa del task i-esimo

- $d_{i,j}$ denota la deadline assoluta della j-esima istanza del task i-esimo $d_{i,j} = \Phi_i + (j-1)T_i + D_i$

- $s_{i,j}$ è lo start time della j-esima istanza del task i-esimo

- $f_{i,j}$ è il finishing time della j-esima istanza del task i-esimo

Per semplificare l'analisi di schedulabilità, assumiamo le seguenti ipotesi sui task:

1. Le istanze di un task sono attivate regolarmente ad una frequenza costante. L'intervallo tra due attivazioni consecutive è il periodo del task, chiamiamolo $T_i$.

2. Tutte le istanze del task hanno lo stesso tempo worst-case di esecuzione $C_i$

3. Tutte le istanze del task hanno la stessa deadline relativa $D_i$, che è uguale al periodo del task

4. Tutti i task del set sono indipendenti, non ci sono costraint di precedenza tra i task e non ci sono risorse condivise

5. Nessun task può sospendere se stesso

6. Tutti i task sono released appena arrivano

7. Assumiamo che tutti gli overhead del kernel siano 0

Le assunzioni 1 e 2 non sono restrittive in quanto in molte applicazioni funzionano esattamente così. Le assunzioni 3 e 4 potrebbero invece essere troppo strette in applicazioni pratiche.

Denotiamo un set di task periodici come:

$$
\Gamma = \{ \tau_i(\Phi_i, T_i, C_i), i =1, ...,n\}
$$

I release time e le deadline assolute di un istanza k-esima possono essere calcolate come:

$$
r_{i,k} = \Phi_i + (k-i)T_i \\
d_{i,k} = r_{i,k} + T_i = \Phi_i + kT_i
$$

Altri parametri definiti sui task periodici sono definiti:

- **Hyperperiod**: minimo intervallo di tempo dopo cui la schedule si ripete. Se $H$ è la lunghezza di questo intervallo allora la schedule in $[0,H]$ + la stessa che c'è in ...... BOH.
  Per un set di task periodici attivati allo stesso tempo 0, l'iperperiodo è dato dal minimo comune multiplo dei periodi

- **Job response time** è il tempo (misurato dal release time) nel quale il job è terminato $R_{i,k} = f_{i,k} - r_{i,k}$

- **Task response time** è il massimo tempo di risposta tra tutti i job di un task $R_i = \underset{k}{max}R_{i,k}$

- **Critical istant** di un task è il tempo di arrivo che produce la più grande response time di un task

- **Critical time zone** di un task è l'intervallo tra l'istante critico e il response time della corrispondente richiesta del task

- **Relative Start Time Jitter** di un task è la massima deviazione tra la start di due istanze consecutive 
  $ RRJ_i = \underset{k}{max} |(s_{i,k}-r_{i,k}) - (s_{i, k-i} - r_{i,k-1})| $

- **Absolute Start Time Jitter** di un task è la massima deviazione tra la start di tutte le istanze 
  $ARJ_i = \underset{k}{max}(s_{i,k}-r_{i,k}) - \underset{k}{min}(s_{i,k}-r_{i,k})$

- **Relative Finishing Jitter** di un task è la deviazione massima tra la fine di due istanze consecutive
  $RFJ_i = \underset{k}{max} |(f_{i,k}-r_{i,k}) - (f_{i, k-i} - r_{i,k-1})|$

- **Absolute Finishing Jitter** di un task è la massima deviazione di fine tra tute le istanze
  $AFJ_i = \underset{k}{max}(f_{i,k}-r_{i,k}) - \underset{k}{min}(f_{i,k}-r_{i,k})$

Un task periodico è detto fattibile se tutte le sue istanze finiscono entro le loro deadline. Un set è detto schedulabile (o fattibile) se tutti i task nel set sono fattibili.

### Processor utilization Factor

Dato un set di task periodici, il fattore di utilizzo del processore è definito come

$$
U = \sum^n_{i=1} \frac{C_i}{T_i}
$$

Ovvero quanto la cpu è occupata nell'eseguire il set di task periodici. 

Esiste un limite di U massimo sopra al quale il set di task non è schedulabile. Questo limite dipende dal set di task e dall'algoritmo usato per schedulare i task.

Sia $U_{ub}(\Gamma, A)$ l'upper bound del processor utilization factor per un set di task dato l'algoritmo A. Quando $U = U_{ub}(\Gamma, A)$ si dice che il set di task sta utilizzando completamente il processore. In questa situazione il set è schedulabile secondo A ma un incremento dei tempi di computazione in un qualsiasi task renderebbe il set non fattibile.

Per un dato algoritmo A, il least upper bound $U_{lub}(A)$ del fattore di utilizzo del processore è il minimo tra i fattori di utilizzazione si task set che usano completamente il processore

$$
U_{lub} = \underset{\Gamma}{min}U_{ub}(\Gamma, A)
$$

Dato un set di task se il suo fattore di utilizzazione del processore è minore o uguale al least upper bound allora è schedulabile dall'algoritmo, invece se U è maggiore del bound e minore di 1 è schedulabile solo se i periodi dei task sono compatibili. Se U è maggiore di 1 il task set non è schedulabile da nessun algoritmo. Per mostrare questo risultato diciamo che $H$ è l'iperperiodo del task set. Se U>1 abbiamo anche che UH>H, che può essere scritto come

$$
\sum^n_{i=1}\frac{H}{T_i}C_i>H
$$

Il fattore $H/T_i$ rappresenta il numero (intero) di volte che il task i-esimo è eseguito nell'iperperiodo, mentre la quantità $(H/T_i)C_i$ è il tempo totale di computazione richiesto dal task i-esimo nell'iperperiodo. Quindi la somma a sinistra rappresenta il totale della domanda di computazione richiesta dal task set nell'iperperiodo. Ovviamente se la domanda supera il tempo del processore disponibile non esiste nessuna schedule fattibile per il task set.

### Timeline scheduling

È uno dei metodi più usati per gestire i task periodici nei sistemi di difesa militare e nel controllo del traffico. Il metodo consiste nel dividere l'asse temporale in slot di uguale lunghezza, nei quali uno o più task possono essere allocati per l'esecuzione, in modo da rispettare le frequenze derivate dai requisiti dell'applicazione. Un timer sincronizza l'attivazione dei task all'inizio di ogni time slot. 

Abbiamo un Minor Cycle, che è la durata del time slot ed è il massimo comun divisore tra i periodi dei task. L'intervallo a cui si ripete la schedule è l'iperperiodo o Major Cycle, che è uguale a minimo comune multiplo tra i periodi.

Per verificare la fattibilità consideriamo i tempi di esecuzione nel caso peggiore e verifichiamo che rientrino nel time slot.

Il maggior vantaggio di questo tipo di scheduling è la semplicità: esso può essere implementato con un timer che genera un interrupt alla frequenza del time slot e chiamando i task nell'ordine dato dal major cycle. Non ci sono context switch quindi non abbiamo overhead. 

Abbiamo alcuni problemi: fragilità in caso di overload, per effettuare dei cambiamenti nei task bisogna rifare tutto, non si riescono a gestire adeguatamente i task aperiodici.

### Rate Monotonic scheduling

Questo algoritmo di scheduling assegna le priorità dei task in base alla loro frequenza. Task con periodo più breve avranno priorità maggiore. Visto che i periodi sono costanti RM è un fixed-priority assignment. RM è intrinsecamente preemptive: il task in esecuzione viene preemptato se arriva un task con periodo minore.

È stato dimostrato che RM è ottimale, nel senso che se un task set è schedulabile da un algoritmo a priorità fissa, allora è anche schedulabile da RM.

Calcolo del least upper bound per n task

$$
U_{lub} = n(2^{1/n}-1)
$$

**Hyperbolic bound per RM**

La fattibilità di RM per un set di task è verificata nel seguente modo.

Sia $\Gamma = \{\tau_1,...,\tau_n\}$ un set di $n$ task periodici, dove ogni task è caratterizzato da un utilizzo del processore pari a $U_i$. Allora il set è schedulabile con RM se

$$
\prod^n_{i=1} (U_i + 1) \le 2
$$

L'hyperbolic bound offre un margine maggiore, nel caso devo vedere la fattibilità di un task con RM uso questo.

### Earliest Deadline First

EDF è un algoritmo di scheduling dinamico che seleziona il task in base alle deadline assolute: il task con la deadline assoluta minore avrà una priorità maggiore. Possiamo esprimere la deadline assoluta della j-esima istanza di un task come

$$
d_{i,j} = \Phi_i + (j-1)T_i + D_i
$$

EDF è tipicamente eseguito in modalità preemptive.
EDF non fa alcuna assunzione sulla periodicità dei task, può essere usato quindi per schedulare sia task periodici che aperiodici.

#### Analisi di schedulabilità

Un set di task è schedulabile con EDF se e solo se

$$
\sum_{i=1}^n \frac{C_i}{T_i} \le 1
$$

### Deadline Monotonic

In DM indeboliamo l'assunzione che "il periodo è uguale alla deadline".

È un'estensione di RM dove le deadline dei task sono minori o uguali al periodo.

Ogni task periodico è caratterizzato da 4 parametri:

- Una fase $\Phi$

- Un tempo di computazione nel caso peggiore $C_i$ (costante per ogni istanza del task)

- Una deadline relativa $D_i$ (costante per ogni istanza)

- Un periodo $T_i$

Questi parametri sono legati dalle seguenti relazioni:

$$
\begin{cases}
C_i \le D_i \le T_i \\
r_{i,k} = \Phi_i + (k-1)T_i \\
d_{i,k} = r_{i,k} + D_i
\end{cases}
$$

Secondo DM ad ogni task è associata una priorità fissa $P_i$ inversamente proporzionale alla sua deadline $D_i$. Quindi ad ogni istante il task con la minore relative deadline è eseguito. Visto che le relative deadlines sono costanti, DM assegna le priorità staticamente. Come RM, DM è usato con preemptiveness.

DM è ottimale, nel senso che se un task set è schedulabilie da un algoritmo con assegnazione fissa di priorità allora esso è schedulabile anche con DM.

#### Analisi di schedulabilità

La fattibilità di un task set con costrained deadlines potrebbe essere garantita usando il test di utilizzo del processore, riducendo i periodi dei task alle loro deadline relative

$$
\sum_{i=1}^n \frac{C_i}{D_i} \le n(2^{1/n} - 1)
$$

Tuttavia questo test sarebbe piuttosto pessimistico, in quanto il carico di lavoro del processore sarebbe sovrastimato. Un test meno pessimistico può essere fatto notando che:

- Il caso peggiore di richiesta del processore avviene quando tutti i task vengono rilasciati in contemporanea, al loro istante critico

- Per ogni task, la somma del processing time e l'interferenza (preemption) imposta dagli altri task con priorità maggiore deve essere minore uguale della deadline relativa del task.

Assumendo che i task siano ordinati per deadline relative in ordine crescente, possiamo esprimere questo test come:

$$
\forall i : 1 \le i \le n \quad C_i + I_i \le D_i
$$

dove $I_i$ è la misura dell'interferenza relativa al task i-esimo, e può essere calcolata come la somma del processing time di tutti i task a priorità maggiore rilasciati prima di $D_i$:

$$
I_i = \sum_{j=1}^{i-1} ceiling(\frac{D_i}{T_j})C_j
$$

Notiamo che questo test è sufficiente ma non necessario per garantire la schedulabilità del task set. 

Per trovare un test necessario e sufficiente per DM bisogna trovare l'interleaving esatto per ogni processo. Questa procedura è molto costosa. Esiste la Response Time Analysis che sarebbe necessaria e sufficiente ma noi non la facciamo perchè siamo bimbi speciali.

### Comparazione tra RM e EDF

In conclusione, il problema di scheduling di task periodici indipendenti e preemptable è stato risolto sia con assegnazione di priorità fissa che dinamica.

Usare priorità fissa è più semplice da implementare. Se implementiamo la coda dei task ready con una multilevel queue con P livelli di priorità, inserimento e estrazione dei task è fatta in $\Omicron(1)$. In uno scheduler guidato dalle deadline invece la migliore soluzione per implementare la coda dei task ready è un heap, e gestire i task ha una complessità pari a $\Omicron(\log n)$

Se lasciamo da parte i problemi di implementazione, che diventano rilevanti solo se abbiamo centinaia di task o se abbiamo processori lenti, lo scheduling con priorità dinamica ha molti vantaggi rispetto allo scheduling con priorità fissa.

Per l'analisi di schedulabilita RM richiede una complessità pseudo-polinomiale, mentre per EDF può essere fatta in $\Omicron (n)$. Nel caso generale in cui le deadlines sono minori o uguali al periodo la schedulabilità diventa pseudopolinomiale per entrambi. Sotto priorità fissa la fattibilità del task set può essere testata usano la response time analysis mentre sotto priorità dinamica può essere testata usando il criterio di richiesta del processore.

EDF può utilizzare completamente il processore, mentre RM garantisce la fattibilità del task set con utilizzo minore del 69% nel caso peggiore. Nel caso medio, uno studio statistico ha mostrato che per un task set generato random RM riesce a schedulare con un utilizzazione del processore di circa l'88%. 

EDF nonostante i tempi di computazione extra per aggiornare le deadline assolute introduce meno overhead di RM quando prendiamo in considerazione i context switches. Infatti in RM avvengono molti più context switch che in EDF.

EDF ha anche una proprietà interessante: durante overloads permanenti fa automaticamente un rescaling dei period, in modo che i task si comportano come se stessero venendo eseguiti ad una frequenza minore.

Nel caso di scheduling a priorità fissa un overload permanente causa un blocco totale dei task a priorità bassa.

Inoltre, lo scheduling dinamico risponde meglio se abbiamo anche task aperiodici. Questa proprietà viene dal maggiore bound di utilizzo del processore di EDF. In EDF i task periodici utilizzano $U_p$ percentuale del processore, lasciando $1-U_p$ per essere allocata per l'esecuzione dei task aperiodici.

## Resource access protocols

Quando si hanno risorse condivise si possono usare i semafori per gestire la codivisoone di queste risorse tra più task: quando un task deve utilizzare una risorsa chiama la funzione wait(s), in attesa che la risorsa sia libera. Entra quindi in una sezione critica nella quale utlizza la risorsa e quella risorsa (mentre ci troviamo all'interno di questa sezione critica) non può essere utlizzata da altri task (che eventualmente resteranno in wait). Alla fine della sezione critica si esegue una signal(s) per segnalare ai task in attesa che la risorsa è stata liberata.

Quando nei sistemi monoprocessore più task concorrenti usano risorse condivise in exclusive mode possono esserci problemi.  

### Problema dell'inversione di priorità

Consideriamo due task che condividono una risorsa esclusiva. Per garantire la mutua esclusione definiamo delle sezioni critiche. Se un semaforo binario è ussato per questo scopo ogni sezione critica inizia con wait e finisce con signal.

Se la preemption è permessa e il task 1 ha una priorità maggiore del task 2 allora il task 1 può ritrovarsi bloccato, nel caso che il secondo task sia stato attivato per primo e abbia bloccato la risorsa condivisa.  Il task 1 dovrà necessariamente aspettare un tempo pari al tempo della sezione critica del task 2.

Tuttavia, nel caso generale, il blocking time di un task su una risorsa occupata non può essere limitato dalla durata della sezione critica eseguita dal task di priorità minore. Può succedere che un task di priorità bassa stia eseguendo una sezione critica e venga preemptato da un task di priorità "media", che non agisce sulla risorsa condivisa ma vada comunque a bloccare un task di priorità alta che era bloccato a causa del fatto che il task a priorità bassa fosse in una sezione critica.

Quando un task di priorità alta si trova ad aspettare l'esecuzione di task a priorità più bassa (al di là delle sezioni critiche) abbiamo un inversione delle priorità.

Ci sono più approcci a questo problema, sia sotto scheduling a priorità fissa che scheduling a priorità dinamica. Nei metodi con priorità fissa lo scheduling consiste nell'alzare il livello di priorità di un task quando accede ad una risorsa condivisa, secondo un protocollo per entrare e uscire dalle sezioni critiche.

Nei metodi sviluppati sotto EDF modifichiamo i parametri basati sulle deadline relative dei task.

Ci sono i seguenti protocolli di accesso alle risorse:

1. Non-Preemptive protocol

2. Highest Locker Priority

3. Priority Inheritance Protocol

4. Priority Ceiling Protocol

5. Stack Resource Policy
