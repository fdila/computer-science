# Big Data

Piattaforme per gestire un grosso volume di dati.

- volume, tanti dati

- variety, data in many forms

- velocity, data in motion

- veracity, data in doubt

- visibility, data in the open

- value, data of many value

In un architettura di big data ho sistema di storage e sistema di analisi dei dati.

## HDFS

Hadoop Distributed File System

Filesystem distributo

Altamente scalabile con data replication su 3 nodi

Write once, read many.

Muoviamo l'elaborazione verso i dati.

HW che costa poco

Pochi file grandi da eleborare.

File divisi in chunk:

- ogni chunk replicato su 3 servers

Architettura master-slave:

- namenode: master con info varie

- datanode: slave coi dati

C'è anche secondary namenode per backup.

## Map reduce

Elaborazione dei dati. Map reduce è un modello di programmazione/engine che permette di scrivere programmi in stile funzionale ed eseguirli in parallelo su cluster di macchine poco costose.

Fase di Map:

- iterare su grande numero di record

- estrarre qualcosa di interessante da ognuno

- mettere insieme e ordinare i risultati intermedi

Fase di Reduce:

- aggregare risultati intermedi

- generare file di output

Controlla anche nodi con job tracker

## Hadoop

Unendo HDFS e map reduce otteniamo Hadoop.

Hive:

- strato sw che permette di scrivere query sql e traduce in map-reduce

- stile data warehouse

### YARN

Fa da quello che era il job tracker con map reduce.

Ci sono resource manager e application manager.




