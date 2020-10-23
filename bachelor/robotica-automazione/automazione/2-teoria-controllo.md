# Teoria del controllo

Sistemi di controllo retroazionati

Stimatore per stimare stato x da output y, posso farlo solo se processo è osservabile.

Solo se sistema lineare controllabile e osservabile posso fare controllore lineare.

Sistema canonico di Lur'E (lurie)

Requisiti:

- Stabilità
  
  - Stabilità in condizioni nominali: asintotica stabilità 
  
  - Stabilità in condizioni perturbate: stabilità robusta (errori di modellazione)

- Prestazioni: deve convergere al setpoint velocemente
  
  - Prestazioni statiche: in condizioni nominali a transitorio esaurito
  
  - Prestazioni dinamiche: durante il transitorio
  
  - Prestazioni in condizioni perturbate

- Moderazione variabile di controllo (non sparare i gain)

L(s) funzione di anello -> tutto meno retroazione

NON CANCELLARE POLI INSTABILI CON ZERI

FdT(s) = Y(s)/Ysegnato(s) = L(s)/(1+L(s))

$ 1+L(s) = 0 $

Funzione trasferimento di tutto il sistema != L(s)

Diagrammi di Nyquist: Fdt(s) con s che varia su cammino di nyquist. è simmetrico rispetto a asse Re.

Criterio di Nyquist: verifica as. stabilità di sistema retroazionato.

Si definiscono:

- P numero di poli di L(s) con parte reale > 0

- N numero di giri compiuti in senso antiorario da diagramma di nyquist di L(s) intorno a -1

N = P allora sistema retroazionato è stabile.

_moderazione azione di controllo_

Stabilità in condizioni perturbate--> margine di guadagno

1. mu > 0

2. P = 0

3. diagramma nyquist interseca una sola volta il semiasse reale negativo, punto (xa, 0);

4. il punto di intersezione deve stare a destra di (-1, 0)

allora possiamo definire margine guadagno: $1/|x_A|$

Il punto A corrisponde a pulsazione pi greco. 

Posso trovare margine guadagno anche su diagramma di bode. Vedo dove fase interseca -180, traccio linea retta, vedo dove interseca modulo, misuro distanza tra quello e asse.

**Margine di fase**

1. mu > 0

2. P = 0

3. interseca solo una volta circonferenza raggio unitario. punto wc 

4. |pc| < 180

wc pulsazione critica.

margine di fase = 180 - |pc|

margine di fase è spesso 60 gradi

#### criterio di bode per stabilità robusta

1. P = 0

2. Diagramma bode attraversa una sola volta asse w.

3. mu > 0

4. margine di fase > 0

Quindi no giri nel diagramma Nyquista intorno a -1

## Specifiche da dare per sistema di controllo

- Stabilità in condizioni nominali.
  
  - no zeri del controllore che cancellano poli instabili del sistema da controllare

- Precisione statica che tende a 0 (quando ho transitorio finito)

- Precisione dinamica

- Reiezione ai disturbi D e N

- Moderazione guadagno

- Regolatore deve essere realizzabile 

- attenzione alla potenza (limiti fisici del sistema)

- non deve avere troppi poli/zeri

### Progettazione

Ho parte statica R1 e parte dinamica R2

Parte statica easy, guarda le tabelle

Tecnica di assegnazione dei poli per R2

Specifiche:

- errore all'infinito < qualcosa

- margine di guadagno

- margine di fase

## PID
