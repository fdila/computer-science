# Sistemi distribuiti relazionali

Più basi di dati locali, più applicazioni su ogni nodo di elaborazione.

**Architettura shared nothing**

Tre categorie per dividere il livello di federazione (categorie tra loro indipendenti):

- autonomia

- distribuzione

- eterogeneità

**AUTONOMIA**:

Grado di indipendenza tra i nodi. Diverse forme:

- autonomia di progetto: ogni nodo ha un proprio modello dei dati e di gestione delle transazioni

- autonomia di condivisione: ogni nodo sceglie la porzione di dati da condividere ma condivide con gli altri nodi lo schema comune.

- autonomia di esecuzione: ogni nodo sceglie in che modo eseguire le transazioni.

Si hanno quindi:

- DBMS strettamente integrati con nessuna autonomia, con dati logicamente centralizzati e un unico data manager per le transazione applicative, e vari data manager che eseguono le direttive centrali

- DBMS semi-autonomi, ogni data manager è autonomo ma partecipa a transazioni globali, dove una parte dei dati è condivisa e dove sono richieste modifiche architetturali per poter far parte della federazione.

- DBMS peer-to-peer completamente autonomi, dove ogni dbms lavora autonomamente e non sa dell'esistenza degli altri.

**DISTRIBUZIONE**

3 livelli classici:

- distribuzione client/server

- distribuzione peer2peer

- nessuna distribuzione

**ETEROGENEITÀ**

Vari aspetti:

- modello dei dati

- linguaggio di query

- gestione delle transazioni

- schema concettuale e logico

Si hanno quindi vari tipi di dbms:

- DDBMS (dbms distribuito omogeneo): si ha alta distribuzione ma non autonomia ed eterogeneità

- DBMS eterogeneo logicamente integrato (data warehouse): alta eterogeneità ma non distribuzione e autonomia

- DBMS distribuiti eterogenei: alta eterogeneità e distribuzione ma non autonomia

- DBMS distribuiti federati eterogenei: alta distribuzione ed eterogeneità e semi-autonomia

- MULTI DB MS: totalmente autonomi.

## DDBMS

Tanti schemi logici e tanti schemi fisici per ogni nodo.

Approccio **Local as view (LAV)**: Tutti gli schemi si interfacciano con uno schema logico globale, ogni schema logico locale è una view del globale. 

Lo schema globale viene progettato prima di quelli locali

Step per la progettazione:

- analisi dei requisiti

- progettazione concettuale

- progettazione della distribuzione, per capire dove mettere i dati

- progettazione della logica locale, che traduce dallo schema concettuale globale allo schema logico

- progettazione fisica locale

**Portabilità**: capacità di eseguire le stesse applicazioni db su ambienti runtime diversi, la portabilità è a compile-time.

**Interoperabilità**: capacità di eseguire applicazioni che coinvolgono contemporaneamente sistemi diversi e eterogenei.

Per gestire interoperabilità vengono introdotti middleware, tra cui **ODBC**: esso si pone sopra i dbms e dà un'immagine indipendente di quello che c'è sotto, come se fosse un driver.

Si hanno anche protocolli come **X-Open Distributed Transaction Processing (DTP)** che stabiliscono una serie di API che vengono implementate da ogni singolo dbms per offrire connettività standard.

### Caratteristiche dei DDBMS

Diversi tipi di architetture:

- **shared everything**:  db manager e disco sono in unico nodo

- **shared-disk**: + db manager su stessa Storage Area Network (Oracle RAC)

- **shared-nothing**: ogni db management ha il suo disco.

Proprietà generali di un ddbms:

- **località**: tendendo i dati vicino alle applicazioni che li usano miglioriamo performance. Partizione dei dati corrisponde spesso a partizione naturale di applicazioni e utenti. I dati risiedono vicini a dove vengono usati più spesso ma sono comunque accessibili globalmente.

- **modularità**: distribuzione dinamica dei dati si adatta meglio alle esigenze delle applicazioni.

- **resistenza ai guasti**: maggior fragilità per numero di componenti che aumentano ma anche ridondanza, quindi maggior resistenza ai guasti

- **prestazioni ed efficienza**: tanti aspetti, come il parallelismo nelle operazioni, distribuzione del carico etc

Funzionalità specifiche dei ddbms:

- trasmissione di query, transazioni, frammenti di db e dati di controllo tra i nodi

- frammentazione, replicazione e trasparenza

- query processor e query plan per la previsione di una strategia globale accanto a strategie per query locali

- controllo di concorrenza

- strategie di recovery e gestione dei guasti.

**Frammentazione**: possibilità di allocare porzioni diverse del db su nodi diversi.

- frammentazione orizzontale che prevede di frammentare una tabella in base alle righe.

