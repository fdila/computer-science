# Data Quality

Definizioni varie ed eventuali:

- utilità: precisione della rappresentazione interna del dato rispetto al compito svolto

- fedeltà: aderenza del dato alla realtà

- qualità: caratteristiche di un artefatto che influiscono sulla sua capacità di soddisfare le esigenze e le aspettative dell'utente. Un dato è di qualità se è adatto all'uso che se ne deve fare -> fitness for use

- dimensione (o caratteristica): caratteristica specifica che descrive la qualità delle informazioni, a volte è misurabile

- sottodimensioni: sotto caratteristiche che spesso classificano una certa dimensione

Se le dimensioni sono misurabili ci sono delle metriche per farlo.

Le metriche sono un insieme di procedure che comprende:

- una procedura (o metodo) di misurazione

- una corretta unità di misura

Ci sono metriche:

- oggettive: modi formali e precisi per misurare le metriche per dimensione di qualità in termini di valori di un dominio, indipendenti da percezione/valutazione umana

- soggettive: dipendono dalla percezione/valutazione umana.

**Accuratezza:** vicinanza tra un valore v e un valore v' considerato come la corretta rappresentazione del fenomeno del mondo reale che v intende rappresentare

- accuratezza sintattica

- accuratezza semantica

Su stringhe si può valutare accuratezza con distanza di edit (normalizzata e non).

**Completezza**: copertura con la quale il fenomeno osservato è rappresentato nell'insieme dei dati. Nel mondo NoSQL difficile visto che non abbiamo un "mondo chiuso".

**Currency**: misura con quale rapidità i dati sono aggiornati rispetto al corrispondente evento nel mondo reale.

**Tempestività**: misura quanto i dati sono aggiornati rispetto ad un particolare processo che li utilizza.

**Consistenza**:

- consistenza con i vincoli di integrità o dipendenze funzionali definiti sullo schema. 

- consistenza delle diverse rappresentazioni di uno stesso oggetto della realtà presenti nella base di dati.

**Accessibilità**: capacità di un utente di accedere ai dati.

## Quality improvement

### Record linkage

### Data fusion




