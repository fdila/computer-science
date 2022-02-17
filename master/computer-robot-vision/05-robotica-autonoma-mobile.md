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

### Beam Model

4 fenomeni:

- misura corretta con rumore locale, gaussiano
- oggetto inatteso: distribuzione esponenziale
- max range (fallimento del sensore): piccola uniforme
- numeri a caso: grande uniforme

Distribuzione totale è la mixture delle 4.
Come parametri abbiamo i 4 pesi delle 4 pdf che vengono sommate, il parametro sigma della gaussiana e il parametri lambda per l'esponenziale.

## Autolocalizzazione

### Tassonomia

### EKF based

### Grid based

### PF based

## SLAM

### SLAM EKF-based

### SLAM PF-based

### Visual SLAM

### Graph SLAM

## Approcci DNN per problemi di computer and robot vision