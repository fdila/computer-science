# Sensoristica

## Sensori propriocettivi

Misurano lo stato interno del manipolatore.
Esempi di misure dei sensori propriocettivi:

- posizione del giunto

- velocità del giunto

- coppia del giunto 

### Trasduttori di posizione

Danno in output un segnale elettrico proporzionale alla posizione lineare o angolare rispetto a una posizione di riferimento. Solitamente usati trasduttori angolari in applicazioni robot. I più comuni sono _encoder_ e _resolver_

#### Encoder

Due tipi di encoder: assoluti e incrementali.

Assoluti: cerchi (track) concentriche con sequenze di settori trasparenti e opachi. ad ogni combinazione corrisponde un angolo. 

Incrementali: più semplici ed economici. Due track con settori che si alternano in quadratura. Può anche esserci una track che segna il giro completo. L'approccio basato sulla misura della"frequenza del treno di impulsi", di fatto consistente nella misura del numero di cicli osservati, è adatta all'esecuzione di misure quando la velocità di rotazione è elevata perché le letture di posizione ottenute dall'encoder sono soggette ad un errore di quantizzazione piccolo, relativamente allo spazio percorso tra una lettura e la successiva. Al contrario, quando lo spazio percorso è piccolo, l'errore di quantizzazione diviene preponderante; in quest'ultimo caso si preferisce misurare il tempo che intercorre tra fronti consecutivi.

#### Resolver (no)

### Trasduttori di velocità

Si chiamano tacometri, i tipi base sono a corrente continua (DC) e a corrente alternata (AC).

#### Tacometro DC

È il tipo più usato. È un generatore a corrente continua il cui campo magnetico è fornito da un magnete permantente. Il voltaggio in uscita è proporzionale alla velocità angolare.
Data la presenza di un commutatore esiste un ripple non eliminabile, in quanto dipende dalla velocità angolare. 

#### Tacometro AC

Per evitare il ripple dei tacometri DC si può usare un tacometro AC. 

## Sensori eterocettivi

### Sensori di forza

#### Shaft torque sensor

misura corrente armatura in un motore dc brushed. 

#### Wrist force sensor

Misura tre componenti di forza e tre componenti di movimento rispetto al frame attached all'end-effector.
C'è una matrice di calibrazione.

### Sensori di distanza

Utili per determinare la presenza di un oggetto nel workspace e misurare la distanza dal robot.  Un sottoinsieme dei sensori di distanza sono i sensori di prossimità, che rilevano solo la presenza di oggetti vicino a parti sensibili del robot. La distanza entro la quale vengono rilevati gli oggetti si chiama _sensivitive range_ 
Nel caso genereale i sensori di distanza sono in grado di restiturire dati strutturati sulla posizione di oggetti nello spazio rispetto al sensore.
I tipi più usati sono i _sonar_ (SOund NAvigation and Ranging) che si basano sulla propagazione del suono attraverso fluidi elastici, e i _laser_ (Light Amplification  by Stimulated Emission of Radiation), che si basano sulla propagazione della luce.

#### Sonar

Usano pulsazioni acustiche e il loro eco per misuare la distanza di un oggetto. La distandza dell'oggetto è proporzionale al tempo di viaggio dell'eco, chiamato _time of flight (ToF)_, ovvero il tempo impegato per percorrere la distanza sensore-oggetto-sensore. Costano poco, pesano poco, consumano poca energia e sono facilmente computabili. Usano comunemente ultrasuoni, con frequenze tra 20KHz e 200KHz, ma esistono anche sonar che raggiungono i MHz.

$$
distanza = (velocitàDelSuono*ToF)/2
$$

Il raggio delle onde emesse dal sonar dipende dalla frequenza delle onde stesse: maggiore la frequenza, minore l'angolo e quindi maggiore è la risoluzione angolare. Tipicamente l'angolo è non infieriore a 15deg.

Lo stesso componente (il trasduttore) trasmette il segnale acustico e riceve l'eco. Ci sono due tipi di trasduttori: piezoelettrici e elettrostatici.
....

Se onda e materiale vanno d'accordo il materiale assorbe onda e non genera eco. Aneddoto della mammella imbalsamata.

#### Laser

(nb, qui li chiama laser, ma sarebbero Laser Range Finder LRF)

Due tipi: time-of-flight e con triangolazione.

Time-of-flight calcola la distanza misurando il tempo che passa tra quando viene emessa la luce a quando torna indietro e viene recepita dal detector. Praticamente come i sonar, solo che sostituiamo la velocità del suono con la velocità della luce.
...
I sensori ToF emettono solo un raggio, quindi le misure sono ottenute da un solo punto della superfice. Per ottenere più informazioni facciamo ruotare il raggio (o facciamo ruotare degli specchi).  
Posso avere più lrf tra loro inclinati in modo diverso rispetto all'asse di rotazione. LRF a più piani di scansione. 32/64 piani. Velodyne 32e per automotive. 
Arrray di Specchi MEMS.
Phased arrays: array controllati in fase. Emissione segnale in fase. 

 I sensori a triangolazione è basato sulla trigonometria (teorema del coseno).

