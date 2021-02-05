# Neo4j

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




