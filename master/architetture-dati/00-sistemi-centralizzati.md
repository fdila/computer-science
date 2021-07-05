# Sistemi centralizzati

**DBMS**: database management system:

- tanti dati

- persistenti

- condivisi

- affidabile

Si hanno:

- uno o più storage, con uno o più file system

- il dbms software che fa da componente logico

- applicazioni che elaborano dati provenienti dal db

- DBA (database admin)

Definizione architettura ANSI/SPARC:

- schemi esterni, porzioni di db messi a disposizione alle applicazioni

- schema logico (concettuale): modello relazionale dei dati

- schema fisico: tecnologia usata per implementare le tabelle.

Inoltre:

- unico linguaggio di interrogazione

- unico sistema di gestione accesso, aggiornamento e gestione di transazioni/interrogazioni

- unica modalità di ripristino in caso di emergenza

- unico dba

- no autonomia gestionale

**Problemi di concorrenza**: se le transazioni sono seriali ok

**Sistema di autorizzazione**

**Query**

Funzionalità cooperanti del dbms:

- Query compiler che prende query in sql e traduce con un compilatore

- Gestore di interrogazioni e aggiornamenti che trasforma query in algebra relazionale, facendo operazioni di ottimizzazione

- Gestore dei metodi di accesso per passaggio tra file e tabelle passando da gestore del buffer e gestore della memoria secondaria.

- DDL compiler, (Data Description Language), che si occupa dei comandi del dba

- Gestore della concorrenza

- Gestore dell'affidabilità, garantisce che un dato non vada perso

- Gestore delle transazioni

## Ottimizzazione query

**Parsing**: stabilisce se query è sensata e se tabelle e attributi sono coerenti con schema db. Per questo c'è **Data catalog** che contiene le info sui vari db e il loro schema.

Parser fa analisi lessicale, sintattica e semantica. Produce **query tree**.

Si calcola anche **query plan logico** per capire cosa fare prima, per ottimizzare tempi. La query viene rappresentata come albero dove nodi interni sono le operazioni algebriche, le foglie sono strutture dati logiche (tabelle).

Abbiamo anche un db chiamato **statistics** che contiene statistiche sulla storia delle query per ottimizzare query.

L'ottimizzazione ha complessità esponenziale, si introducono ottimizzazione anche con Branch&Bound.

## Transazioni

Transazione -> insieme di istruzioni d'accesso in lettura e scrittura ai dati.

Iniziano con begin-transaction e all'interno deve essere eseguito

- o commit work, per terminare l'operazione

- o rollback work, per abortire transazione

Un sistema transazionale OLTP (OnLine Transaction Processing) è in grado di definire e eseguire transazioni per conto di molte applicazioni concorrenti.

Tra commit e rollback ne va eseguito SOLO UNO.

**Proprietà ACID:**

- **Atomicità**: una transazione è un'unità atomica. Non si può lasciare db in stato intermedio.

- **Consistenza:** transazione rispetta i vincoli di integrità (se lo stato iniziale è corretto lo è anche quello finale). Se ci sono violazioni non devono restare alla fine (si fa rollback).

- **Isolamento**: la transazione non risente delle altre transazioni concorrenti. Una transazione non espone i suoi stati intermedi per evitare effetto domino.

- **Durabilità**: effetti di una transazione andata in commit non vanno persi anche in presenza di guasti (in questo caso si usa un recovery manager).

## Gestore concorrenza

Serve per permettere di eseguire più operazioni in parallelo.

Definiamo uno schedule come sequenza di esecuzione di un insieme di transazioni. Uno schedule è seriale se una transazione termina prima che inizi la successiva.

Si sfrutta **proprietà di isolamento** facendo in modo che ogni transazione esegua come se non ci fosse concorrenza: un insieme di transazioni eseguite concorrentemente produce lo stesso risultato che produrrebbe una delle possibili esecuzioni sequenziali delle stesse transazioni allora si ha la proprietà di isolamento.

Si ha quindi che uno schedule è serializzabile se l'esito della sua esecuzione è lo stesso che si avrebbe con una qualsiasi permutazione delle operazioni.

Vari algoritmi per il controllo della concorrenza:

- controllo basato su conflict equivalence

- controllo di concorrenza basato sui *locks* (protocollo 2 phase locking). Si hanno tabelle di lock. In ogni transazione tutte le richieste di lock precedono tutti gli unlock.

- controllo di concorrenza basato su timestamp
