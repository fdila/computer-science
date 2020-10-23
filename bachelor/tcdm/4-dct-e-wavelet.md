# DCT e Wavelet

## Trasformate

- Fourier

- DCT

- KLT

- WHT

- Wavelet

Scelta dipende da capacità di decorrelare dati, semplicità di realizzazione, minore visibilità di difetti nella ricostruzione

## DCT

Trasformata coseno discreta.
Dobbiamo scorrelare le informazioni. Scorrelando i dati riduciamo ridondanza.
Rispetto a Fourier scorrela meglio i dati. C'è solo la parte reale.
Kernel coseno.  Kernel separabile e simmetrico.  Gode di proprietà di linearità.

Il valor medio è riconducibile alla frequenza 0.

Blocchetti 8x8 per jpeg ma non ho capito.

Rispetto a fourier mi servono meno coefficienti.

## Wavelet

**Analisi multirisoluzione**: rappresentazione e analisi di segnali a diverse risoluzioni. 

Codifica per sottobande: filtro con pb e pa. e sotto campiono con passo 2. Posso fare questa roba più volte. Rispetto a righe e rispetto colonne dopo.

Prosegui in queste decomposizioni finchè hai voglia

**funzione di scala** scaling function, filtro pb

**wavelet** filtro pa

Immagine approssimata nell'angolino in alto a sinistra, poi ho tutte le alte frequenze

**analisi** passo da segnale a sottoimmagini

**sintesi** ricostruzione

Decompongo i quadrati con maggior contenuto informativo quando faccio i pacchetti di wavelet.

Si può usare per fare de-noising.
