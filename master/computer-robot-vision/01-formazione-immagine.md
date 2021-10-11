# Formazione dell'immagine

## Modelli geometrici

- prospettica
- ortografica
- scalata

**Modello pin-hole/proiezione prospettica**: immagine mondo reale - centro proiezione - immagine capovolta su piano immagine.

Sul piano immagine arrivano i raggi che passano dal foro.

**Proiezione ortografica**: punti non passano da un centro, quindi non sono ribaltati. Ad esempio posso usarla per camera nel cielo/spazio che guarda la Terra.

**Proiezione scalata**: proiezione intermedia tra prospettica e ortografica. Se guardo oggetti solo a una profondità le differenze prospettiche sono piccole, piccole differenze prospettiche.
Tipo nastro trasportatore con camera sopra.

### Modello pinhole

Retta che passa dal centro di proiezione $C$: retta di proiezione se la traccio da $P$ e $C$, retta di interpretazione se la traccio da $P'$ e $C$. 

Punto nel mondo $P(x,y,z)$, punto immagine $P(x', y', z')$.

![pinhole](img/pinhole.png)

Distanza piano immagine e centro proiezione è la distanza focale $f$, l' asse che passa su $f$ si chiama _asse ottico_.

Sapendo che $P'$ giace sul piano immagine possiamo dire che $z' = f$.
Sapendo anche che P e P' giacciono sulla stessa retta abbiamo che:

![pinhole2](img/pinhole2.png)
![pinhole3](img/pinhole3.png)

Se parto da immagine e trovo retta di interpretazione ho perdita di informazione, in quanto so trovare la retta ma non so trovare qual è il punto nel mondo, in quanto potrebbe trovarsi ovunque sulla retta trovata. Possibile soluzione è la stereoscopia.

Altra osservazione: stiamo dando per scontato di conoscere $f$.

Casi d'uso a seconda di variabili note e incognite:

|                 | Note          | Incognite |
|-----------------|---------------|-----------|
| Proiezione      | X, Y, Z, f    | u, v      |
| Interpretazione | u, v, f       | X, Y, Z   |
| Calibrazione    | X, Y, Z, u, v | f         |


Possiamo ribaltare il piano immagine e portarlo davanti al centro di proiezione, per non avere le coordinate "ribaltate". Chiamiamo questo piano _piano immagine virtuale_.

**Model based vision**: una piccola nota.
Quanto detto precedentemente (non poter sapere dov'è il punto nel mondo a partire dal punto immagine) è valido per un singolo punto.
Se nell'immagine ho un oggetto e conosco le caratteristiche dell'oggetto sono in grado di ricavare la posizione dell'oggetto e di quello che ha intorno.
Questa branca della computer vision non è parte del corso, non abbiamo abbastanza CFU per farlo.

## Dettagli tecnici sulle camere

### Necessità di lenti, lent sottili

### Cerchi di sfocamento e profondità di campo

### Spettro del campo elettromagnetico

### Frequenza di campionamento

