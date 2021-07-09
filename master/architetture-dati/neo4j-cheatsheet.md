# Cheatsheet Neo4j

Trovare nodi in base a attributi

```
MATCH(p:Person) WHERE p.name = "cose" RETURN p
```

Trovare nodi in base a relazioni

```
MATCH(p:Person)-[:ACTED_IN]->(m:Movie) 
WHERE p.name="Tom Hanks" return p,m
```

Trovare relazioni e loro tipo

```
MATCH(p:Person)-[r]->(m:Movie) 
WHERE m.title="Cloud Atlas" return p.name, type(r), r, m.title
```

Trovare cose con n archi che le collegano

```
MATCH (pm)-[*1..4]-(k:Person {name:"Kevin Bacon"}) return pm
```

Trovare cose collegate dal path più corto e ritornarlo

```
MATCH sp = 
shortestPath ((p:Person {name:"Kevin Bacon"})-[*]-(k:Person {name:"Meg Ryan"})) return sp
```

Match multipli

```
MATCH (tom:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]
      -(coactors), 
(p:Person)-[:ACTED_IN]->(m2:Movie)<-[:ACTED_IN]
      -(coactors) Where not (p)-[:ACTED_IN]->(m) RETURN p
```

Raggruppare e fare liste

```
MATCH (s:Supplier)-[:SUPPLIES]->(:Product)-[:PART_OF]->(c:Category) 
RETURN s.companyName as Company, collect(distinct c.categoryName) as Categories
```

Ordinare risultati

```
MATCH (p:Person {gender:"F", lastName: "Colombo"}) 
RETURN p.firstName ORDER BY p.firstName ASC
```

Usare cose di aggregazione nel WHERE

```
MATCH (b:Book)<-[r:Wrote]-(p:Author) 
WITH b, count(r) as cnt WHERE cnt>=3 RETURN b.title, cnt
```

Creare nodo con attributi

```
CREATE(p1:Person {name:"John", age:27})
```

Creare relazione

```
CREATE (john)-[:Knows{since: "01/09/2013"}]->(sally)
```

```
MATCH (sally:Person {name: "Sally"}), (john:Person {name: "John"}) 
CREATE (john)-[:friend_of {date: "01/09/2013"}]->(sally)
```
