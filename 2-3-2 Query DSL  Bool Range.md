### Bool 복합 Query

```
GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "message": "quick"
          }
        },
        {
          "match_phrase": {
            "message": "lazy dog"
          }
        }
      ]
    }
  }
}


GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "message": "quick"
          }
        }
      ],
      "must_not": [
        {
          "match_phrase": {
            "message": "lazy dog"
          }
        }
      ]
    }
  }
}

#should 쿼리
#fox중에서 lazy에 대해서 가중치를 부여한다.

GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "message": "fox"
          }
        }
      ],
      "should": [
        {
          "match": {
            "message": "lazy"
          }
        }
      ]
    }
  }
}

#exact value 쿼리
#fox도 있어야 되고, quick도 있어야 됨

GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "message": "fox"
          }
        },
        {
          "match": {
            "message": "quick"
          }
        }
      ]
    }
  }
}

#must 대신 filter로 하면?
#결과는 똑같지만 점수에서 차이가 난다.
```



### filter

```
# filter는 점수에는 반영이 되지 않는다.

#보기 싫은 검색 결과만 빼고 싶을때 

GET my_index/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "message": "fox"
          }
        }
      ],
      "filter": [
        {
          "match": {
            "message": "quick"
          }
        }
      ]
    }
  }
}
```



### 범위 쿼리

```
POST phones/_bulk
{"index":{"_id":1}}
{"model":"Samsung GalaxyS 5","price":475,"date":"2014-02-24"}
{"index":{"_id":2}}
{"model":"Samsung GalaxyS 6","price":795,"date":"2015-03-15"}
{"index":{"_id":3}}
{"model":"Samsung GalaxyS 7","price":859,"date":"2016-02-21"}
{"index":{"_id":4}}
{"model":"Samsung GalaxyS 8","price":959,"date":"2017-03-29"}
{"index":{"_id":5}}
{"model":"Samsung GalaxyS 9","price":1059,"date":"2018-02-25"}

### price 범위 검색

GET phones/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 700,
        "lt": 900
      }
    }
  }
}

### 날짜 범위 검색

GET phones/_search
{
  "query": {
    "range": {
      "date": {
        "gt": "2014-01-01",
        "lt": "2017-01-01"
      }
    }
  }
}
```