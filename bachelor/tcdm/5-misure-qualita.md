# Misure qualità

Nella codifica (non confondere con digitalizzazione) di un segnale abbiamo:

- Mapper -> ridondanza temporale/spaziale

- Quantizzatore -> ridondanza percettiva

- Codificatore di simbolo -> ridondanza di codifica

Algoritmi lossless non hanno parte di quantizzazione.

**Codifica con trasformate** 

- nel mapping prima divido immagine in sottoimmagini

- poi  mapper su ogni sottoimmagine

solitamente sottoimagini grandi 8x8

**Root Mean Square Error**   $[1/MN*\sum\sum[f^*(x,y) - f(x,y)]^2]^{1/2}$

**SNR**

Quelle sopra sono misure oggettive.

Misure full reference -> ho segnale non compresso con cui confrontare segnale compresso

Ci sono criteri soggettivi. Un'immagine con un rmse minore potrebbe essere percettivamente peggiore di una con rmse maggiore.

Perchè 8x8 blocchi? Guardiamo grafico che ha rmse su y e subimage size su x.
8 è il compromesso migliore per DCT.

Con DCT ho artefatti blocchetti

Con wavelet ho artefatti blurrati
