# Programmazione robot

## Classificazione traiettorie

- Stop-to-stop: semplici, attuatori tipo pistoni, escursione eseguita in un colpo solo. Movimenti banali, traiettoria non pianificabile. Punti di fermo rilevati da dei fine corsa. Solo per pick and place

- Point to point: si va da un punto a un altro punto, punti nello spazio rilevati con sensori.  Punti mostrati sul campo. 

- Controllato:  controllo di ciò che succede andando da punto A a punto B. Non reagisce a imprevisti, o al massimo si ferma e dà errore

- Continuo: movimento più fluido, si fa a run time, reagisce a imprevisti

## Tipi di insegnamento

- Diretto

- Mediante simulacro

- Teleoperato

## Classificazione linguaggi

4 livelli:

- Task level -> non esiste

- Object level (RAPT, LMGEO) -> esiste per finta

- Manipulator level (AL, VAL, LM) -> istruzioni a livello del manipolatore (tipo braccio vai in punto x e lui ci va), coordinate cartesiane

- Joint level (ARM BASIC) -> istruzioni a livello dei giunti (tipo muovi giunto1 di 45deg)

## ARM BASIC

- STEP D(velocità), J1,J2 ... J6

- CLOSE [D] chiudi a velocità D

- SET [D] cambia in modalità manuale 

- RESET [D] modalità automatica, resetta robot

- READ V1,V2.... legge sensori

- ARM N seleziona il braccio

## AL

### SCALAR, VECTOR, ROT

- SCALAR  S1; S1 <- 2.3; ci sono anche le unità di misura
  
  - DISTANCE SCALAR D1; D1<-5.0*inches

- VECTOR array di 3 scalari, rappresentati da x,y,z
  
  - V1 <- VECTOR(0,0,1)
  
  - ci sono vettori predefiniti xhat, yhat, zhat, nilvect
  
  - |V1| lunghezza vettore

- ROT 
  
  - R1 <- ROT(xhat, 90*deg)
  
  - VR <- AXIS(R1) estrae asse rotazione
  
  - S <- |R1| estrae angolo di rotazione
  
  - rotazione predefinita nilrot, attorno a z di 0 gradi

### FRAME, TRANS

- FRAME sistema di riferimento
  
  - F1 <- FRAME(ROT(..), vettoreposizione)
  
  - frame base Station
  
  - barm frame del braccio blu
  
  - V2 <- V WRT F1 (v2 è v nelle coordinate f1)

- TRANS trasformazione tra due frame
  
  - TRANS T1
  
  - T1 <- F1->F2 trasformazione da f1 a f2
  
  - T1 <- TRANS(ROT(), VECTOR())
  
  In pratica sono la stessa roba

### Blocco BEGIN-END

Stessa roba delle graffe in C

### MOVE, OPEN, CLOSE, CENTER

- MOVE arm TO pos;

- OPEN hand [TO scalare]

- CLOSE hand [TO scalare]

- CENTER arm;  per centrare su oggetto

### Pick-and-place

Argomento orale

Chiudo

Mi alzo

Mi sposto

Scendo
Apro

Mi rialzo

### MOVE con APPROACH, DEPARTURE, VIA points, DURATION

- MOVE arm TO pose
  
  - WITH APPROACH = a (vettore)
  
  - WITH DEPARTURE = d (vettore)
  
  - VIA punti intermedi da cui deve passare
  
  - DURATION secondi

### Mattone nel forno

vabe dai, pick and place + via points

### AFFIX, UNFIX

Relazioni tra frame.

- AFFIX
  
  - AFFIX f1 TO f2 RIGIDLY
  
  - se sposto f1 si sposta anche f2
  
  - AFFIX f1 TO f2 NON RIGIDLY
  
  - non collegati rigidamente, non si spostano

- UNFIX
  
  - UNFIX f1 FROM f2

Otteneniamo un albero delle trasformazioni

### Mondo a blocchi, impilazione due cubi

blocco1_top, blocco1_center etc... come frame

AFFIX tra i frame dei blocchi

AFFIX tra braccio e blocco quando lo prendo in mano

UNFIX quando deposito il blocco.
Posso fare MOVE su blocco una volta che l'ho affixato.

### Controllo in forza, istruzioni ON-DO, FORCE, TORQUE, STIFFNESS

- ON cond DO action
  
  - ON FORCE(vettore) DO action
  
  - ON TORQUE(vettore) DO action
  
  - Tipo se supero un certo limite di forza/coppia ferma tutto

- WITH FORCE (vettore) = int //tipo per fare gli incastri

### Strutture di controllo (IF-THEN-ELSE, FOR-DO, WHILE-DO, DO-UNTIL) e PROCEDURE

- IF cond THEN lista_statement ELSE altra_lista

- FOR var_scal <- exp_scalare STEP exp-scalare UNTIL exp-scalare DO lista-statement;

- WHILE codn DO lista

- DO lista UNTIL condizione

- tipo PROCEDURE nome (lista parametri); body;

### Programmazione concorrente (COBEGIN-COEND) e istruzioni di sincronizzazione (EVENT, WAIT, SIGNAL)

Multitasking. Processi paralleli.

```bash
COBEGIN

    BEGIN

    ...

    END

    BEGIN

    ...

    END

COEND
```

I due blocchi BEGIN sono eseguiti in parallelo

EVENT E1, variabile semaforo

SIGNAL E1

WAIT E1, aspetta signal di e1

### Es passaggio pezzo tra bracci

bracci fanno cose, programmazione concorrente.

### 
