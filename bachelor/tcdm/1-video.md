# Video

Persistenza della visione -> movimento apparente

Movimento apparente percepito a frequenze molto basse (16 frame/sec)    

Se un pattern cambia molto più velocemente del refresh rate del nostro sistema visivo vediamo l'immagine sfocata. Se invece l'intervallo tra un frame e il successivo è troppo ampio l'immagine appare discontinua.

**Critical Flicker Frequency** frequenza temporale alla quale si passa dalla percezione di uno stimolo intermittente (flicker) alla percezione di uno stimolo continuo. Il frame rate per l'acquisizione/riproduzione di un video non deve essere inferiore alla critical flicker frequency. La cff varia tra 20hz e 80hz in base a più fattori:

- Luminosità media del display: più è luminoso più cresce la frequenza critica.

- Luminosità dell'ambiente: più l'ambiente è luminoso più cresce

- Distanza dallo schermo: più è vicino più cresce

Flash rate/ frequenza di refresh: frequenza con cui è riprodotta un'immagine sul display. Diversa da frame rate perchè comprende anche la ripetizione della stessa immagine, il frame rate indica quante nuove immagini al secondo sono trasmesse.

**Interlacciamento** In video field è un insieme di campioni di un'immagine, composto da linee alternate dell'immagine. I vari field sono campionati a istanti diversi, secondo il field rate. Immagine divisa in field pari e dispari alternati per metà tempo rispetto ai fps. In questo modo aumento la frequenza apparente e elimino flicker. In genere non è visibile ma se si riprende un'azione molto rapida si vede.

**Riproduzione del colore** ??

**Sottocampionamento croma** Il campionamento del colore è espresso come x:y:z

- x numero relativo ai campioni di luminanza

- y numero di campioni chroma per ogni linea dispari

- z numero di campioni chroma per le altre linee

4:2:0 usato per JPEG e MPEG
