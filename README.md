============================================ Day 1 ============================================

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

============================================ Day 2 ============================================


