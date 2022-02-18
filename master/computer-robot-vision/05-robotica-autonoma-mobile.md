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

### Visual SLAM

## Approcci DNN per problemi di computer and robot vision