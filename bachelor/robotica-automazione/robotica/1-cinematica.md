# Cinematica

## concetti base vari ed eventuali

**pose di un corpo rigido** definita da posizione e orientamento

**trasformazione rispetto a frame corrente** $T^0_2 = T^0_1*T^1_2$

**trasformazione rispetto a mondo** $T^0_2 = T^1_2 * T^0_1$

**angoli di eulero zyx** roll pitch yaw, rispetto a world

**angoli eulero zyz** z y' z'', rispetto a frame corrente

**quaternioni** descrivono orientamento con 4 parametri

**trasformazioni omogenee**

## Cinematica diretta

Un braccio è fatto da link connessi da giunti. I giunti possono essere rotativi o prismatici. I DoF (degrees of freedom) determinano la posture del robot. Tipicamente a ogni giunto è associato un DoF. Ad ogni link è associato un frame

### Convenzioni DH

4 parametri $(a,d, alpha, theta)$, che descrivono la matrice che effettua la trasformazione tra il frame del link i-1 al link i. 

- a traslazione su x

- d traslazione su z

- alpha rotazione su x

- theta rotazione su z

### Operational space

(anche detto spazio cartesiano). spazio nel quale viene specificata la pose dell'end-effector.

##### Joint space

spazio in cui sono definite le variabili dei giunti.

##### Workspace

regione in cui è possibile far andare l'end effector. Anche detto spazio raggiungibile.

**Spazio raggiungibile con destrezza**: sottoinsieme del workspace, raggiungibile dall'end-effector con più orientamenti.

### Accuratezza e ripetibilità

Info reperibili su datasheet del robot.

##### Accuratezza

Deviazione tra la posizione raggiunta dal braccio e la posizione  calcolata dalla cinematica diretta. La differenza è dovuta a tolleranze meccaniche. Tipicamente <1mm e dipende da dimensioni e struttura del manipolatore. Varia anche in base alla posizione dell'end-effector.

##### Ripetibilità

Misura della capacità di ritornare a una posizione precedente. Dipende anche da trasduttori e controllori, e il suo valore è tipicamente inferiore di quello dell'accuratezza.

### Ridondanza cinematica

Un manipolatore è definito ridondante se ha almeno un DoF maggiore delle variabili necessarie per un determinato task.

Un manipolatore è intrinsecamente ridondante se le dimensioni del workspace sono minori delle dimensioni del joint space.

Vantaggi di un manipolatore ridondante: destrezza, evita ostacoli, supera limiti meccanici dei joint.

### Calibrazione cinematica

Serve per trovare stime accurate dei parametri DH. 

È un problema non lineare, va iterato finchè non converge. 

È fatta dal produttore per garantire l'accuratezza del datasheet.

Un altro tipo di calibrazione deve essere fatta dall'utente all'inizio di ogni operazione. Si chiama homing, ovvero si fa tornare il robot a una posizione predefinita e si inizializzano i trasduttori.

## Cinematica inversa

Si tratta di calcolare joint variables da pose dell'end effector.

È difficile perchè:

- le equazioni non sono lineari

- possono esistere più soluzioni

- possono esistere infinite soluzioni

- possono non esistere soluzioni

L'esistenza di soluzioni è garantita solo nello spazio di lavoro con destrezza.

Nel caso di 3 assi concorrenti in un punto possiamo separare il problema della posizione dal problema dell'orientamento (decoupling).

Step:

- Computare la posizione del polso pw(q1,q2,q3)

- Risolvere la cinematica inversa per (q1,q2,q3)

- Computare la matrice $R^0_3(q1,q2,q3)$

- Computare $R^3_6(th4,th5,th5) = R^{0T}_3R$

- Risolavere la cinematica inversa per l'orientamento

Quindi, ad esempio, nel caso di bracci con polso sferico possiamo calcolare la posizione del braccio, e successivamente l'orientamento del polso.

Nel caso di braccio antropomorfo per ogni pose dell'end-effector esistono 4 posture del manipolatore.
