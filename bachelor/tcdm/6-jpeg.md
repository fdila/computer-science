# JPEG

## Compressione jpeg

Compressione immagini fotografiche.

Pipeline algoritmo compressione:

- Conversione spazio colore (compressione su componenti cromatiche sottocampionando 4:2:0)

- Suddivisione in blocchi 8x8 di ciascun canale

- Per ogni blocco faccio DCT

- Comprimo coefficienti

- Leggo a zig-zag coefficienti e metto in vettore

- Per i primo valore uso DPCM, per gli altri RLE, poi posso usare huffman

**Conversione spazio colore** Si usa di solito sottocampionamento 4:2:0  (ho perdita)

**Suddivisione in blocchi** 8x8

**Applico DCT** da un blocco 8x8 ottengo 8x8 coefficienti, il primo coefficiente in alto a sinistra è la componente continua.

**Quantizzazione coefficienti DCT** ho tabelle di quantizzazione Q. 

$$
\hat{F}(u,v) = round(F(u,v)/Q(u,v))
$$

F hat è la tabella dei coefficienti quantizzati. Per ricostruire moltiplico F hat * Q



## Compressione jpeg 2000

NO DCT, basato su Wavelet.
Non lavora su blocchetti. Sfrutta analisi multirisoluzione.

- Scomposizione wavelet a 3 livelli.

- Artefatto blurrato

jpeg2k ha fallito. soggettivamente non è migliore di jpeg.
Può introdurre regioni di interesse per specificare regioni su cui comprimere meno.
