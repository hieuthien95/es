================= Day 1 =================
https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-index.html

### Check status es
```
curl "localhost:9200/_cat/indices?v"
```

### Create or Update index
```
PUT /customer/_doc/1
{
  "name": "John Doe"
}
```

### Get 1 index
```
GET /customer/_doc/1
```

### Create index BULK
```
curl -H "Content-Type: application/json" -XPOST "localhost:9200/bank/_bulk?pretty&refresh" --data-binary "@accounts.json"
```

================= Day 2 =================
https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-search.html#getting-started-search

### match_all
```
GET /customer/_search
{
  "query": { "match_all": {} },
  "sort": [
    { "age": "asc" }
  ],
  "from": 0,
  "size": 10
}
```

### match
```
GET /customer/_search
{
  "query": { 
    "match": {
      "name": "john doe"
    } 
  }
}
```

### match_phrase
```
GET /customer/_search
{
  "query": { 
    "match_phrase": {
      "name": "john doe"
    } 
  }
}
```

### bool: match / should / must_not 
```
GET /customer/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "123" } }
      ],
      "must_not": [
        { "match": { "name" : "J2ohn D2oe" } }
      ]
    }
  }
}
```

### range
```
GET /customer/_search
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "age": {
            "gte": 30,
            "lte": 130
          }
        }
      }
    }
  }
}
```

================= Day 2 =================
https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-aggregations.html

