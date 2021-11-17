% Computer and Robot Vision, 2021/2022
% Federica Di Lauro
%

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

![pinhole2](img/pinhole2.png){ width=50% }
![pinhole3](img/pinhole3.png){ width=20% }

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
I raggi arrivano alla lente e convergono in un punto. Questo punto è chiamato **fuoco** della lente (questo se tutti i raggi arrivano paralleli tra loro). La lente è composta da due calotte sferiche, al centro troviamo un piano. La distanza tra il centro di questo piano e il fuoco è chiamata **focale della lente**.
Se da un punto $P$ arrivano raggi non paralleli tra loro troveremo un punto $P'$ diverso dal fuoco, in cui il punto immagine è a fuoco.

**Equazione delle lenti sottili** (con $Z$ distanza centro lente - punto nel mondo e $Z'$ distanza centro lente - punto immagine): 
$$
1/Z' - 1/Z = 1/f
$$

I vari punti del mondo vanno quindi a fuoco ad una distanza diversa.

Le conseguenze dell'approssimazione lente sottile sono diverse:

- I raggi che vengono rifratti nella lente subiscono un’unica deviazione;
- La distanza focale (f) può essere presa indiﬀerentemente dal centro ottico o dalla superficie della lente;
- I due fuochi sono simmetrici rispetto al centro ottico e le due distanze focali sono uguali.

### Cerchi di sfocamento e profondità di campo

Il fatto che i vari punti vadano a fuoco a distanze diverse e che il piano immagine sia ad una distanza fissa porta ad avere dei "cerchi" sul piano immagine, i così detti **cerchi di sfocamento**.
Dipendono sia dalla posizione a cui vanno a fuoco i punti e dalla posizione del piano immagine.

### Spettro del campo elettromagnetico

Legato alle lenti è l'indice di rifrazione, che varia a seconda della lunghezza d'onda dello spettro. Quindi le varie componenti a lunghezza d'onda diversa possono subire aberrazioni dovute alla rifrazione.

### Frequenza di campionamento

I dispositivi digitali abbiamo una serie di elementi sensibili (sensori) disposti ad una certa distanza. La distanza tra essi fa si che il dispositivo abbia una specifica frequenza di campionamento legata anche alla lunghezza d'onda. 
Per catturare lunghezze d'onda di $n$ micrometri dobbiamo avere sensori disposti ad almeno $n/2$ micrometri tra loro.

Il diametro dei cerchi di sfocamento deve essere inferiore alla spaziatura dei sensori. Inizio a percepire la presenza dei cerchi di sfocamento esce dai confini del singolo sensore e viene percepito in più sensori.

Diametro cerchi di sfocamento:
$$
\frac{D}{Z'} * (\overline{Z'} - Z')
$$

$Z'$ è il punto dove va a fuoco il punto.

$\overline{Z'}$ è la distanza del piano immagine.

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

![In rosso distorsione a cuscinotto, in blu distorsione a barilotto](img/distorsioni-radiali.png){ width=60% }

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

Abbiamo due problemi legati alla calibrazione della proiezione:

- i parametri intrinseci della camera
- i parametri estrinseci, ovvero la pose della camera rispetto al mondo 

Analizziamo i problemi legati ai parametri intrinseci.

Rappresentazione in forma matriciale della proiezione con uso di coordinate omogenee.

Tornando alla proiezione del modello pin hole avevamo che:

$$
\begin{cases}
u = f*(X/Z) \\
v = f*(Y/Z)
\end{cases}
$$

Se abbiamo punto $P^C$ ovvero il punto mondo in coordinate omogenee $|w_1, w_2, w_3, w_4|^T$ rispetto alla camera, possiamo trovare una matrice di dimensioni (3,4) tale che $K*P^C = |w_1, w_2, w_3|^T$, e possiamo dire che: 

$$
\begin{cases}
u = w_1/w_3 \\
v = w_2/w_3
\end{cases}
$$

Sappiamo anche che:

$$
\begin{cases}
w_1 = fx \\
w_2 = fy \\
w_3 = z
\end{cases}
$$

La matrice vista sopra è quindi:

$$
M = 
\begin{bmatrix}
f & 0 & 0 & 0 \\
0 & f & 0 & 0 \\
0 & 0 & 1 & 0 \\
\end{bmatrix}
$$

E troviamo quindi il punto sull'immagine corrispondente al punto mondo.

$$
p = M*P^C
$$

TODO 
Notiamo inoltre che la lunghezza focale utilizzata nella matrice degli intrinseci deve essere espressa in pixel, mentre solitamente nelle specifiche della camera è espressa in millimetri. Sapendo la dimensione di un pixel possiamo trovare:

$f [pixels] = \frac{(focal length [mm])}{(pixel pitch [\mu m / pixel])}$


Problemi ancora aperti:

- centro immagine spostato rispetto al centro di proiezione.
- aspect ratio non unitario: dobbiamo posizionare correttamente il valore di posizione in memoria nel piano immagine continuo. Dovuto alla disposizione degli elementi sensoriali e la loro spaziatura su asse x e y.
- non perpendicolarità tra righe e colonne di pixel, ovvero lo *skew*, anche se normalmente è 90°

Per il primo punto abbiamo una pura tralsazione, per il secondo troviamo il rapporto tra la spaziatura sulle x e la spaziatura sulle y.

$$
\begin{bmatrix}
1 & 0 & u_0 \\
0 & 1 & v_0 \\
0 & 0 & 1 \\
\end{bmatrix}
$$

Per il secondo abbiamo una matrice per scaling
$$
\begin{bmatrix}
ar & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1  \\
\end{bmatrix}
$$

Per il terzo abbiamo un singolo parametro 
$$
\begin{bmatrix}
1 & s & 0 \\
0 & 1 & 0 \\
0 & 0 & 1  \\
\end{bmatrix}
$$

Moltiplicando tra loro le matrici troviamo la matrice degli intriseci, comunemente chiamata $K$:

$$
K = 
\begin{bmatrix}
ar*f & s & u_0 \\
0 & f & v_0 \\
0 & 0 & 1 \\
\end{bmatrix}
$$


Se abbiamo anche la matrice $T^C_W$ che rappresenta la rototraslazione della camera rispetto al mondo possiamo trovare la proiezione rispetto al mondo:

$$
K \cdot T^C_W
$$

infatti 

$$
T^C_W * P^W = P^C
$$

Moltiplicando tutte le matrici viste troviamo la matrice di proiezione totale.
Per scrivere la matrice totale abbiamo bisogno di 10 parametri:

- 3 di rotazione e 3 di traslazione per la matrice che rappresenta la rototraslazione tra camera e mondo
- 1 (ovvero $f$) per la matrice che proietta il punto
- 2 per la traslazione del centro immagine
- 1 per l'aspect ratio 
- 1 per lo skew

La matrice totale è una (3,4), ovvero ha 12 elementi, di cui 11 indipendenti in quanto stiamo usando matrici per trasformazioni omogenee.


### Calibrazione DLT (Direct Linear Transform)

Troviamo direttamente i valori numerici dei componenti della matrice totale di calibrazione.

In fase calibrazione abbiamo immagine e informazione tridimensionale del punto scena.
Effettuiamo quindi delle misure che ci danno delle relazione sugli 11 valori incogniti della matrice di calibrazione.
Ogni misura che prendiamo ha 5 elementi:

$$
\begin{bmatrix} x & y & z & u & v \end{bmatrix}^T
$$

Per ogni misura posso impostare un sistema.

$$
\begin{cases}
w_1 = m_{1,1} * x + m_{1,2} * y + m_{1,3}*z + m_{1,4} \\
w_2 = m_{2,1} * x + m_{2,2} * y + m_{2,3}*z + m_{2,4} \\
w_3 = m_{3,1} * x + m_{3,2} * y + m_{3,3}*z + m_{3,4}
\end{cases}
$$

Sapendo che $u = w_1/w_3$ e $v = w_2/w_3$ troviamo un sistema con due equazioni (per semplicità di scrittura non scrivo per esteso $w_1, w_2, w_3$ trovati sopra):

$$
\begin{cases}
u*w3 - w1 = 0 \\
v*w3 - w2 = 0
\end{cases}
$$

Quindi _teoricamente_ per trovare gli 11 parametri mi servono almeno 6 misure, però non ha senso in quanto ci saranno sicuramente errori nelle misure. Si usano centinaia di punti.

Andiamo a fare una regressione andando a minimizzare il quadrato degli errori.

Da una parte ho lo spazio tridimensionale dei punti (x,y,z) e lo spazio bidimensionale dello spazio 2d piano immagine con i punti (u, v).
Devo coprire tutto lo spazio.

Con DLT i vari componenti della matrice $M$ non hanno una struttura precisa, troviamo solo dei valori numerici, non riflettono la struttura "vera" della matrice con proiezioni, aspect ratio etc.

Aspetto pratico: immagine con un pattern (scacchiera o pallini), nel mondo reale metto pattern planare, così devo solo trovare la posizione del pattern planare e trovo successivamente la posizione dei pallini/quadrati conoscendo la posizione del pattern.
Metto sistema di riferimento mondo in un posto comodo, poi faccio triangolazione tra sistema e pattern planare.

![Segmento AB -> pattern planare, O -> origine sistema riferimento, segmento OR -> baseline](img/dlt_triangolazione.png){ width=60% }

Questa triangolazione è soggetta ovviamente a incertezze nelle misure.
Questa incertezza è non-costante, la distribuzione degli errori cambia al variare della distanza del punto dall'osservatore.

La precisione con il quale trovo AB dipende molto dalla distanza OR.

Dobbiamo rappresentare anche l'incertezza delle misure. Come? Lo scopriremo nel futuro.

Esistono configurazioni degeneri (scoperte da Faugeras (?)) nello spazio 3D che non mi permettono di calcolare la matrice $M$. I punti che vado a prendere devono giacere su piani diversi.

### Calibrazione con metodo Zhang

NB sezione fatta mooolto poco, il prof voleva quasi tagliarla, basta sapere che esiste in pratica. Riferirsi al laboratorio pratico se si vogliono più info.

- Homography: si stanzia in un'omografia tra piani. Omografia -> punti di un piano finiscono in corrispondenza coi punti di un altro piano. Rappresentabile come trasformazione in coordinate omogenee.

- Parametri intrinseci/estrinseci.

Immagini utilizzate: target planare, solitamente scacchiera. 
Vengono determinati i punti di intersezione tra quadrati neri e quadrati bianchi.
Non fornisco l'informazione rispetto ad un unico sistema di riferimento.
Ciascun insieme di punti è noto nel suo sistema di riferimento (ovvero la scacchiera, solitamente lo posizioniamo in corrispondenza del primo _corner_ trovato).

La tecnica Zhang lavora in 2 fasi. Inizialmente determina i parametri intrinseci, utilizzando le diverse immagini raccolte.
Dopo di che posso trovare gli estrinseci.

Questo approccio permette anche di calibrare i parametri di distorsione.

**Caratterizzazione di matrici proiezione prospettica**

Caratteristiche della matrice M di proiezione:

$$
M = 
\begin{bmatrix}
a_{1,1} & a_{1,2} & a_{1,3} & b_1 \\
a_{2,1} & a_{2,2} & a_{2,3} & b_2 \\
a_{3,1} & a_{3,2} & a_{3,3} & b_3 \\
\end{bmatrix}
$$

Se chiamiamo $A$ la matrice composta dagli $a_{i,j}$ e $a_i$ le righe i-esime si ha sempre che:

$$
det(A) \neq 0
$$

Se abbiamo una matrice con _zero skew_ possiamo dire che:

$$
(a_1 * a_3) \cdot (a_2 * a_3) = 0
$$

Se abbiamo una matrice con _aspect ratio unitario_ abbiamo:

$$
(a_1 * a_3) \cdot (a_1 * a_3) = (a_2 * a_3) \cdot (a_2 * a_3)
$$

## Aspetti tecnologici

Sensori a stato solido.

### CCD

Matrice di elementi nelle quali viene svolta la trasduzione. In ogni elemento sensibile si accumula una carica.
Tra gli elementi sensibili c'è un registro di scorrimento.
Tra ogni colonna abbiamo una colonna di registri a scorrimento, che vanno poi a scrivere in una riga di registri a scorrimento. **Interline transfer**.
La presenza di colonne di registri implica la presenza di zone cieche tra una colonna di elementi sensibili e l'altra. Questo problema viene risolto con l'utilizzo di microlenti applicate sopra agli elementi sensibili e che coprono anche i registri, in modo da concentrare la luce in arrivo sull'elemento sensibile.

Rumore: ogni volta che la carica si sposta c'è rumore. Soffrono anche di rumore termico.

Per risparmiare i produttori hanno inventato la scansione interlacciata, ovvero la scansione delle righe della matrice avviene su due tempi, in un primo tempo viene scansionata la riga pari, nel tempo successivo la riga dispari. Questo permette di utilizzare un solo registro a scorrimento per due righe. Se abbiamo una scena dinamica ci troveremo con immagini strane, magari con elementi raddoppiati in quanto i tempi di esposizione di righe pari e dispari è diverso.

Il problema di interlacing è vecchio, ormai si ha la **progressive scan** in cui le righe sono scansionate una dopo l'altra.

Esiste anche la struttura chiamata **frame transfer**: gli elementi ciechi non sono tra le colonne ma sono in uno spazio separato.

### CMOS

Ho contemporaneamente sul disposistivo sensoriale una capacità di elaborazione.

Si ha indirizzamento di pixel: si riesce ad indirizzare ogni singolo elemento.

Il tempo tra una lettura e l'altra è (spesso) il tempo di esposizione, ovvero per quanto facciamo "caricare" l'elemento sensibile.

Legato al tempo di esposizione è il **motion blur**: se integro l'immagine per troppo tempo e il soggetto/scena è in movimento fa si che i punti degli oggetti di interesse passino per i diversi pixel.

**Rolling shutter**: shutter rolla tra i vari pixel dell'immagine, ho tempi di esposizione diversi tra i vari elementi sensibili della camera.

**Global shutter**: shutter globale, stesso tempo di esposizione tra tutti i pixel. È più difficile da fare con tecnologia CMOS.

Si ha un rapporto lineare tra energia in ingresso e in uscita dal sensore. È un rapporto lineare fino alla fascia di saturazione.
Dovuto alla saturazione è il problema di **blooming/smearing**: la carica che fa andare in saturazione un sensore si va poi a "espandere" sui sensori vicini, andandoli a saturare.

**HDR**: range dinamico, delta tra valore minimo e valore massimo. 
Se ho scena statica posso fare la stessa foto con esposizione diversa e mettere assieme le varie parti della scena, ottendeno un range dinamico alto. Esistono anche telecamere a range dinamico: 

- telecamere HDR che fanno doppia esposizione
- telecamere che misurano in modo continuo la carica su ogni pixel, se un pixel satura lo svuota e conta quante volte lo svuota. Quindi ogni pixel ha un range molto più alto rispetto al range del solo sensore.

**Efficienza quantica**: l'intensità del segnale catturato dal sensore varia a seconda della lunghezza d'onda. I sensori a stato solido sono caratterizzati da una coda verso il near infra-red. Le frequenze d'onda sono trasdotte con intensità diverse. 
Questo implica uno scostamento dalla fedeltà cromatica.

Bisogna inoltre **quantizzare** il segnale: a seconda del numero di bit abbiamo un rapporto segnale-rumore diverso. Esso è definito generalmente come $SNR = \mu / \sigma$. Il rumore della camera può produrre deviazione standard alta e influire sul numero di byte realmente necessari: sono necessari di 50dB di rapporto segnale rumore per avere 8 bit di dati significativi.

### Camere 3D

Kinect 1: NON È UNA CAMERA 3D, fa triangolazione con due camere.

Funzionano sul principio ToF. Differenza con lidar: il lidar gira.
Flash lidar == camera 3D.

### Visori notturni

In condizioni estreme si raffreddano le camere per ridurre effetto joule. 

Nei visori notturni si illumina l'area con luce NIR, con i sensori riesco a vedere luce NIR.

### Camere a colori

Posso avere 3 senso R G B separati per ogni pixel, ma è molto improbabile.

La maggior parte delle camere esistenti segue l'approccio basato sul **bayer filter**. Ogni blocco di 4 pixel ha 2 pixel ricoperti da un filtro per il verde, un pixel per il blu e uno per rilevare il rosso.
Si hanno poi algoritmi di interpolazione per i colori.

Si può avere sottocampionamento sulla crominanza rispetto alla luminanza.

Le camere professionali possono avere algoritmo di interpolazione di colore integrat, oppure mi danno i valori dei pixel associati al loro "colore" (quindi se è un pixel con filtro R, G o B)

**Stacked sensors**: impiliamo più strati, ogni strato ha un sensore R, G o B e da filtri che fanno passare la luce del colore corrispondente.

## Event Based Cameras

Nuovo tipo di camere che registra le variazioni di luce (movimento) anzichè registrare immagini statiche.

Sono costituite da una matrice di pixel, ma questi pixel sono asincroni tra di loro e "scattano" quando viene rilevato un cambiamento di luce sul sensore: quando il cambiamento è positivo (incremento di luce) si ha un evento positivo, e viceversa.

Non si hanno più immagini ma stream di eventi.

In una camera normale se c'è movimento molto veloce si ha motion blur, mentre le event cameras riescono a registrare eventi con una frequenza di 1 $\mu$ s

Nelle camere ad eventi non c'è informazione ridondante: si hanno solo informazioni su ciò che sta cambiando, il che porta a non avere uno "sfondo" e riduce il data rate.

Si hanno anche vantaggi sul HDR.

Si possono usare per **optical flow**, **visual odometry**, **SLAM**







