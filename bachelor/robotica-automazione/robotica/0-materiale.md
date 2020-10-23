# Materiale da studiare scritto robotica

## Materiale cinematica

- sezione 2.8, saltando la parte 2.8.3 sulle catene cinematiche chiuse. La figura 2.16 va interiorizzata perfettamente (notare che αi è attorno ad xi).

- sezione 2.9, saltando sia la parte 2.9.2 su "parallelogram arm", che la parte 2.9.6 su "Stanford manipulator".

- sezione 2.10, in particolare i concetti di spazio operativo (cartesiano) e dei giunti

- la sottosezione 2.10.1 "workspace" ed i concetti di spazio di lavoro "raggiungibile", "raggiungibile con destrezza", accuratezza e ripetibilità;

- la sottosezione 2.10.2 "kinematic redundancy" ed il concetto di ridondanza cinematica (relativa ad un task) e della utilità pratica che può venire dall'avere della ridondanza cinematica in un task;

- la sottosezione 2.11 "kinematic calibration", in particolare fino al punto in cui si spiega come il problema sia un problema di ottimizzazione globale non lineare e l'ultimo paragrafo sul fatto che la calibrazione cinematica sia una attività del produttore del braccio robotico, mentre lo "homing" sia invece da svolgersi ad ogni accensione del robot (torneremo comunque sul motivo alla base della procedura di homing quando parleremo di sensori di posizione angolare incrementali).

- sezione 2.12 cinematica inversa, sono poco importanti i dettagli delle risoluzioni ed entrambe le sezioni 2.12.1 e 2.12.3

## Materiale controllo motori

- capitolo 5, breve introduzione e tutta la sezione 5.1.

Un paio di note in relazione al materiale per giovedì:

Il termine "POWER AMPLIFIER" nella Figura 5.1 non mi soddisfa. Forse "POWER MODULATOR" potrebbe essere un termine più adeguato: infatti la potenza che fa muovere il motore, spostando il carico, non è "amplificata" nel blocco fisico corrispondente a quello che in Figura 5.1 viene chiamato "POWER AMPLIFIER", viene invece "modulata", ma comunque viene fornita tutta dal "POWER SUPPLY".
Il testo non dice niente in relazione al cosiddetto H-Bridge ovvero l'insieme di componenti elettronici usati per alimentare i motori DC parzializzando la potenza prelevata dal "POWER SUPPLY" mediante PWM ed in modo tale poter anche invertire il senso di rotazione. Ho per questo aggiunto un breve lista di link subito dopo il link al capitolo 5 del libro di testo. Quello relativo agli spikes non è obbligatorio, gli altri dicono più o meno le stesse cose, con parole e grafica leggermente diverse.

## Materiale da studiare su controllo del manipolatore.

- Siciliano cap. 8: leggere, senza troppa attenzione alle formule e schemi, fino alla sezione 8.3 inclusa, in particolare la sottosezione 8.3.1.

## Materiale da studiare su pianificazione / interpolazione della traiettoria.

- Siciliano: cap 4, in particolare: 4.0, 4.1, 4.2, in particolare:
  - 4.2.1 tutto, ma il primo approccio "parabolic velocity profile" solo leggere velocemente mentre il secondo approccio "trapezoidal velocity profile" fare bene, in particolare la figura 4.2 va capita bene;
  - 4.2.2 fino a "Interpolating polynomials with imposed velocities at path points" escluso; 4.3: solo 4.3.0
- Craig: cap. 7 (il "piatto forte" sono le 2 sezioni "Cubic polynomials" e "Linear function with parabolic blends"), tranne:
  la sezione "Cubic polynomials for a path with via points" (notare che la Fig. 7.3 fa parte della precedente sezione "Cubic polynomials"),
  la sezione "Linear function with parabolic blends for a path with via points" (notare che la Fig. 7.8 fa parte della precedente sezione "Linear function with parabolic blends"), la sezione 7.7, 7.8 e 7.9.

##### Note.

sul Craig si usa il termine "station" per indicare il frame che sul Sciliano è chiamato "base";
sul Craig si usa il termine "Linear function with parabolic blends" per fare riferimento allo stesso approccio che sul Siciliano è chiamato "trapezoidal velocity profile".
in generale, trovo che in entrambi i testi non sia abbastanza rese esplicito che in assenza di una interpolazione di traiettoria, per un sistema di controllo a giunti indipendenti, si acrebbe un movimento, non coordinato, in cui ciascun giunto tenterebbe di raggiungere il suo set point e questo comporterebbe non solo che qualche giunto terminerebbe prima il suo moto rispetto ad altri (cosa che su un braccio non cartesiano porta ad un movimento che si allontana dalla linea congiungente la pose di arrivo a quella di partenza), ma soprattutto il movimento dei giunti più esterni lungo la catena cinematica si trasformano in carichi molto elevati, usuranti, sui giunti più vicini alla base; una situazione da evitare!
Inoltre, altro aspetto detto solo in modo implicito, se il programmatore non ha deciso anche il tempo entro cui completare il movimento, il primo passo è quello di identificare il giunto più lento, quello che pur raggiungendo la velocità massima, impiega più tempo a raggiungere il suo setpoint di posizione. Gli altri giunti, che potrebbero tutti essere più veloci ovvero raggiungere il loro setpoint in meno tmepo, verrano opportunamente rallentati, al limite (anche riducendo la accelerazione) non raggiungendo nemmeno la velocità di crociera ovvero seguendo un profilo di velocità che si riduce ad essere triangolare.
Con la notazione X.0 indico la parte di testo iniziale del capitolo X, prima della sezione X.1.

