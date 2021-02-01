# NoSQL

Modello relazionale pro:

- modello ben definito

- principio closed world assumption (tutto quello che mi serve è presente nello schemad del db)

- 35 anni di sviluppo su sicurezza, ottimizzazione e standardizzazione

- ben conosciuto

Modello relazionale contro:

- principio closed world assumption non è più valido ai giorni d'oggi

- non compatibile con linguaggi programmazione moderni (ci sono framework ORM come spring ma hanno comunque problemi)

- difficile modificare schema del db

- garantire ACID è molto costoso e dopo un certo punto di espansione è praticamente impossibile economicamente fare grandi sistemi distribuiti (problema scalabilità)

- il time in market delle applicazioni si è ridotto portando a rendere obsoleto il processo di integrazione di rdbms. Anche il time to market si è ridotto.

## Modelli NoSQL

3 caratteristiche fondamentali:

- tutti i modelli sono **schema free**

- tutti i DBMS NoSQL usano il **CAP theorem**

- Si passa da ACID a BASE.

###### Schema free

Nel modello relazionale definiamo prima di tutto il modello e poi popoliamo coi dati. Con NoSQL abbiamo un'architettura tale per cui il modello è basato sui dati, quindi potenzialmente ogni record ha uno schema diverso. Si ha **open world assumption**. Molta flessibilità ma costo dal punto di vista query.

###### CAP theorem

Preso un sistema distribuito di nodi si considerano 3 aspetti:

- Consistency: tutti i nodi abbiano gli stessi dati nello stesso istante (garantisce che tutti i client hanno sempre la stessa vista sui dati)

- Availability: garanzia che ogni richiesta ricevuta dal sistema riceva una risposta, sia in caso di fallimento che di successo. (garantisce che un client puà sempre leggere/scrivere)

- Partition Tolerance: il sistema deve continuare ad operare anche se si hanno perdite di messaggi o fallimenti di parti del sistema. (garantisce che il sistema continui a funzionare nonostante partizioni fisiche della rete)

Il teorema garantisce che tra queste 3 caratteristiche, in un sistema distribuito, se ne possano avere contemporaneamente 2 soddisfatte, mai 3.

I sistemi NoSQL sono tipicamente divisi in:

- Sistemi CP (garantiscono consistenza e partition tolerance)

- Sistemi AP (garantiscono availability e partition tolerance)

###### BASE

Acronimo sta per:

- Basic Available: la risposta viene sempre data anche in caso di consistenza parziale

- Soft state: si rinuncia al concetto di consistenza di ACID (ovvero rispettare vincoli di integrità su db)

- Eventual consistency: prima o poi i dati convergeranno ad uno stato di consistenza.

## Document based system

Abbiamo una chiave, object identifier, che può essere indicizzata tramite meccanismo di hashing. Documenti memorizzati solitamente in file json o xml.

Possiamo vedere un db documentale come un albero. Concetto di "elemento più importante degli altri".

Caratteristiche:

- multidimensionale, ad albero

- ogni campo può contenere zero valori, un valore, più valori o altri documenti.

- si possono effettuare query ad ogni campo e in ogni livello

- lo schema è flessibile, due documenti nella stessa collezione possono avere schema diverso

- posso aggiungere "in linea" nuove info

- non devo fare join avendo una serie di documenti dentro documenti.

Due tecniche principali per mettere in relazione le cose:

- Referencing: come modello relazionale, si mettono in relazione due documenti tramite un attributo.

- Embedding: aggiungere all'interno del documento stesso l'altro documento con le info necessarie.

Terminologia RDBMS vs documentale:

- tabella <-> collezione

- riga <-> documento

- colonna <-> chiave

### MongoDB

DBMS documentale con dati memorizzati in binary json (bson).

Embedding è più performante.

Possono esserci indici.

###### Repliche in MongoDB

Mongo rientra nella categoria CP, non garantisce disponibilità in caso di guasto.

La replica si ha in modalità master-slave, nel gergo di mongo si dice **primary-secondary**. Tutte le scritture si fanno su primario e poi vanno su secondari.

Replica parziale e incrementale: inizialmente sync che prende tutti i dati, poi prende dai file di log le operazioni.

Garanzia tolleranza grazie a meccanismo di elezione dei nodi nel caso il primary vada down.

Un nodo può assumere uno dei seguenti stati:

- STARTUP: nodo che non è membro di nessun replica set.

- PRIMARY: unico nodo nel replica set che accetterà le operazioni di scrittura

- SECONDARY: possono ricevere copie dei dati (possono essere eletti primary)

- RECOVERING: nodo che sta effettuando operazione di recupero dei dati (può essere eletto primary?)

- STARTUP2: appena entrato in un set (può essere eletto primary?)

- ARBITRER: prende parte alle elezioni per promuovere un nodo a primary

- DOWN: nodo irraggiungibile

- ROLLBACK: un nodo che sta svolgendo rollback per cui sarà inutilizzabile per le letture (può essere eletto primary?)

Meccanismo di elezione:

- ogni replica manda un heartbeat agli altri nodi

- ogni nodo ha un id

- se un nodo non sente l'heartbeat del master viene indetta elezione

-  livelli di priorità sui secondary

- il nodo in cima viene eletto primary

###### Scrittura

Scrivo solo su primario

Opzione **writeConcern** per indicare al sistema il comportamento del replica set:

- w, numero di nodi in cui il dato deve essere replicato prima di concludere l'operazione

- j, intenzione di scrivere sui log di WT prima che operazione sia eseguita.

- wtimeout, tempo limite da aspettare nel caso in cui w sia maggiore di 0

###### Frammentazione

Meccanismo di sharding, scalabilità orizzontale

3 tipi di sharding per scalabilità orizzontale:

- hash-based, su chiave

- range-based, in base ad un certo range di elementi

- tag-aware, in base a certi attributi

Meccanismo dinamico

Ruoli:

- mongos: entry point, decompone query

- config server: riconosce struttura shard per sapere dove sono i vari documenti

- shard: hanno i dati.

Sia shard che config server sono replicati.

Nel caso di query su un solo shard si parla di target query, su più shard di broadcast query.

Primary shard: contiene tutto il db

Secondary shard: contengono frammenti e repliche

###### Lettura

Opzione readConcern:

- Local: la lettura viene effettuata sul nodo più vicino, senza verificare che il dato è stato scritto sul resto dei nodi

- Available: default per leggere dai nodi secondari

- Majority: quando la metà più uno delle repliche ha ricevuto un ack in scrittura sul dato.

###### Transazioni

Usa motore Wired Tiger

Uso lock ??

- shared (S) per le letture

- exclusive (X) per le scritture

- intent shared

- intent exclusive



CouchDB esiste, e poco altro.

## Graph DB


