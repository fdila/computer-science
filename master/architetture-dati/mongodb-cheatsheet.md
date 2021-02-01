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

**Contare**

```python
collection.find().count()
```


