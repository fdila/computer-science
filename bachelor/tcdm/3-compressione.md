# Compressione

Due tipi di compressione: **error-free(loss less)** e **lossy**.

**Rapporto di compressione**: $C=b_1/b_2$ con b1 n di bit per rappresentare prima della compressione e b2 bit per rappresentare dopo la compressione.

**Ridondanza relativa** = $R = 1 - (1/C)$ 

Tre tipi di ridondanza:

- Ridondanza della codifica

- Ridondanza spaziale (o temporale)

- Ridondanza percettiva

I primi due tipi sono ridondanza statistica.

## **Ridondanza della codifica:**

Minimizziamo il numero di bit per codificare i livelli attraverso codifica a lunghezza variabile **VLC Variable-Length Coding**. Ho un numero minori di bit per rappresentare i livelli più probabili e viceversa. Tecnica di tipo loss-less.

**Entropia**: misura il numero medio minimo di simboli binari necessari a codificare il messaggio. Misura il grado di incertezza della sorgente. 

**Codifica di Huffman**. è un VLC, ai caratteri più frequanti viene associato un codice di pochi bit e viceversa. Il codice da associare può essere determinato costruendo una struttura ad albero binario sulla base della frequenza dei singoli caratteri. Minimizza numero di bit medi per codice in modo da farlo essere più vicino possibile all'entropia della sorgente.

## Ridondanza spaziale:

**Run Lenght Encoding** quando c'è correlazione spaziale. Se ad esempio in un'immagine ho 10 pixel uguali di fila memorizzerò il valore del pixel e poi quante volte è ripetuto. Metodo lossless.

**DPCM**: Differential coding. Nel PCM al posto che memorizzare il valore assoluto memorizzo la differenza con il campione precedente.

Il differential coding si può usare anche sulle immagini.

## Algoritmi lossless universali

Modellano dinamicamente le caratteristiche statistiche dei dati e adeguano la codifica di conseguenza:

- Adaptive Huffman Coding -> rimuove solo ridondanza di codifca

- Algoritmi Lempel-Ziv (gzip, pkzip) -> rimuove sia ridond. codifica che spaziale

- Arithmetic Coding

## Codifica video: inter frames

C'è ridondanza anche tra un frame e l'altro di un video, sfrutto ridondanza temporale per comprimere.

## **Ridondanza percettiva:**

In base alla percezione umana. C'è perdita, lossy.

Non tutta l'informazione ha la stessa importanza per il nostro sistema percettivo

**Masking** mascheramento in frequenza, la presenza di un forte suono a una certa frequenza tende a mascherare i suoni a frequenze vicine. In corrispondenza di un segnale sonoro a una generica frequenza si ha un'alterazione della soglia di udibilità delle frequenze limitrofe, che non vengono percepite.

**Ridondanza psicovisuale** 
Legge di Weber: la sensibilità alle variazioni di luminosità diminuisce man mano che limmagine diventa più scura -> quantizzazione più grossolana nelle zone più scure.
Siamo più sensibili al rumore nelle regioni uniformi che nelle regioni ad alta frequenza
Siamo più sensibili a variazioni di luminanza che di crominanza.
