# Audio

Il suono è un fenomeno ondulatorio come la luce.

Caratteristiche

| Parametro percettivo | Paramtero fisico | Rappresenta        |
| -------------------- | ---------------- | ------------------ |
| Altezza              | Frequenza        | Tonalità           |
| Intensità            | Ampiezza         | Volume             |
| Timbro               | Spettro          | Tipologia stumento |

**Campo di udibilità** è determinato dai valori limite di intensità e frequenza.

- il limite inferiore per l'intensità è costituito dalla soglia di udibilità,  quello superiore è la soglia del dolore

- I limiti per la frequenza sono tra 20 e 200000hz

In base alla frequenza varia anche la percezione dell'intensità, un suono a frequenze basse deve avere ampiezza maggiore per essere udito. A diverse frequenze percepiamo suoni con lo stesso volume a intensità diverse. Curve isofone.

Diverse scale rappresentazione. Scala di Mel relazione tra sensazione di altezza e frequenza, uguali differenze sulla scala di Mel corrispondono a uguali differenze percepite di tono ma non uguali differenze di frequenza.

Per il volume usiamo il dB. La misura in dB è il rapporto in scala logaritmica tra due potenze. Al denominatore per i suoni mettiamo la soglia di udibilità

Digitalizzazione suono:

Segnale analogico -> filtro pb -> adc -> dac -> interpolatore pb

**Codifica** PCM e PAM:

- PCM Pulse code modulation

- PAM Pulse amplitude modulation

PCM: campionamento, quantizzazione e codifica, per la quantizzazione per ogni valore dell'ampiezza del segnale viene assegnato un valore. C'è sia PCM lineare che non lineare.

PAM: stessa forma d'onda base, modulo l'ampiezza di questa forma

Abbiamo due orecchie -> due canali (stereo) 
