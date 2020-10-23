# Controllo

## Controllo motori:

Attuatori: due tipi di servomotori _elettrici_ e _idraulici_.

### Attuazione di giunti

Il movimnto di un giunto è realizzato da un sistema di attuazione che consiste generalmente di:

- power supply

- power amplifier (o modulator)

- servomotore

- trasmissione

#### Trasmissione

L'esercuzione dei movimenti di un manipolatore richiede poca velocità e tanta coppia. In genere i servomotori forniscono alte velocità e poca coppia. Si aggiunge quindi una trasmissione (riduzione/gear). La scelta della trasmissione dipende dal tipo di movimento desiderato: una trasmissione puù trasformare l'output di un motore sia per quanto riguarda velocità e coppia, sia per il tipo di movimento (traslazione o rotazione).

In alcuni casi non si usano trasmissioni, questo si chiama _direct drive_.

#### Servomotori

3 tipi di motori:

- Pneumatici, che utilizzano l'energia fornita da un compressore e la trasformano in energia meccanica con pistoni e turbine

- Idraudlici, che trasformano l'energia idraulica in energia meccanica con pompe.

- Elettrici, che vabè ci siamo capiti.

Requirements di un motore tipici:

- bassa inerzia e alta power-to-weight ratio

- possibilità di overload e delivery of impulse torques

- Capacità di sviluppare alte accelerazioni

- Ampio range di velocità

- Accuratezza della posizione

- Low torque ripple

I motori più usati sono quelli elettrici. In particolare i motori DC brushed e i motori DC brushless.

Brushless +costosi, +performance, +velocità, si rovinano meno. Disperdono calore più velocemente, sono +compatti. Insomma, l'unico motivo per scegliere un brushed è il costo.

Esistono anche gli _stepper_.

Differenze varie ed eventuali fra elettrici e idraulici TODO non ho voglia

#### Power amplifiers (o modulatori)

Modulano il segnale di controllo per fornire la giusta potenza ai servomotori. Vedi anche ponte H.

#### Power supply

Per motori elettrici trasformatore e  uncontrolled bridge rectifier. 

Per motori idraulici succedono cose, dobbiamo davvero saperle?

## Controllo manipolatore

Siciliano cap. 8: leggere, senza troppa attenzione alle formule e schemi, fino alla sezione
8.3 inclusa, in particolare la sottosezione 8.3.1.

Due aspetti trattati separatamente: controllo del movimento nello spazio libero e controllo dell'interazione con l'ambiente. Sono presentate tecniche di controllo nello spazio dei giunti. Si possono distinguere in schemi decentralizzati, in cui ogni giunto è controllato in modo indipendente dagli altri giunti, e schemi centralizzati, dove l'effetto delle interazioni tra i giunti vengono considerate

### Problema del controllo

il driving system dei giunti influenza il tipo di controllo usato. La presenza di riduzioni attaccate ai motori tende a linearizzare le dinamiche del sistema, e quindi decouple i giunti. Il costo è l'introdizione di attrito, elasticita e backlash che potrebbe limitare la performance del sistema. Un robot attuato con direct drive invece non ha questi costi ma il sistema sarà non lineare e saranno rilevanti i couplings tra i giunti. 

È bene ricordare che la specificazione dei task è specificata nell'operational space, mentre il controllo delle azione avviene nel joint space. Abbiamo quindi due tipi di schemi di controllo generale: _joint space control_ e _operational space control_.

Il controllo nello spazio dei giunti è articolato in due sottoprolemi: prima si risolvono le cinematiche inverse per trasformare il task nel movimento del giunto. Viene poi progettato uno schema di controllo per eseguire il movimento. In questo modo però non è presente un feedback sul mondo.

Il contollo nello spazio operazionale segue un approccio che richiede una complessità algoritmica maggiore. La cinematica inversa è inserita all'interno del loop di controllo retroazionato. Si agisce direttamente sulle variabili dello spazio operazionale.

### Controllo nello spazio dei giunti

Ogni giunto è controllato indipendentemente dagli altri secondo uno schema di controllo decentralizzato.

Può anche esserci un controllo sulla coppia.

### Controllo decentralizzato

La strategia più semplice tratta un manipolatore come formato da n sistemi indipendenti (n giunti) e controlla ogni giunto come un sistema siso. Gli effetti di coupling tra i giunti sono trattati come disturbi.

Più soluzioni che usano un numero diverso di feedback:

- Position feedback

- Position and velocity feedback

- Position, velocity and accelleration feedback

Bisogna tenere in cosiderazione tutti i giunti per fare un controllo decente: bisogna evitare sforzi eccessivi ai giunti e coordinarli in modo che tutti raggiungano il proprio setpoint insieme.


