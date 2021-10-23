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

#### Algoritmi a correlazione

