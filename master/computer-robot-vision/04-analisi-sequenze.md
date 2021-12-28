# Analisi di sequenze di immagini

Oltre al campionamento spaziale/intensità abbiamo anche il campionamento temporale.

In generale gli spostamenti di tempo sono piccoli (alta frequenza di campionamento temporale)

Il movimento di un punto in una sequenza di immagini può essere causato:
- dal movimento dell'oggetto nella scena
- dal movimento della camera
- entrambi

Ricerca corrispondenze facilitata dall'ampia frequenza di campionamento temporale.
La "baseline" è piccola, la qualità di ricostruzione è pessima se guardiamo solo due dati immagini consecutivi.

**Structure from motion**

Come in stereo abbiamo 2 classi di metodi:

- metodi differenziali (quello che era gray level/denso in stereo): fornisce info per ogni punto nell'immagine
- metodi matching (analogo di feature based)

**Time to impact**: da sequenza troviamo il tempo mancante per andare a sbattere contro un certo ostacolo andando a guardare come varia la dimensione dell'ostacolo.