C'è un laser che emette il laser e un sensore CCD che rileva la luce riflessa. Sapendo la distanza tra laser e ccd possiamo calcolare la distanza dell'oggetto.

#### ToF vs Triangolazione

Errore in ToF costante.

Errore in triangolazione dipende dalla distanza a cui si pone il target. Dipendenza quadratica. Più il target è lontano l'errore cresce quadrtaticamente. Decresce con la distanza tra i punti di vista. 

#### Lavorare a sfasamento

LRF lavorano quasi sempre in sfasamento. Si usa una modulante della frequenza dell'onda emessa, quindi guardo sfasamento tra fase onda emessa e fase dell'eco.

[RP Photonics Encyclopedia - phase shift method for distance measurements, laser rangefinders](https://www.rp-photonics.com/phase_shift_method_for_distance_measurements.html)

https://home.roboticlab.eu/_detail/en/examples/sensor/lidar_phase_sift.png

#### Vision sensors

Misurano intensita della luce riflessa da un oggetto. Si usa un elemento fotosensibile chiamto pixel, capace di trasformale la luce in energia elettrica. Sensori più comuni sono CCD e CMOS.

#### CCD

Charge Coupled Device. Array rettangolare di di photosites. 

Il CCD è un componente elettronico analogico nelle intensità e discreto nello spazio, usato per effettuare la lettura seriale dei dati (analogici) raccolti in un numero discreto di elementi riceventi (ad esempio in una telecamera: c'è una matrice 2D di piazzole in cui ha luogo la conversione dell'energia ricevuta dalla scena in carica elettrica). È del tutto possibile costruire in misuratore di distanza con un laser ed una telecamera lineare (come presentato in figura 5.21), che si basa su un CCD per la lettura dei dati dell'array di elementi sensibili. Si tratta però di un approccio davvero poco usato, quando invece esistono dispositivi che non usano laser, ma luce infrarossa focalizzata (e per questo lavorano solo in precisi intervalli di distanza) ed al posto della camera lineare usato un dispositivo detto PSD (Position Sensitive Device, se volete potete guardare https://en.wikipedia.org/wiki/Position_sensitive_device). La Sharp ha un catalogo di dispositivi molto usato in robotica.

#### CMOS

Complementary Metal Oxide Semiconductor. Array rettangolare di fotodiodi. 

#### Camera

todo

#### Camere 3D

Luce strutturata. Ricostruzione 3d di un profilo generato.  Profilometria. Triangolazione.

Kinect 1: a triangolazione. da una parte emettitore che emette fasci laser, in direzioni pseudocasuali. Camera osserva questi spot. Algorimti sono in grado di capire quale spot corrisponde a quale fascio. Così calcolo con triangolazione distanza.

Elevata quantità di coordinate 3d di punti. Dotato anche di camera RGB a metà tra camera infrared e proiettore. Questa camera è calibrata in modo da poter attribuire colore a punti. Genera immagine RGB corredata di info di profondità. Le camere 3d possono essere in grado di generare o solo dato profondità, o anche con colori. Camere RGBD hanno sia profondità che colori. 

In outdoor l'energia prodotta dal sole non funzionano.

In indoor il range è limitato dall'intensità degli spot emessi, qualche metro di distanza (4-5 metri).

Camere 3d basate su ToF, si chiamano FLASH LIDAR. Proietta ovunque. Per ciascun target si ha un echo. All'interno della camera array di rilevatori di echo.
Flash modulato, echo modulato, si lavora in sfasamento. Ciascun elemento che riceve echo è in grado di dire lo sfasamento da quando è stato emesso il flash. Ricostruisco così profondità. Abbiamo mappa di profondità. Immagine a 2D e mezzo. Kinect2 era ToF con camera RGB. Nel kinect2 risoluzioni più elevate dell'uno. Campo di lavoro 8-9 metri, anche in outdoor.

### Proximity sensing

in un range di lavoro, avvertire presenza di oggetto a prescindere dalla localizzazione.

#### uso di range sensor

direttiva macchine per dispositivi sicurezza.

#### capacitativi

sapere che esistono

piatti condensatore, modifica capacità inbase a tocchi, range di pochi cm

#### induttivi

sapere che esistono

passa un oggetto, variazioni di campo elettromagnetico

#### magnetici

come induttivi

#### fotocellule, generalità, a forchetta, a riflessione

fascio tra forchetta. vedo fascio e se si interrompe significa che qualcosa è in mezzo. si usano dentro gli encoder.

a riflessione: emetto e rilevo echo. Vantaggio: costruzione più robusta, nei sistemi a forchetta devo garantire allineamento, a riflessione c'è solo un dispositivo.

#### effetto Hall

come magnetici

#### PIR (Passive InfraRed)

quello degli antifurti. motion detection. banda infrared lontana, misurano calore. 

### Point Clouds

lista di punti nello spazio

assieme al dato geometrico, dato pittorico

registrazione pc: "fondere" più point cloud, ad esempio per fondere più pc a partire da odometria. algoritmi per riallineare pc visto che odometria non è perfetta

ICP iterative closest point: con stima iniziale di posizione relativa. si cercano corrispondenze.

100mila varianti.
