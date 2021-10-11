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

### Necessità di lenti, lenti sottili

Dal punto di vista fisico il modello pinhole è irrealizzabile, in quanto il foro (centro di proiezione) non può essere infinitesimo nella realtà.

Il foro è di una dimensione finita, da cui passaranno più raggi paralleli, passiamo dall'avere un punto immagine ad avere un "cerchio immagine". I cerchi si vanno a sovrapporre e questo è un problema. Se restringo troppo il cerchio (cerchio infinitesimo) entra troppa poca energia (energia infinitesima). 

Si introduce quindi l'uso di lenti. Di solito si hanno più lenti insieme, noi ci soffermiamo su modello con singola **lente sottile**.
I raggi arrivano alla lente e convergono in un punto. Questo punto è chiamato **fuoco** della lente (questo se tutti i raggi arrivano paralleli tra loro). La lente è composta da due calotte sferiche, al centro troviamo un piano. Il centro di questo. La distanza tra il centro di questo piano e il fuoco è chiamata **focale della lente**.
Se da un punto $P$ arrivano raggi non paralleli tra loro troveremo un punto $P'$ diverso dal fuoco, in cui il punto immagine è a fuoco.
**Legge di Snell** (con $Z$ distanza centro lente - punto nel mondo e $Z'$ distanza centro lente - punto immagine): 
$$
1/Z + 1/Z' = 1/f
$$

I vari punti del mondo vanno quindi a fuoco ad una distanza diversa.

### Cerchi di sfocamento e profondità di campo

Il fatto che i vari punti vadano a fuoco a distanze diverse e che il piano immagine sia ad una distanza fissa porta ad avere dei "cerchi" sul piano immagine, i così detti **cerchi di sfocamento**.
Dipendono sia dalla posizione a cui vanno a fuoco i punti e dalla posizione del piano immagine.

### Spettro del campo elettromagnetico

Legato alle lenti è l'indice di rifrazione, che varia a seconda della lunghezza d'onda dello spettro.
(TODO trovare un senso a questa lezione).

### Frequenza di campionamento

I dispositivi digitali abbiamo una serie di elementi sensibili (sensori) disposti ad una certa distanza. La distanza tra essi fa si che il dispositivo abbia una specifica frequenza di campionamento legata anche alla lunghezza d'onda. 
Per catturare lunghezze d'onda di $n$ micrometri dobbiamo avere sensori disposti ad almeno $n/2$ micrometri tra loro.

Il diametro dei cerchi di sfocamento deve essere inferiore alla spaziatura dei sensori. Inizio a percepire la presenza dei cerchi di sfocamento esce dai confini del singolo sensore e viene percepito in più sensori.

Diametro cerchi di sfocamento:
$$
D/Z' * (Z'_{segnato} - Z')
$$

$Z'$ è il punto dove va a fuoco il punto.
$Z'_{segnato}$ è la distanza del piano immagine.
$D$ è il diaframma della camera, che limita i raggi entranti che si proiettano sul piano immagine.

Agendo sul diaframma riesco a modificare la **profondità di campo**.

## Difetti e problemi

### Aberrazioni cromatiche

Indice di rifrazione è dipendente dalla lunghezza d'onda. 

Allontanandosi dal centro immagine ci allontaniamo dal modello ideale pinhole.

Messa a fuoco dipende anche dalle lunghezza d'onda, aberrazione cromatica.

### FOV, Field of View, distorsioni radiale e tangenziale

**FOV**: più è lungo l'obiettivo più è "stretta" l'immagine.

Esempio lente fisheye: focale corta, grande FOV ma tante aberrazioni che ci fanno discostare da modello pinhole.

**Distorsione radiale**: distorsioni più intense delle tangenziali.
A loro volta si suddividono in:
- **a cuscinotto**: distanze centro immagine crescono.
- **a barilotto**: distanze centro immagine descrescono.

![distorsioni](img/distorsioni-radiali.png)
*In rosso distorsione a cuscinotto, in blu distorsione a barilotto*

In funzione della distanza dal centro immagine la proiezione nominale cresce lungo il raggio oppure decresce lungo il raggio. 
Quindi spostamento punto immagine lungo la retta, in avanti o indietro ma resta sempre sulla retta.

**Distorsione tangenziale**: Il punto proiettato si sposta dalla retta di proiezione in modo ortogonale al raggio.

<u>**Le distorsioni non sono riconducibili ad un modello lineare di proiezione**</u>

Posso applicare un algoritmo per rimuovere distorsioni prima e successivamente applicare il modello lineare di proiezione.

### Vignetting

Cresce con lunghezza focale e cresce con distanza da centro immagine.
Il passaggio tra i vari "pezzi" dell'obiettivo fa perdere i raggi sui bordi interni dell'ottica. 
L'intensità luminosa media decresce al crescere della distanza dal centro immagine.
Questo problema aumenta all'aumentare della lunghezza dell'ottica.

## Calibrazione della proiezione

