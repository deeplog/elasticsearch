### Query DSL: 풀텍스트

```
# 2-3-1 Query DSL : 풀텍스트

DELETE my_index

POST my_index/_bulk
{"index":{"_id":1}}
{"message":"The quick brown fox"}
{"index":{"_id":2}}
{"message":"The quick brown fox jumps over the lazy dog"}
{"index":{"_id":3}}
{"message":"The quick brown fox jumps over the quick dog"}
{"index":{"_id":4}}
{"message":"Brown fox brown dog"}
{"index":{"_id":5}}
{"message":"Lazy jumping dog"}

```



### 매치쿼리

```
# 매치 쿼리
GET my_index/_search
{
  "query": {
    "match": {
      "message": "quick dog"
    }
  }
}

# and 옵션
GET my_index/_search
{
  "query": {
    "match": {
      "message":{
        "query": "quick dog",
        "operator": "and"
      }
    }
  }
}
```

### match phrase

```
#match phrase
# and 옵션
GET my_index/_search
{
  "query": {
    "match_phrase": {
      "message": "lazy dog"
    }
  }
}


#match phrase + slope
GET my_index/_search
{
  "query": {
    "match_phrase": {
      "message": {
        "query": "lazy dog",
        "slop": 1
      }
    }
  }
}
```



```
#query string
#lucene 쿼리를 넣을 수 있음
GET my_index/_search
{
  "query": {
    "query_string": {
      "default_field": "message",
      "query": "(jumping AND lazy) OR \"quick dog\""
    }
  }
}
```

