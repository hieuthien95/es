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

### avg
```
POST /kibana_sample_data_ecommerce/_search?size=0
{
    "aggs" : {
        "avg_price" : { "avg" : { "field" : "products.base_price" } }
    }
}
```
```
POST /customer/_search?size=0
{
    "aggs" : {
        "avg_age" : {
            "avg" : {
                "script" : {
                    "source" : "doc.age.value"
                }
            }
        }
    }
}
```

================= Day 3 =================

### cardinality
```
POST /customer/_search?size=0
{
    "aggs" : {
        "type_count" : {
            "cardinality" : {
                "field" : "age"
            }
        }
    }
}
```

### extended_stats / stats
```
GET /kibana_sample_data_ecommerce/_search
{
    "size": 0,
    "aggs" : {
        "age_stats" : { "extended_stats" : { "field" : "products.base_price" } }
    }
}
```

### min/max
```
POST /kibana_sample_data_ecommerce/_search?size=0&pretty
{
    "aggs" : {
        "max_price" : { "max" : { "field" : "products.base_price" } }
    }
}
```

### percentiles / percentile_ranks
```
GET /kibana_sample_data_ecommerce/_search
{
    "size": 0,
    "aggs" : {
        "demo_1_2_3" : {
            "percentiles" : {
                "field" : "products.base_price"
                // "percents" : [95, 99, 99.9]
            }
        }
    }
}
```

### value_count
```
POST /kibana_sample_data_ecommerce/_search?size=0
{
    "aggs" : {
        "price_count" : { "value_count" : { "field" : "products.base_price" } }
    }
}
```

================= Day 3 =================

```
GET /kibana_sample_data_ecommerce/_search?pretty
{
  "query": { 
    "bool": { 
      "must": [
        { "match": { "currency" : "EUR"        }},
        { "match": {  "customer_first_name" : "Eddie" }}
      ],
      "filter": [ 
        { "terms":  { "day_of_week" : ["Monday", "Tuesday"] }},
        { "range": { "day_of_week_i": { "gte": "1" }}}
      ]
    }
  }
}
```





