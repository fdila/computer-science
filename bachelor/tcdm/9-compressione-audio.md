# Compressione audio

Diminuire livelli quantizzazione e frequenza di campionamento non porta a grandi risultati.

Tecniche lossless:

- RLE compressione silenzio

- DPCM codifca entropica

Tecniche lossy:

- ADPCM Adaprive Differential Pulse Code modultation: predice valore di un campione a partire dai campioni precedenti e viene codificato l'errore di predizione quantizzando. Quantizzazione adattiva, il passo di quantizzazione dipende dalla dinamica

- Per il parlato, LPC e CELP sfruttano un modello vocale e trasmettono i parametri del modello.

Metodi di compressione basati su fenomeni psicoacustici

Per il parlato tengo frequenze tra 50Hz e 2kHz

Curve isofone: curve a pari volume percepito. Non linearità tra percezione e intensità.

Udito non ha comportamento uguale nelle varie frequenze.

**Mascheramento in frequenza** se un suono ha ampiezza alta maschera toni con frequenze limitrofe. Maggiore è la potenza del suono che maschera maggiore è la banda mascherata. In alcune bande non vale il principio di sovrapposizione degli effetti. Bande critiche: intervallo di frequenze dove non vale il principio.  25 bande.

**Mascheramento temporale**: un suono ad alta intensità satura i recettori all'interno dell'orecchio. 

Effetto di masking combinato (tempo-frequenze): in 3d

**Standard MPEG:**

1. Applica un banco di filtri per scommporre in frequenze

2. Quantizza output filtri: applica modello psicoacustico ai dati per allcoare opportunamente i bit. Mantenere il rumore della quantizzazione al di sotto della soglia di mascheramento. Trasmettere le componenti in frequenza che sono state mascherate con un numero minore di bit.

3. Codifica.

Codifica audio MPEG definito su 3 layer, compatibili: livello superiore può interpretare livello più basso.

1. Layer 1 algoritmo base di qualità abbastanza buona

2. Layer 2 maggior compressione al maggior costo di complessità di encoder e decoder

3. Layer 3 (mp3) usa sia Sub-Band-Coding  e Adaptive Transform Coding: più complesso ma la complessità è più in codifica che in decodifica.

**MPEG Coding Algorithm:**

il segnale viene diviso in 32 sottobande con dei filtri. A queste bande si applicano i fenomeni psicoacustici. 

1. Usa filtri per dividere in 32 sottobande di frequenza (filtraggio sub-band)

2. Determina per ciascuna banda il mascheramento causato dalle bande vicine applicando il modello psicoacustico scelto

3. Se la potenza di una banda è inferiore alla soglia di mascheramento, la banda mascherata non viene codificata

4. Altrimenti, determina il numero di bit necessari a rappresentare il coefficiente tale che il rumore introdotto dalla quantizzazione sia sotto l'effetto di mascheramento. Garantisce non percezione del rumore prodotto

5. Codifica con Huffman.
