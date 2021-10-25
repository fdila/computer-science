# Stereoscopia

Ricostruiamo il mondo avendo due camere e le immagini da esse scattate nello stesso momento.

Intersezione dell'asse ottico delle due camere: **punto di fissazione**. 

Linea che congiunge i due centri della camera: **baseline**. Più le camere sono distanti più ho precisione. *Vedi parte sulla triangolazione nel capitolo formazione immagine*

**Epipoli**: intersezione tra baseline e piani immagine. Se camere sono parallele sono all'infinito.
Tutto il piano identificato da puntomondo - centro camera 1 - centro camera 2 si chiama **piano epipolare**.

Problemi da affrontare per ricostruzione con stereoscopia:
- Abbiamo misure su piano immagine, informazioni sulle camere, dobbiamo intersecare P'C1 e P''C2. Problema triangolazione.
- Ricerca delle corrispondenze dei punti mondo nei due piani immagine.

Per la ricerca delle corrispondenze posso identificare un piano immagine come primario e uno secondario. Dò un identificativo ai punti sul primario, e cerco le corrispondenze nel secondario.
Poi faccio viceversa e confronto le corrispondenze.
Ricerca molto complessa.

**Ipotesi fondamentale stereoscopia**: vado a cercare un intorno di P' circa uguale a un intorno di P''

Tanto più è ampia la baseline più è a rischio questa ipotesi: più è ampia più cambio punto di vista e rischio di non trovare agevolmente le corrispondenze.

## Approcci alla stereoscopia

- Feature based: cerco delle corrispondenze a livello di "cose" nell'immagine

- Pixel level/gray level: trovo corrispondenze a livello di pixel sfruttando i vincoli della geometria


### Vincolo epipolare

Per trovare corrispondenze sfrutto il fatto che dal punto immagine P' il punto nel mondo è sicuramente un punto sulla line C1-P, quindi il punto corrispondente nel piano immagine 2 si troverà su questa retta proiettata, non devo ceracare in tutto il piano immagine 2.
Possiamo dire che il possibile punto corrispondente P'' si trova nell'intersezione tra il piano epipolare che si forma con C1-P-C2 e il piano immagine 2. La retta che viene a formarsi in questo modo è la **linea epipolare**.
Tutte queste linee passano per l'epipolo.

Più formamlemente diciamo che:
$$
\forall P'_{\pi_{1}} \text{ prendo sul piano immagine } \pi_{2} \text{ i punti appartententi alla } \textbf{linea epipolare } l \in \pi_{2}
$$
In questo modo riduciamo lo spazio di ricerca da $R^2$ a $R^1$.

### Algoritmi

#### Correlazione

Ricerca di pattern tra le due immagini (segnali).

**Rettifica** delle immagini per fare stereoscopia, ovvero modifica delle immagini per avere le camere parallele (TODO chiedere linee epipolari?). 
Viene più facile ricercare le corrispondenze.

Cerco scostamento del punto della primaria se lo immergo nella secondaria per trovare il suo corrispondente. Questo scostamento è chiamato **disparità**.

Diparità sparsa vs densa (pixel vs feature) TODO CHIEDERE COME FUNZIONA DENSA.

C'è anche il problema **foreshortening**, lo stesso pezzo di mondo può apparire di dimensioni diverse a seconda della prospettiva, quindi non posso basarmi solo su disparita x,y,z ma andrebbe presa in considerazione anche il cambio di dimensioni.

Regione $R(P_l)$ nel piano $r$ in cui vado a cercare il punto $P_l$ del piano $l$.
Questa regione si trova sulla linee epipolare.

Se da $P_l$ vado alle stesse coordinate nell'immagine $I_r$ e sommo la disparità $P_l$.
$\forall d(P_l) \in R(P_l)$ calcolo quanto vale la funzione che dice quanto sono simili i pixel, funzione $\psi(u,v)$ (u e v sono pixel).
Esistono diverse funzioni come crosscorrelazione, somma valori assoluti, somma quadrati...

In generale viene calcolata cifra di merito 
$$
c(d) = \sum^W_{k=-W} \sum^W_{l=-W} \psi(I_l(i+k, j+l),I_r(i+k - d_1, j+l -d_2))
$$

con $W$ dimensione finestra della regione di interesse.

La funzione $\psi$ può essere:

- crosscorrelazione $(u \cdot v)$
- SSD, sum of squared differencies: $-(u-v)^2$
- SAD, sum of absolute differencies (più veloce da calcolare)

Quanto deve essere grande la finestra? Abbastanza da trovare qualcosa di riconoscibile nel segnale. 
Fino a ora consideravamo W uguale per altezza e larghezza, ma è una semplificazione, possiamo avere dimensioni diverse.

#### Analisi multirisoluzione

Presa un'immagine posso applicarci un filtro passabasso e ottengo un'immagine derivata. 
Ottengo un'immagine con meno "dettagli" (vengono tagliate le alte frequenze). 
Posso applicare su questa nuova immagine un altro filtro passabasso e così via.

L'insieme di queste immagini è chiamato lo *scale space*

Posso partire da un'immagine con molte frequenze tagliate, in quanto c'è meno segnale e quindi ho meno "cose" che posso associare.
Prendo i risultati che ottengo ad una scala alta come base per vincolare la ricerca ad una scala più bassa. TODO ho capito bene?

**Discontinuity preserving**: i filtri passabassi gaussiani non garantiscono che la posizione dei "bordi" rimanga la stessa nelle varie immagini.
Esistono alcuni algoritmi che sono in grado di farlo: anisotropic diffusion, steerable filters.