4.2.2 "non ho capito"
4.3 boh

## Materiale sensoristica

- Siciliano sezione 5.3: tutto tranne:
  - resolvers,
  - AC tachometer solo le prime 2 righe
- Siciliano sezione 5.4: tutto tranne:
  - strain gauge
  - AC tachometer solo le prime 2 righe,

##### Note.

- In relazione agli encoder incrementali: sui datasheet trovate usualmente il termine "channel" per indicare una connessione elettrica in uscita da un encoder che misura le transizioni su una "traccia" (track è il termine usato sul testo); il testo quindi si riferisce solo a come è fatto il "disco", non includendo l'elettronica di lettura del dato sul disco.
- Ci possono essere sistemi ottici a fotocellula, sia a riflessione che passanti (ne riparliamo quando tratteremo le fotocellule), sistemi che percepiscono la presenza / assenza di materiale ferromagnetico, etc.
- l testo, quando parla di encoder incrementali, dice, correttamente, che la presenza sulle 2 tracce di tacche "in mutua quadratura" consente di determinare la direzione di movimento. Non dice però, anche se forse a qualcuno potrebbe apparire ovvio, che "in mutua quadratura" significa che, leggendo otticamente le tacche ed ottenendo un segnale elettrico, quando si è arrivati a metà del periodo del segnale elettrico corrispondente ad una tacca / non-tacca su una traccia, si ha che l'altra commuta.
- La presenza di segnali in quadratura consente di determinare la direzione di movimento, verificando se arriva prima il "livello tacca" di una traccia o dell'altra; questo è detto nel libro. Il libro non dice invece che, al posto di contare i livelli si possono contare i fronti e quindi si può ottenere, oltre alla determinazione della direzione, anche un quadruplicamento della risoluzione dell'encoder.
- Per contare i fronti è necessaria un piccola rete logica anteposta ad un timer; questa si trova spesso già disponibile sui microprocessori dedicati al controllo motori, all'interno delle periferiche (usualmente timer) per la gestione degli encoder.
- Le 2 righe dedicate alla misura di velocità ottenuta a partire dalla misura di posizione generata da un encoder sono un po' troppo sintetiche: l'approccio basato sulla misura della "frequenza del treno di impulsi", di fatto consistente nella misura del numero di cicli osservati, è adatta all'esecuzione di misure quando la velocità di rotazione è elevata perché le letture di posizione ottenute dall'encoder sono soggette ad un errore di quantizzazione piccolo, relativamente allo spazio percorso tra una lettura e la successiva. Al contrario, quando lo spazio percorso è piccolo, l'errore di quantizzazione diviene preponderante; in quest'ultimo caso si preferisce misurare il tempo che intercorre tra fronti consecutivi.
- Parlando di sonar, il testo fa riferimento all'interazione tra l'onda elastica e la superficie contro cui l'onda elastica impatta. In particolare, parla della interazione assorbente che ha luogo quando le dimensioni delle irregolarità presenti sulla superficie "risuonano" (sono simili o multipli - sottomultipli) con la lunghezze d'onda dell'onda elastica (le lunghezze d'onda, se si tratta di un treno multi-frequenza di onde). Questo è incompleto: l'intensità dell'assorbimento dipende anche dalla spaziatura tra molecolare / atomica / agglomerati di materia all'interno del corpo sulla cui superficie l'onda incide. Aneddoto sulla mammella di mucca imbalsamata ed invece il guanto per lavare i piatti pieno d'acqua.
- Parlando di Laser range finder (LRF), il testo li nomina solo come "Lasers"; questo non è corretto, il laser è il fascio emesso, tutto l'apparato. includendo anche il laser, che consente di effettuare misure di distanza, si chiama laser range finder.
- Il testo non sottolinea in modo adeguato il fatto che il fascio ottenuto con un laser sia, per quanto non perfettamente "parallelo", molto più concentrato (con una apertura molto inferiore; apertura = l'angolo in cui ha luogo la gran parte della distribuzione dell'energia attorno alla direzione di massima intensità). Questo ha un ruolo importante nel campionamento spaziale della scena; con un sonar si hanno aperture dell'ordine dei 30º, con un LRF anche inferiori al grado.
- Un altro, più grave, errore del testo è che introduce i 2 approcci alla misura di distanza (tempo di volo e triangolazione), come 2 modi in cui si possono usare i laser per misurare distanze. Questo è un errore: anche i sonar sono dispositivi per la misura della distanza basati sull'approccio "ToF", l'uso di una coppia di telecamere "normali" (vedremo che ci sono anche "telecamere non-normali, es. camere 3D), consente di misurare distanze con l'approccio della triangolazione. Questa differenza è importante perché cambia la distribuzione degli errori. Di questo parliamo nell'incontro interattivo.
- Quando il testo nomina le "limitazioni sulla accuratezza delle misure dei LRFs", parla solo delle misure fatte emettendo singoli impulsi, si dice in gergo "lavorando in banda base", ma i LRF, proprio per non dover effettuare misure a quelle frequenze (pochi ps di periodo) lavorano con il principio della misura dello sfasamento di una modulante. Resta vero, anche lavorando in sfasamento, il concetto successivo degli intervalli di ambiguità. Ne parliamo nell'incontro interattivo.
- A valle del discorso sul lavorare in sfasamento, fate riferimento alla figura https://home.roboticlab.eu/_detail/en/examples/sensor/lidar_phase_sift.png invece della figura 5.20
- Il discorso sulla scansione della scena, che porta poi ai dispositivi effettivamente usati in robotica (un LRF senza scansione è come quelli usati dai geometri), detti laser scanner, è più articolato di quanto detto nel libro, lo facciamo nell'incontro interattivo.
  Altro aspetto non citato dal libro, ma che sta diventando sempre più importante, è quello della intensità dell'onda riflessa: il testo parla della sola misura di distanza, ma una gran parte dei laser scanner moderni forniscono anche una intensità dell'eco, che è legata al "colore" della superficie su cui il raggio impatta.
- Nella figura 5.21 si parla, a mia opinione in modo scorretto, di dispositivo CCD. Il CCD è un componente elettronico analogico nelle intensità e discreto nello spazio, usato per effettuare la lettura seriale dei dati (analogici) raccolti in un numero discreto di elementi riceventi (ad esempio in una telecamera: c'è una matrice 2D di piazzole in cui ha luogo la conversione dell'energia ricevuta dalla scena in carica elettrica). È del tutto possibile costruire in misuratore di distanza con un laser ed una telecamera lineare (come presentato in figura 5.21), che si basa su un CCD per la lettura dei dati dell'array di elementi sensibili. Si tratta però di un approccio davvero poco usato, quando invece esistono dispositivi che non usano laser, ma luce infrarossa focalizzata (e per questo lavorano solo in precisi intervalli di distanza) ed al posto della camera lineare usato un dispositivo detto PSD (Position Sensitive Device, se volete potete guardare https://en.wikipedia.org/wiki/Position_sensitive_device). La Sharp ha un catalogo di dispositivi molto usato in robotica.
- Il secondo punto della lista puntata a pagina 225 viene usualmente chiamato "structured light" o "luce strutturata", ma il testo non lo dice.
  Il "transport mechanism (similar to an analog shift register)" is a CCD, ignoro perché il testo non usi il termine giusto dove sarebbe giusto usarlo.
  La descrizione del funzionamento dei sensori CMOS non mi risulta essere corretta, in particolare la tesi secondo cui il dato raccolto derivi da una scarica guidata dall'energia luminosa incidente e quindi (?) il sensore non è integrating. A me questo non risulta e facendo un po' di ricerche su internet trovo conferme che cambia la struttura (ogni pixel è trasdotto sul posto, senza fare uso di CCD) e la tecnologia produttiva sembra più semplice.
- Anche la tesi secondo cui le immagini dei sensori CMOS sarebbero esenti da blooming non mi risulta, cfr ad esempio https://patents.google.com/patent/US6633028B2/en. Per come sono costruiti i sensori CMOS, risultano meno soggetti al problema del blooming.
- Ad oggi non è normale trovare una camera con lo shutter; il tempo di integrazione è controllato a livello del sensore, non da un otturatore meccanico.
- Nella equazione 5.43 la "so-called camera calibration matrix" è la "camera projection matrix", che, anche se richiederà di essere calibrata, modella la proiezione.
- Si salti pure la digressione in fondo a pagina 229, da "If a monochrome CCD camera", fino a "this array is then updated at field or frame rate."; l'argomento non è più attuale: oggi di acqusisiscono direttamente dati in digitale.
- Il libro non copre per niente il campo delle camere 3D, sia a triangolazione che ToF. Ne parliamo nell'incontro interattivo.

# 
