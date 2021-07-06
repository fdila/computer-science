# Data Quality

Definizioni varie ed eventuali:

- **utilità**: precisione della rappresentazione interna del dato rispetto al compito svolto

- **fedeltà**: aderenza del dato alla realtà

- **qualità**: caratteristiche di un artefatto che influiscono sulla sua capacità di soddisfare le esigenze e le aspettative dell'utente. Un dato è di qualità se è adatto all'uso che se ne deve fare -> fitness for use

- **dimensione** (o caratteristica): caratteristica specifica che descrive la qualità delle informazioni, a volte è misurabile

- **sottodimensioni**: sotto caratteristiche che spesso classificano una certa dimensione

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

Su stringhe si può valutare accuratezza con distanza di edit (normalizzata e non), tipo distanza di Hamming.

Per stringhe fatte da più stringhe abbiamo distanza di token, come Jaccard index.

**Completezza**: copertura con la quale il fenomeno osservato è rappresentato nell'insieme dei dati. Guardiamo quanti NULL ci sono (rispetto a tuple, attributi, tabelle). Nel mondo NoSQL difficile visto che non abbiamo un "mondo chiuso".

**Currency**: misura con quale rapidità i dati sono aggiornati rispetto al corrispondente evento nel mondo reale.

**Tempestività**: misura quanto i dati sono aggiornati rispetto ad un particolare processo che li utilizza.

**Consistenza**:

- consistenza con i vincoli di integrità o dipendenze funzionali definiti sullo schema. 

- consistenza delle diverse rappresentazioni di uno stesso oggetto della realtà presenti nella base di dati.

**Accessibilità**: capacità di un utente di accedere ai dati.

## Quality improvement

Fase prima si chiama **Quality assestment**, nella fase di **quality improvement** miglioriami i dati.

Due strategie:

- Data-driven: miglioriamo i dati stessi modificando i valori con altri dati ritenuti di buona qualità. Varie procedure:
  
  - acquisizione di nuovi dati
  
  - record linkage, identificazione degli oggetti. confronta i dataset con una fonte certificata identificando tuple che possono far riferimento a quelle del dataset
  
  - affidabilità della fonte, selezioniamo fonti dati in base  a qualità

- Process-driven: miglioriamo il processo di acquisizione dei dati. Ambito Business Process Reengineering, riprogettiamo i processi. Due tecniche:
  
  - process control: si aggiungono procedure di controllo nel processo di produzione dati.
  
  - process redisign: si ridisegnano i processi per rimuovere le cause della scarsa qualità.

Approfondiamo data-driven. Si hanno miglioramenti specifici per la dimensione:

- accuratezza tramite confronto dei valori con un dominio di riferimento

- completezza tramite completamento dei dati incompleti con tecniche specifiche che sfruttano la conoscenza sui dati.

- consistenza tramite l'identificazione dei dati corretti sfruttando vincoli di integrità, dipendenze funzionali etc, correggendo poi tramite sorgenti esterni  o acquisendo nuovamente i dati.

Si usano anche tecniche di **Error localization and correction** che identifica ed elimina gli errori di qualità rilevando valori che non soddisfano un determinato insieme di regole, dette **edits**.

Un altra tecnica è la **deduplica**; che corrisponde al raggruppamento di record di dataset che si riferiscono alla stessa entità del mondo reale.

Altra tecnica (applicata all'inizio di tutto) è la **normalizzazione** per standardizzare i tipi, le stringhe etc. Ho tabelle di riferimento.

### Record linkage

Diverse varianti:

- deduplicazione: considera solo una tabella ed è usata principalmente con modello relazionale.

- record linkage: matchiamo tra due (o più) archivi di dati

- canonicalizzazione: fornisce il record più completo, attribuisce i valori tramite la fusione costruendo dei single version of truth, usando metodi probabilistici

- referencing: detto anche entity disambiguation, si matchano record sporchi con uno pulito

Varie tecniche per la comparazione di coppie:

- empirica: basata sulla distanza di simboli nei valori delle tuple

- probabilistica: presumo di conoscere un campione di frequenze di distanze tra coppie di tuple, note come corrispondenti o non corrispondenti. Si usano soglie per match e mismatch

- knowledge based: si decide in base a regole di match

- mista: sia probabilistica che knowledge based

- tecniche di ML

Vari step:

- costruzione spazio di ricerca come prodotto cartesiano delle tuple.

- tecniche di blocking per ridurre lo spazio di ricerca (sorted neighbor, vedi integrazione dati che è la stessa cosa)

- su spazio ridotto si usa un metodo di comparazione e un metodo di decisione associato.

### Data fusion

Dobbiamo fondere i record una volta che troviamo i match.

Varie tecniche di gestione dei conflitti:

- ignorare il conflitto: non è una buona soluzione. Esempio Pass It On che presenta tutti i valori.

- evitare il conflitto: scelgo di prendere istanze senza conflitti. Scelgo una fonte bella è tengo quella, strategia Trust Your Friend

- risolvere il conflitto: prendo una sorgente più sicura, considero dati e metadati prima di risolvere il conflitto. Due strategie:
  
  - decidere di tenere un valore tra quelli in conflitto (ad esempio tengo il dato più recente)
  
  - strategie di mediazione: scelgo un valore che non necessariamente esiste tra i valori inconsistenti.

La scelta deve essere comunicata a chi userà i dati. Questo è il tema della provenance dei dati, tenere traccia delle decisioni prese.

Con la **data preparation** facciamo cose:

- data normalization (tipo convertire tutte le stringhe in lowercase)

- schema normalization (tipo matchare attributi che rappresentano stessa cosa)

- imputation: fase di decisione (dove capiamo come gestire NULL ad esempio)

#### Data conflict

Tipi di conflitti:

- intra-source: stessa informazione nello stesso sorgente rappresentata in modo diverso

- inter-source: stessa informazione in sorgenti diversi.

Varie tecniche:

- usare una tabella di riferimento

- standardizzare e trasformare i dati secondo un unico standard

- sfruttare la conoscenza del dominio

- fare outlier detection e eliminare gli errori.

Step del processo di integrazione:

- schema mapping, si fa una sorta di schema integration

- data transformation, standardizzazione

- duplicate detection

- data fusion
