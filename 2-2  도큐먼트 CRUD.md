```
POST my_index/_update/1
{
  "doc":{
  "age": 40
  }
}

PUT my_index/_doc/1
{
  "age": 40
}

PUT my_index/_doc/1
{
  "name":"Jongmin Kim",
  "message":"안녕하세요 Elasticsearch"
}

get my_index/_doc/1

get my_index/_source/1

DELETE my_index/_doc/1
```



### bulk API
대용량 데이터를 색인할때 사용

```
POST _bulk
{"index":{"_index":"test", "_id":"1"}}
{"field":"value one"}
{"index":{"_index":"test", "_id":"2"}}
{"field":"value two"}
{"delete":{"_index":"test", "_id":"2"}}
{"create":{"_index":"test", "_id":"3"}}
{"field":"value three"}
{"update":{"_index":"test", "_id":"1"}}
{"doc":{"field":"value two"}}

GET test/_doc/3
```






### Search

```
GET test/_search?q=value AND three

GET test/_search?q=field:value

GET my_index/_search
{
  "query": {
    "match": {
      "message": "안녕하세요"
    }
  }
}
```









