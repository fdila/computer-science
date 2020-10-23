# Immagini

L'occhio è fatto di coni e bastoncelli. Ci sono tre tipi di coni (un tipo per R (onde lunghe) uno per G(medie) uno per B(corte)). I bastoncelli entrano in gioco quando c'è poca luce e tutto è rappresentato da toni di grigio. Abbiamo più bastoncelli che coni, siamo più sensibili alle variazioni di luminanza che di crominanza.

**Risposta tristimolo** i coni proiettano in uno spazio a 3 dimensioni la risposta allo stimolo che gli giunge da un oggetto illuminto. Ogni colore può essere descritto da 3 valori.

**Sintesi adittiva** è quella usata dall'occhio umani e dai dispositivi che imitano l'occhio umano (fotocamere e simili) RGB

**Sintesi sottrattiva** colori Cyan Magenta Yellow. Ogni filtro sottrae una parte della luce. Le superfici che ci appaiono colorate sottraggono alla nostra vision euna parte dello spettro visibile.

Alcuni modelli di colore:

- RGB, camere e videocamere

- HSB (hue saturation brightness): corrisponde alla percezione umana, anche chiamato HLS

- HSV come hsb ma con tinta definita su angolo

- CMYB (Cyan Magenta Yellow Black) utlizzato per sintesi sottrattiva nei sistemi di riproduzione

Modelli di colore per video:

- YIQ segnale TV in north america e giappone

- YUV in europa

- YCbCr usato in video digitali

Formati grafici: tecnologia per memorizzare l'immagine. Due tipologie:

- Immagini scalari o raster, definite su griglia di pixel

- Immagini vettoriali, rappresentate da formule matematiche

Per immagini raster:

- **campionamento** numero di pixel (NON RISOLUZIONE)

- **quantizzazione** bpp bit per pixel (profondità colore/livelli grigio)

**Risoluzione** pixel per inches. 

**Quantizzazione cromatica**:

- B/N 1 bit 2 colori

- livelli di grigio/colormap 8 bit

- TRUE COLOR 24 bit

**Range dinamico** intervallo tra ampiezza massima e minima del segnale. Legato al numero di bit impiegato. È legato al concetto di contrasto. Le foto hanno solitamente basso range dinamico se vogliamo **HDR** alto range dinamico, "fondiamo" più immagini.

**Istogramma** N di campioni per livelli di grigio

**Dithering**: se il dispositivo di output ha una profondità di colore inferiore all'immagine. Es se ho un'immagine a livelli di grigio e devo stamparla in bn divido in blocchi da riempire con diversi pattern cos' da simulare i livelli di grigio. È anche utilizzato per introdurre rumore ad alta frequenza in un immagine, in modo tale che il rumore di quantizzazione sia meno sgradevole dal punto di vista percettivo.
