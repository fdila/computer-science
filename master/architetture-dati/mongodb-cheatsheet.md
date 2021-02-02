# Cheatsheet MongoDB

**Create operations**

```python
db.collection.insertOne()
db.collection.insertMany()
db.collection.insert()
```

**Read operations**

```python
#trova tutti
collection.find({})

#trova e limita al primo risultato
collection.find({}).limit(1)

#trova filtrando su attributo = valore
collection.find({'attributo': valore})

#trova e seleziona tutti gli attributi tranne id
collection.find({},{'_id': 0})

#trova e seleziona solo gli attributi a e b
collection.find({}, {'a':1, 'b':1})

#trova e ordina per attributo ascendente
collection.find().sort('a', 1)
```

**Operatori di comparazione**

```python
# equal un valore
$eq 
# not equal un valore
$neq
# greater than valore
$gt
# greater equal than valore
$gte
# less than valore
$lt
# less equal than valore
$lte
# non ha valore nell'array (not in)
$nin


collection.find({a: {'$gt': 0, 'lt': 10}})
```

**Operatori logici**

```python
$and
$not
$nor
$or

collection.find({'and': [{'a': "pippo"},{'b': "pluto"}]})
```

**Operatori per elementi**

```python
#trova se attributo 'cose' non c'è
collection.find({'cose': {'$exists': 'false'}})


#trova se attributo cose è int
collection.find({'cose': {'$type': 'int'}})
```

**Evaluation operators**

```python
# aggregation expression
$expr
# regex
$regex
# text
$text
```

**Operatori geospaziali**

```python
$geoIntersect
$geo
$near
$nearSphere
```

**Operatori su array**

```python
# contiene tutti gli elementi specificat
$all
# contiene gli elementi?
$elem
# se size array è uguale
$size
```

**Contare**

```python
collection.find().count()
```

**Aggregazione**

```python
collection.aggregate{[
    {$group:
        {
          _id: <expression>, // Group By Expression (ex. $nome_attributi    )
          <field1>: { <accumulator1> : <expression1> },
        }    
    }
    { $match: {
        "attributo": 10
      }
    }
    { $project: {"_id": 0, "attr:" 1}}
    { $count: "n_cose"}
    { $limit: 100}
    { $sort: {"att10",1}}
      
  ]
}

```

```python
$avg
$first
$last
$max
$mix
$sum
```

**Relazioni con reference**

```python
collection1.aggregate([
    {  '$lookup' : {
            from: "collection2",
            localField: "id_coso",
            foreignField: "id",
            as: "nome_coso"         
        }
    }
])
```

**Indici**

```python
collection.create_index([("attributo", pymongo.DESCENDING)])
```

**Operazioni di update**

```python
collection.updateOne()
collection.updateMany()
collection.replaceOne()
collection.update()
```

**Operazioni di delete**

```python
collection.deleteOne()
collection.deleteMany()
collection.remove()
```


