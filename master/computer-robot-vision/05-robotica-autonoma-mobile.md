# Percezione per robotica autonoma mobile

## Basi di cinematica & co

Cinematica differenziale: solite cose.

**Raggio di curvatura**: per ogni punto di una linea dello spazio posso calcolare la tangente alla linea. Cerchio osculatore, tracciato tra tre punti della linea. COSE.

Cinematica ackermann: solite cose, differenziale sulle ruote dietro.

Synchro-drive: due motori, cose complicate, trasla.

Veicoli anolomici: omnidirezionali, ruote mechanum/swedish.

## Modelli per stato robot

Velocity model è meno accurato e viene usato per il motion planning, odometry model è più accurato ma presuppone di aver già effettuato il movimento e quindi non puòò essere usato per il planning.

### Velocity Model

Uso i comandi di velocità (velocità di traslazione e di rotazione) per trovare $p(x_t|x_{t-1}, u_t)$

### Odometry Model

Suppongo di aver fatto già il movimento e aver misurato le rotazioni. Quindi calcolo l'odometria.
Il movimento è scomposto in 3 movimenti elementari: rotazione, traslazione, rotazione.
  
## Sistemi di range sensing

As usual, ci sono problemi a misurare le cose nel mondo. Rumore gaussiano non è realistico.

### Beam Modelgit

4 fenomeni:

- misura corretta con rumore locale, gaussiano
- oggetto inatteso: distribuzione esponenziale
- max range (fallimento del sensore): piccola uniforme
- numeri a caso: grande uniforme

Distribuzione totale è la mixture delle 4.
Come parametri abbiamo i 4 pesi delle 4 pdf che vengono sommate, il parametro sigma della gaussiana e il parametri lambda per l'esponenziale.

## Autolocalizzazione

Sapere dov'è il robot nella mappa.

### Tassonomia

- Global localization vs local
- Kidnapped robot
- Ambienti statici vs dinamici

Gli algoritmi probablistici sono tutti varianti del filtro di Bayes.
Da pose precedente, controllo, misura, e mappa ricavo la pose successiva facendo predizione e integrazione delle misure.

### EKF based
Caso speciale dei localizzazione Markoviana.
Il belief dello stato è rappresentato da media e covarianza.
Supponiamo che la mappa sia una mappa di features.

- Inizialmente assumiamo di conoscere le corrispondenze tra misure e features.
- Se non abbiamo le corrispondenze (cosa molto comune) le cose si complicano, problema data association.

### Grid based

Usa histogram filter. Mappa divisa in una griglia.

### PF based

AMCL, filtro a particelle.

Problema kidnapped robot -> soluzione aggiungere particelle random

KDL sampling: si adatta il numero di particelle all'incertezza che abbiamo

## SLAM

Simultaneous localization and mapping.

Online SLAM: $p(x_t,m | u_{1:t}, z_{1:t})$

Full SLAM: $p(x_{1:t},m | u_{1:t}, z_{1:t})$

### SLAM EKF-based

Si usano mappe feature-based.

#### SLAM con corrispondenze note

Simile a localizzazione EKF con corrispondenze note, ma ora stimiamo anche la pose dei landmark.
Il vettore di stato quindi comprende sia la pose del robot che la pose di tutti i landmark.

#### SLAM senza corrispondenze note

Estendiamo SLAM con corrispondenze note a SLAM senza corrispondenze note introducendo lo stimatore Maximum Likelihood Correspondence.

### Graph SLAM

Risolve problema Full SLAM.

Grafo costituito da nodi (pose + mappa) e archi (costraint tra i vari nodi).

### SLAM PF-based

L'approccio con particle filter usa come vettore di stato pose del robot + mappa, quindi abbiamo $p(x,m)$.
Trattare così il problema sarebbe impensabile per la complessità computazionale del calcolo delle particelle. Possiamo notare che se sapessimo con esattezza la pose del robot nel mondo potremmo stimare la pose delle feature nel mondo in modo indipendente l'una dall'altra.
Basandoci su questa osservazione possiamo quindi usare un PF conosciuto come **Rao-Blackwellized**. Questi filtri usano le particelle per rappresentare la postirior di alcune variabili e delle gaussiane (o altre pdf parametriche) per rappresentare altre variabili.

FastSLAM usa le particelle per tenere traccia delle pose, e una gaussiana per ogni feature della mappa. Questo è diverso da EKF-SLAM: in quel caso avevamo una sola gaussiana per stimare la posizione di tutte le feature insieme. Inoltre FastSLAM ha il vantaggio di poter fare diverse data association per ogni particella, avendo quindi più data association e non una singola come in EKF.
FastSLAM usando particelle che tengono traccia di tutta la storia delle pose risolve sia il problema Full SLAM che Online SLAM.

FastSLAM 2.0 fa il sampling delle poses oltre che usando il controllo usando la misura.

FastSLAM ha problemi con le loop closures (TODO non ho interiorizzato il perchè)

**Grid-based FastSLAM**: GMapping

### Visual SLAM

SLAM con camera monoculare. Basato su filtraggio EKF. 
Problema principale depth dei landmark in quanto con proiezione camera si perde l'info 3D.
Quando inizializziamo una nuova feature non abbiamo info sulla profondità. Due soluzioni:

- Delayed initialization:per ogni feature setto un insieme di ipotesi e la rappresento con una funzione solo dopo che è
“collocata”, ovvero dopo un po’ di movimento.Il problema è che queste osservazioni non sono fissate per aggiornare la stima della pose
della camera fino a che non sono convertite e inizializzate veramente. Dal punto di vista della stima possiamo pensare che tutti i punti (features) all’inizio siano all’infinito e si “avvicinino” nel momento in cui il moto della camera crea una parallasse semplicemente ampia. 
Per i punti vicini non c’è problema, per quelli lontani potrebbero volercidei metri o dei kilometri. E’ però importante che questi non siano pienamente indicati come all’infinito, ma che in qualsiasi momento, durante il processo di filtraggio, possono “provare” la loro profondità nel momento in cui c’è stato abbastanza moto. E’ necessario trovare una rappresentazione che dica qualcosa anche di questi punti all’infinito, per esempio, dopo tot moti di traslazione della camera posso dire che il punto è almeno a tot metri dalla predizione.
- Undelayed initialization: tengo il raggio (retta di proiezione) e la depth sconosciuta, con una parametrizzazione, inizializzo feature appena la vedo.

**Monocular SLAM: unified inverse depth**
Le nuove feature sono inizializzate considerando una sola immagine, l’immagine dove la feature è misurata per la prima volta.
L’inizializzazione include lo stato iniziale e la covarianza ( [1,inf] ). Data la linearità della parametrizzazione l’incertezza può essere rappresentata con una funzione e processata con EKF. Finché l’incertezza sulla profondità rimane alta la feature è usata principalmente per determinare l’orientamento della camera.

Oggetti lontani: piccolo parallasse, incertezza non gaussiana, usati per stimare l'orientamento.
Oggetti vicini: grande parallasse, incertezza gaussiana, usati per stimare la traslazione.

**unified inverse depth** parametrization: per ogni feature ho x,y,z della camera nel momento in cui è stata rilevata la feature, i due angoli e l'inverso della distanza. 