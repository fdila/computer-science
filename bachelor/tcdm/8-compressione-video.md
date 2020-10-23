# Compressione video

Campionamento sia spaziale che temporale.

Riduzione ridondanza spaziale (intra-frame) e temporale (inter-frame).

Codifica predittiva.

Compensazione del moto. Ho un vettore di movimento che mi dice dove una determinata zona del frama si sposta.

- I-frame (indipendent frame o intraframe): partenza per la predizione, trattato come immagine singola

- P-frame (predictive frame): viene fatta predizione

Stima del moto:

- divido ogni frame in macroblocchi NxN, per canale intensità N=16 per canali coromatici N=8

- Il frame corrente( da codificare è chiamato traget frame)

- Il frame precedente è il reference frame

- Divido target frame in macroblocchi.

- Confronto con porzione del reference frame (non diviso in macroblocchi), cerco in una finestra di osservazione del reference frame il macroblocco del target frame

- Per ogni macroblocco stimo vettore di moto.

- stima del moto

- compensazione del moto

- calcolo dell'errore di predizione (differenza tra frame di predizione e frame target)

- Si codifica l'errore di predizione e l'errore di moto.

Motion Compensated Difference Frame: differneza tra target frame e frame predetto. Codifico questo.

Questo lavoro è fatto sul canale di intensità.

Si può lavorare con precisione di 1/2 pixel o 1/4 pixel per diminuire l'errore di predizione.

1. forward prediction: reference frame è uno dei frame precedenti

2. backward prediciotn: il reference frame è uno dei successivi

3. Se entrambi bidiractional prediction.

Ricerca del vettore di moto.

- ricerca del blocco corrispondente (block matching)

- Si prende una finestra del reference frame e si cerca il blocco lì dentro

- la misura si chiama MAD (distorsione media assoluta): distorsione media assltua tra pixel di due macroblocchi di dimensioni disallineati (i,j disallineamento). 

Ricerca esaustiva, considera tutti i pixel nella finestra di ricerca. METODO COSTOSO.

Ridondanza spaziale: probabilità di trovare blocco simile man mano che ci s allontana diminuisce in modo esponenziale all'aumentare della distanza:

- 2D logarithmic search

- Ricerca in 3 passi.

2D log search: si valuta MAD su 9 punti, si ripete centrando sul punto che da errore minore dimezzzando la finestra di ricerca a ogni passo.

Ricerca in 3 passi: approccio che sfrutta multirisoluzione: la stima iniziale avviene sul frame a risoluzione minore, da questa stima si parte per raffinare la stima alla risoluzione intermedia. Da questa si parte per la determinazione del vettore di moto finale sul frame alla risolzione massima.

Standard della codifica video digitale:

- ITU-T (sono raccomandazioni, denotati da sigla H.26x)

- ISO sigla MPEG-x

#### H.261

2 tipi di frame i-frame e p-frame

p-frame codifica predittiva forward

shift solo di un pixel

per intra frame codificati come immagine

tabelle di quantizzazione DCT: per i-frame step costante, no tabella, per p-frame valori costanti che variano in un range.

#### MPEG: struttura gerarchica dati (MPEG-1)

- Block: sottounità di codifica dimensione 8x8 pixel

- Macroblock: unità elementare di codifica 16x16 pixel

- Slice: sequenze di macroblocchi, lunghezza variabile, ogni slice è codificata/decodificata in maniera indipendenti

- Picuture

- Group Of Picture

- Sequence

- Video

In mpeg tabella di quantizzazione DCT vera per intraframe

In mpeg predizione sia forward che backward

Ogni GOP termina con un i picture o una p picture (no bidiractional picture)

La differenza di codifica è a livello di macroblocchi, ad esempio in un frame ci possono essere sia blocchi intra che blocchi predicted.

#### MPEG-2

Diversi profili e livelli

Video interlacciati e progressivi

Estensioni nella struttura dati

Frame rate

Supporta anche sottocampionamento chroma 4:2:2 e 4:4:4

7 profili con livelli diversi.

Posso codificare con field, al posto del pattern zig zag posso avere pattern alternativo che scorre righe

MPEG-2 è una codifica scalabile.

- vengono definiti contemporaneamente un layer base e uno o più layer di qualità superiore.

- Il layer base può essere codificare trasmesso e decodificato indipendentemente per fornire un video di qualità base

- La codifica/decodifica dei layer syperiori dipende dal layer base

5 tipi di scalabilità:

- SNR: layer superiore fornisce snr più alto

- Spaziale : layer superiore fornisce risoluzione spaziale maggiore

- Temporale: layer superiore fornisce frame rate più alto

- Ibrida: combinazione delle due precedenti

- Partizionamento dei dati: coefficienti DCt quantizzati divisi in partizioni

#### MPEG-3

è morto prima di nascere, rip

#### MPEG-4

Interattività basata su contenuti

Efficienza di compressione

Accesso universale

Al posto di macroblocchi ho oggetti

Non cerco macroblocchi, cerco oggetti

Descrizione scena con linguaggio particolare BIFS

Deblocking

**

- Descrivere come viene impiegata la codifica predittiva nello standard MPEG.

- Che cosa è il vettore di moto nella compressione mpeg e come viene stimato.

- Descrivere l’algoritmo di compressione video mpeg.

- Descrivere come si trova il vettore di moto nell’algoritmo mpeg. Scegliere una o più tecniche.

- Descrivere e commentare dettagliatamente i diversi ruoli dei frame nell’algoritmo mpeg

**
