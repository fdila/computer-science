# Percezione per robotica autonoma mobile

## Basi di cinematica & co

Cinematica differenziale: solite cose.

**Raggio di curvatura**: per ogni punto di una linea dello spazio posso calcolare la tangente alla linea. Cerchio osculatore, tracciato tra tre punti della linea. COSE.

Cinematica ackermann: solite cose, differenziale sulle ruote dietro.

Synchro-drive: due motori, cose complicate, trasla.

Veicoli anolomici: omnidirezionali, ruote mechanum/swedish.

## Modelli per stato robot

### Velocity Model

Uso le  velocità come contro llo. 

### Odometry Model

Suppongo di aver fatto già il movimento e aver misurato le rotazioni. Quindi calcolo l'odometria.
  
## Sistemi di range sensing

As usual, ci sono problemi a misurare le cose nel mondo. Rumore gaussiano non è realistico.

### Beam Model

4 fenomeni:

- misura corretta con rumore locale, gaussiano
- oggetto inatteso
- max range
- numeri a caso



## Autolocalizzazione

### Tassonomia

### EKF based

### Grid based

### PF based

## SLAM

### SLAM EKF-based

### SLAM PF-based

### Visual SLAM

## Approcci DNN per problemi di computer and robot vision