- frammentazione orizzontale in cui si frammenta rispetto alle colonne. in ogni chunk dovrà essere presente inoltre l'id per poter ricostruire la tabella completa.

Nella frammentazione bisogna garantire:

- completezza: ogni record nella relazione di partenza deve poter essere ritrovato in almeno uno dei frammenti

- ricostruibilità, ovvero la relazione di partenza deve poter essere ricostruita senza perdita di informazione a partire dai frammenti

- disgiunzione: ovvero ogni record della relazione r deve essere rappresentato in uno solo dei frammenti.

- replicazione: opposto di disgiunzione.

**Replicazione**: miglioramento prestazioni in lettura (vedi località), ma diversi aspetti negativi per la scrittura (gestione transazione e update di copie multiple).
Va inoltre studiato cosa replicare, quanto replicare, dove allocare le copie e come gestirle. Per l'allocazione abbiamo gli **schemi di allocazione**.

**Trasparenza**: l'applicazione non deve sapere nulla del funzionamento del db. logica applicativa separata da logica dei dati.
Le applicazioni non devono essere modificare a seguito di  cambiamenti nella definizione e organizzazione dei dati:

- trasparenza logica (indipendenza logica): indipendenza dell'applicazione da modifiche allo schema logico (se un applicazione usa un frammento e ne viene modificato un altro non viene modificata)

- trasparenza fisica

Tre livelli di trasparenza:

- trasparenza di frammentazione: permette di ignorare l'esistenza dei frammenti. il sistema converte query globali in query locali e relazioni in sottorelazioni. la scomposizione delle query per ogni sotto-relazione è detta query rewriting

- trasparenza di replicazione/allocazione: applicazione è consapevole dei frammenti ma non dei nodi su cui si trovano. La query è già spezzata.

- trasparenza di linguaggio: l'applicazione specifica sia i frammenti che i nodi, che possono offrire interfacce che non sono sql standard. Tuttavia l'applicazione sarà scritta in sql stardard a prescindere dai linguaggi locali dei nodi.

## Query distribuite

Analizziamo DDBMS shared-nothing.

### Accesso in lettura

4 fasi che compongono **query processor**:

- query decomposition

- data localization

- global query optimization

- local query optimization

**Query decomposition:** opera su schema logico globale non tenendo conto di distribuzione. Tecniche di ottimizzazione algebrica analoghe a quelle dei dbms non distribuiti. Output query tree.

**Data localization**: considera frammentazione delle tabelle e la distribuzione. Ottimizzazione delle operazioni rispetto alla frammentazione con tecniche di riduzione. Viene prodotta query efficiente per la frammentazione ma non ottimizzata.

**Global query optimization**:  si basa su statistiche sui frammenti. 
Viene arricchito query tree tramite operatori di comunicazione (send e receive) che vengono effettuati tra i nodi.  
Alcune query potranno essere eseguite in parallelo. 
Le operazioni più costose sono quelle di join.
Si hanno algoritmi di calcolo adattivi, si deve studiare la rete e i suoi ritardi.
Si ha ottimizzazione a runtime, dove si riadatta il query plan.
La distribuzione non è predicibile a priori.
Definizioni utili:

- costo di messaggio: costo fisso di spedizione o ricezione di un messaggio (detto setup)

- costo di trasmissione: costo, fisso rispetto alla topologia, di trasmissione dati

- costo di comunicazione:  costo messaggio moltiplicato per numero di messaggi + costo di trasmissione per numero di byte trasmessi.

- costo totale: somma dei costi di operazioni (I/O e cpu) + costi comunicazione

- response time: somma dei costi qualora si tenga conto del parallelismo nelle trasmissioni. Posso usare dei pesi basati sulla cardinalità delle unità da trasferire e tenere conto del massimo tempo di risposta che si ottiene.

Tendenzialmente il costo di comunicazione è il fattore critico.

Bisogna scegliere se ottimizzare:

- response time, aumentando parallelismo anche se può portare ad un aumento del costo totale.

- costo totale, senza tener conto del parallelismo, aumentando il throughput ma diminuendo il response time.

Nel trasferire i dati da un nodo all'altro perdiamo gli indici, quindi join diventa molto costoso. Definiamo l'operazione di **semijoin**: 

$$
R semijoin_A S \equiv \pi_{R^*}(Rjoin_AS)
$$

Scelgo quindi di tenere solo gli attributi di R dopo il semijoin.

**Local optimization**: ottimizzazione degli schemi locali. Ogni nodo riceve una fragment query e la ottimizza. 

### Accesso in scrittura e controllo della concorrenza

Remote transactions: query con insert/delete/update

Deve valere atomicità. Nessun problema su consistenza e durabilità. Controllo sulla concorrenza (Isolamento),

Ogni transazione è fatta da sottotransazioni e ogni sottotransazione viene eseguita da un nodo. Ogni sotto-transazione è schedulata indipendentemente da ciascun nodo. La schedule globale dipende da schedule locali.

