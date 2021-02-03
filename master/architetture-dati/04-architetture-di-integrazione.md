# Architetture di integrazione

Integrazione -> Unire in qualche modo diversi dataset.

Distinguiamo:

- data integration: diversi set di dati con attributi diversi. costruisco unico insieme con tutti gli elementi dei due insiemi.

- data enrichment: arricchire un set di dati con alcuni dati di altri insiemi, qualora possibile.

## Architetture per data integration

Due tecniche:

- Consolidation: raccolgo dataset, li integro e li salvo in un nuovo db, che sarà la nuova architettura dati

- Virtual Data Integration: non memorizzo i risultati dell'integrazione ma dò la possibilità agli utenti di fare query sui dati integrati. Si produce quindi un nuovo schema globale che comunica tramite un mediatore software per prendere i dati dai db "vecchi".

Due approcci:

- integrated read-only views (Mediation): integrazione solo in lettura

- integrated read-write views (mediation with update): difficile e poco studiata.

Tre elementi fondamentali in un'architettura di data integration:

- Global Schema

- Varie sorgenti

- Mapping tra sorgenti e GS

Due componenti fondamentali:

- mediator: data una query la frammenta e la riscrive per poter lavorare sugli schemi locali. Inoltre mette insieme i vari risultati, risolve i conflitti e risponde alle query

- vari wrapper: agganciano ogni schema locale al GS, rappresentando la sorgente in uno schema compatibile con GS.

Approcci per costruire il Global Scheme:

- GAV (Global As View): creo schema globale sulla base dell'osservazione degli schemi sorgente.

- LAV (Local As View): lo schema globale viene progettato a priori indipendentemente dagli schemi locali, dai quali verranno prese soltanto le informazioni di interesse.

- GLAV (Global and Local As View): mapping dato da insieme di viste, alcune sullo schema globale altre sulle sorgenti.

## Data integration

Nell'unire due (o più) dataset possono essere presenti conflitti/eterogeneità:

- eterogeneità di nome

- eterogeneità di tipo

- eterogeneità di modello

### Eterogeneità di nome

Diverse situazioni:

- sinonimia: rappresento stesso concetto con nome diversi, che sono sinonimi. Sintassi diversa, semantica uguale.

- omonimia: concetti diversi con gli stessi nomi. Sintassi uguale, semantica diversa. Caso più difficile da riconoscere.

- iperonimia: tra i due concetti uno è più altro di livello rispetto all'altro, come in una relazione IS-A

In fase di progettazione dello schema integrato devo riconoscere e gestire questi casi.

### Eterogeneità di tipo

Stesso concetto rappresentato in modo strutturalmente diverso nei due schemi:

- domini di definizione differenti per lo stesso attributo in due schemi

- attributo in uno schema dipendente funzionalmente da un attributo nell'altro schema

- attributo in uno schema che è entità nell'altro schema

- attributo in uno schema che è una gerarchia di generalizzazione in un altro schema

- entità in uno schema che è una relazione in un altro schema

- diversi livelli di astrazione per lo stesso concetto in due schemi

- diverse granularità nei domini di definizione

- diverse cardinalità nelle stesse relazioni

- conflitti sulla chiave primaria

### Data integration system

Abbiamo quindi una trasformazione di schema.

Si fa schema matching per capire come unificare i vari schemi.

Si procede poi con l'integrazione vera e propria.

Il software che gestisce queste fasi si chiama data integration system.

Fasi:

- schema trasformation (o pre-integration): prende n schemi e li restituisce omogenei in base a tecniche di model trasformation o reverse engineering.

- correspondences investigation: 

- schema integration e mapping generation

Due strategie fondamentali:

- Integrare a coppie:
  
  - prendo schema 1, lo integro con schema2, integro il risultato con schema3 e così via, ottenendo albero binario sblianciato.
  
  - approccio bilanciato aggregando schemi "vicini"

- Integrare più schemi contemporaneamente:
  
  - integrare tutti gli schemi insieme (brutto, da evitare)
  
  - integrare in modo iterativo, in modo analogo all'approccio binario bilanciato, tenendo comunque basso il numero di schemi da integrare a ogni iterazione.

Si cercano corrispondenze semantiche. Sfruttiamo equivalenze e generalità.

Diversi tipi di conflitti:

- conflitti di classificazione: quando elementi omologhi descrivono insiemi diversi di oggetti del mondo reale. si risolve tramite generalizzazione o specifica della gerarchia.

- conflitti descrittivi: tipi omologhi hanno proprietà diverse o le stesse proprietà descritte diversamente:
  
  - conflitti di nome: nomi diversi per stesse cose
  
  - conflitti di composizioni: diversi attributi

- conflitti strutturali: stessi elementi rappresentati da strutture diverse. Scelgo la struttura "con più cose".

- conflitti di frammentazione: se stesso elemento in uno schema è in un'entità unica e in un altro schema è diviso in più entità. Si risolve aggregando tutto nell'elemento "unico".

Conflitti a livello di istanza:

- conflitti di attributi: ho stesso attributo con due valori diversi. posso usare soluzione **currency**: scelgo il valore temporalmente inserito per ultimo.

- conflitti di chiave.

La risoluzione dei conflitti a livello di istanza di può fare o a design time o a query time. Si hanno funzioni di risoluzione dei conflitti che cercano, dati due valori conflittuali, di restituire quello più probabile. Un criterio di misura può essere l'affidabilità delle sorgenti. 

Due tipi di soluzioni per le istanze:

- deduplication: integrazione dati nella stessa tabella (ovvero se ci sono dati duplicati nella stessa tabella capire cosa farci).

- integrazione dei dati in più tabelle

**Record linkage**: tecnica di risoluzione dei conflitti a livello di istanza. Date le tabelle in input posso avere in output:

- matching tuples: dati che sicuramente matchano (anche se non perfetti, giudicati "match" secondo delle soglie di valutazione)

- non matching tuples

- possible matching tuples: non so dare risposta certa.

La risoluzione dell'ultimo caso viene fatta da un umano anche se da qualche anno vengono studiate tecniche di ML.

Per confrontare i vari attributi delle tabelle dobbiamo ridurre lo spazio di ricerca (fare il prodotto cartesiano non è efficiente). Si hanno **blocking methods** per ridurre lo spazio di ricerca. Una volta ridotto si applica un modello di decisione per il check. 

Quindi per il record linkage si ha:

- preprocessing: normalizzazione dei dati secondo uno standard

- blocking: riduzione spazio di ricerca. Una di queste tecniche è il **sorted neighbour** ovvero sceglie una chiave, ordina in base alla chiave e poi confronta i record con una finestra mobile.

- compare: si sceglie una funzione di distanza e soglie

- decide. valuta distanza e soglie

Per la fusione si può quindi:

- ignorare il conflitto, mettendo tutti i valori disponibili

- cercare di evitare i conflitti basandosi su metadati, sorgente o istanze

- gestire i conflitti tramite funzioni di risoluzione dei conflitti