La schedule globale è serializzabile se gli ordini di serializzazione sono gli stessi per tutti i nodi coinvolti (solo se non c'è replica).

Protocollo di controllo delle repliche: **ROWA (Read Once Write All)**. Consente lettura da qualunque copia ma scrittura va fatta su tutte copie.

#### 2 phase locking per DDBMS

due strategie:

- startegia centralizzata

- strategia primary copy

###### Strategia centralizzata

Ogni nodo ha un lock manager (LM), uno viene eletto come LM coordinatore.

Il Transaction Manager del nodo dove inizia la transazione è considerato TM coordinatore.

La transazione è anche eseguita su altri Data processor e corrispondenti nodi.

Strategia:

- TM chiede al LM i lock

- il LM li concede usando 2pl

- Il TM comunica ai Data processor

- i DP comunicano al TM e il TM al LM la fine delle operazioni.

Problema: il nodo dell'unico LM diventa collo di bottiglia.

###### Strategia primary copy 2pl

Per ogni risorsa (ho le repliche) individuo la copia primaria

La copia primaria fa da LM, un LM per ogni risorsa.

Per ogni risorsa della transazione il TM chiede i lock al LM responsabile della copia primaria, che assegna i lock.

Evitiamo bottle neck, ma introduco complicazione perchè TM deve sapere dove stanno tutti i LM, serve directory globale.

Serve comunque **controllo su deadlock** causati da attesa circolare tra due o più nodi. Gestito nei ddbms tramite time out. Definiamo un algoritmo ascincrono e distribuito (p2p) dove i singoli nodi rilevano i deadlock in giro.

Algoritmo:

- ogni nodo intregra la sequenza di attesa con le condizioni di attesa locale degli altri nodi logicamente legati da condizoni ext

- analizza le condizoni di attesa sul nodo e rileva deadlock locali

- comunica le sequenze di attesa agli altri nodi.

Per evitare che deadlock venga scoperto più volte decidiamo che il nodo i passa al nodo j le liste di deadlock solo se i>j.

Nei sistemi p2p troviamo soluzioni coreografate (si decidono prima le mosse e poi ognuno fa quel che deve) rispetto alle soluzioni orchestrate dei sistemi centralizzati.

#### Gestione dei guasti nei DDBMS

Un sistema distribuito è soggetto, oltre ai guasti locali, anche a perdita di messaggi su rete e partizionamento della rete.

Tipi di guasti e conseguenze:

- guasti dei nodi

- perdita di messaggi: lasciano l'esecuzione di un protocollo in una situazione di indecisione

- Partizionamento della rete: una transazione distribuita può essere attiva contemporaneamente su più sottoreti temporaneamente isolate.

##### Protocollo 2 phase commit.

###### versione senza guasti

- prima fase:
  
  - il TM chiede a tutti i nodi se vogliono fare commit o abort (*prepare*)
  
  - ogni nodo comunica unilateralmente la sua decisione (*ready_to_commit* o *not_ready_to_commit*)

- Seconda fase:
  
  - TM prende decisione globale (se uno vuole abort abort per tutti, altrimenti commit)
  
  - TM comunica a tutti la decisione per poter procedere con le azioni locali.

Nei **log** di ogni nodo compaiono due tipi di record:

- Record di transazione (info sulle operazioni effettuate)

- Record di sistema (evento di checkpoint e dump del db)

Prima scrivo su file di log e poi eseguo operazione.

Nuovi recordi di log su TM:

- prepare record (contiene identità di tutti i nodi e le transazioni)

- global commit o global abort (decisione globale)

- complete (alla fine del protocollo)

Nuovi record di log su RM (i nodi)

- ready record (volontà di partecipare alla fase di commit)

- not ready (indisponibilità al commit)

Gestione dei timeout:

- sia nella prima fase che nella seconda possono avvenire guasti

- in entrambe le fasi devono poter prendere decisioni connesse allo stato in cui si trovano

- avviene utilizzando timer e stabilendo un intervallo di tempo di timeout.

Quindi il protocollo diventa:

- prima fase:
  
  - TM manda prepare ai nodi e fissa timeout per ricezione risposte
  
  - i RM risponde ready/not ready
  
  - TM assume che se un nodo non risponde allora fa ABORT

- Seconda fase:
  
  - TM comunica decisione agli RM e fissa nuovo timeout
  
  - i RM comunicano un ack e poi comunicano se vogliono fare commit o abort
  
  - TM raccoglie tutti gli ack, se scatta timeout fissa nuovo time-out e ripete la trasmissione a tutti i RM che non hanno ancora risposto. Continua finchè
    tutti non rispondono.
  
  - TM scrive su log

![](img/2pc.png)

Protocollo ovviamente centralizzato per come lo abbiamo visto (TM "master"), TM collo di bottiglia

Versione lineare: 

- Tm comunica per primo con primo RM

- primo rm comunica con secondo rm e così via

- tm comunica con ultimo rm

Versione distribuita:

- TM comunica con gli RM

- RMs inviano decisioni a tutti gli RMs

- Ogni RM decide in base ai voti che ascolta dagli altri

- Non serve seconda fase 2p

###### 2pc (centralizzato) in caso di guasto

- un RM nello stato di ready perde la sua autonomia e aspetta TM

- un guasto a TM lascia RM in stato di incertezza

Guasti di componenti:

- protocolli di terminazione -> assicura terminazione

- protocolli di recovery -> assicura ripristino

**Protocolli di terminazione con guasto di un rm:**

- RM cade prima del prepare
  
  - TM dopo timeout fa ABORT

- RM cade dopo aver risposto commit/abort
  
  - RM quando si riprende sa cosa ha scritto lui, se si trova in ready si mette in attesa
  
  - RM chiede cosa fare a TM
  
  - TM rimanda decisione abort/commit 

TM capisce se RM è caduto grazie a timeout.

**Protocolli di terminazione con guasto del tm:**

- TM cade nella fase di prepare
  
  - RM dopo un timeout fanno abort

- TM cade dopo:
  
  - gli RM si possono mettere d'accordo tra di loro per capire cosa fare (algoritmi bizantini)

<u>Variamo comportamento in base a ultimo log in TM:</u>

- Se ultimo log è prepare:
  
  - TM può decidere di fare global abort 
  
  - oppure ripetere la prima fase sperando di giungere a global commit.
  
  - se ultimo log è global-commit o global-abort:
    
    - TM ripete seconda fase

- se ultimo log è una complete
  
  - va tutto bene e TM non fa nulla.

<u>Protocolli di ripristino con caduta di un RM in base ai log:</u>

- nel file di log c'è scritto abort o commit:
  
  - tutto come sistemi centralizzati

- nel file di log l'ultimo messagio è ready:
  
  - RM si blocca perchè non sa la decisione di TM
  
  - 2 casi:
    
    - RM chiede a TM cosa fare (richiesta di remote recovery)
    
    - RM aspetta che TM riesegua la seconda fase del protocollo.

Perdita di messaggi e partizionamento della rete

TM non è in grado di distinguere se è morto RM o se si è perso il messaggio, in entrambi i casi decide abort.

Anche nel caso di perdita di ack la seconda fase viene ripetuta a seguito di timeout

##### Ottimizzazioni di 2pc

Ridurre numero messaggi.

Se un RM vede che le sue operazioni sono read-only finisce protocollo e non partecipa alla seconda fase.

"scordarsi abort, ricordarsi i commit": se decido di fare abort abbandona la transazione e bon. Gli unici record nel log sono global commit, ready e commit.

##### Protocollo xopen DTP

Architettura di venditori che si sono messi d'accordo, ci sono sempre RM e TM.

Si interagisce con API standard.

## Repliche

Ogni vendor ha le sue tecnologie.

Replica è il processo di mantenere varie istanze dello stesso di db allineate tra di loro.

Sincronizzazione: processo per tenere allineate le varie copie "eventually"

Replica sincrona vs asincrona:

- sincrona: come ROWA, appena modifico qualcosa sincronizzo su tutte le repliche e poi completo la transazione

- asincrono: faccio con calma dopo aver finito la transazione.

Vari contesti a cui pensare alla replica:

- condivisione dati tra utenti tra loro scollegati, si ha merge conflict

- data consolidation, quando un'azienda vuole tenere più copie dei dati in vari punti

- data distribution, caso degli e-commerce.

- prestazioni, accesso efficiente, load balancing e accesso offline: ad esempio sito vetrina.

- separare tra data entry e reporting

- coesistenza di applicazioni che hanno bisogni di trasformazioni di dati complesse.

Casi in cui non si dovrebbe replicare:

- se ci sono frequenti update su più copie

- quando la consistenza è critical, solitamente si usa ROWA.

Benefici:

- disponibilità

- reliability

- performance

- load reduction

- disconnected computing

- supports many users

Tipologie:

- Data distribution, 1:many ho db centrale che distribuisce le varie copie passive, che vedono soltando i dati

- P2P, posso gestire con ROWA

- Data consolidation, many:1 vari db conosolidati a livello centrale

- Bi direzionale: copia primaria e copia secondaria (P2P con due soli peer)

- Multi-staging

Come realizzare replica:

- Prendo l'hdd e lo copio da un'altra parte, lo copio e lo rimetto al suo posto

- Faccio backup totale

- Faccio backup incrementale, ovvero faccio prima un backup full, poi avrò il log e trasferisco solo log.

- Event publishing (soluzione microsoft)
