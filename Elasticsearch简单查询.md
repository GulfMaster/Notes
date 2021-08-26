[TOC]

# 索引

~~~
#查看索引设置
GET /bank/_settings

#查看索引
GET /test-index-users/_mapping

#关闭索引
POST /test-index-users/_close

#打开索引
POST /test-index-users/_open

#删除索引
DELETE /test-index-users

#查询索引中的数据
GET /test-index-users/_search

#插入数据（如果没有索引，会自动创建索引）
POST /test-index-users/_doc
{
  "name":"liwenbo",
  "age":888,
  "remarks":"福如东海"
}

#创建索引
PUT /test-index-users
{
  "settings": {
		"number_of_shards": 1,
		"number_of_replicas": 1
	},
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          }
        }
      },
      "age": {
        "type": "long"
      },
      "remarks": {
        "type": "text"
      }
    }
  }
}
~~~





# 聚合查询

~~~
#聚合查询排序
GET /bank/_search
{
  "size":0,
  "aggs":{
    "group_by_age":{
      "terms": {
        "field": "age",
        "size": 10,
        "order":{
          "avg_balance":"desc"
        }
      },
      "aggs":{
        "avg_balance":{
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
~~~



# 查询

## 简单查询

~~~
#filter操作
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "state": "ND"
          }
        }
      ],
      "filter": [
        {
          "term": {
            "age": "40"
          }
        },
        {
          "range": {
            "balance": {
              "gte": 20000,
              "lte": 30000
            }
          }
        }
      ]
    }
  }
}

#多条件查询
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
  }
}

#查询
GET /bank/_search
{
  "query": { "match": { "address": "mill lane" } }
}

#简单查询
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}
~~~



准备数据

~~~
PUT /test-dsl-term-level
{
  "mappings": {
    "properties": {
      "name": {
        "type": "keyword"
      },
      "programming_languages": {
        "type": "keyword"
      },
      "required_matches": {
        "type": "long"
      }
    }
  }
}

POST /test-dsl-term-level/_bulk
{ "index": { "_id": 1 }}
{"name": "Jane Smith", "programming_languages": [ "c++", "java" ], "required_matches": 2}
{ "index": { "_id": 2 }}
{"name": "Jason Response", "programming_languages": [ "java", "php" ], "required_matches": 2}
{ "index": { "_id": 3 }}
{"name": "Dave Pdai", "programming_languages": [ "java", "c++", "php" ], "required_matches": 3, "remarks": "hello world"}
~~~



### id查询:ids

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "ids": {
      "values": [3, 1]
    }
  }
}
~~~

### 前缀:prefix

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "prefix": {
      "name": {
        "value": "Jan"
      }
    }
  }
}
~~~

### 分词匹配:term

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "term": {
      "programming_languages": "php"
    }
  }
}
~~~

### 多个分词匹配:terms

按照读个分词term匹配，它们是or的关系

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "terms": {
      "programming_languages": ["php","c++"]
    }
  }
}
~~~

### 按某个数字字段分词匹配:term set

设计这种方式查询的初衷是用文档中的数字字段动态匹配查询满足term的个数

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "terms_set": {
      "programming_languages": {
        "terms": [ "java", "php" ],
        "minimum_should_match_field": "required_matches"
      }
    }
  }
}
~~~

### 通配符:wildcard

通配符匹配，比如`*`

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "wildcard": {
      "name": {
        "value": "D*ai",
        "boost": 1.0,
        "rewrite": "constant_score"
      }
    }
  }
}
~~~

### 范围:range

常常被用在数字或者日期范围的查询

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "range": {
      "required_matches": {
        "gte": 3,
        "lte": 4
      }
    }
  }
}
~~~

### 正则:regexp

通过[正则表达式](https://www.pdai.tech/md/develop/regex/dev-regex-all.html)查询

以"Jan"开头的name字段

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "regexp": {
      "name": {
        "value": "Ja.*",
        "case_insensitive": true
      }
    }
  }
}
~~~

### 模糊匹配:fuzzy

官方文档对模糊匹配：编辑距离是将一个术语转换为另一个术语所需的一个字符更改的次数。这些更改可以包括：

- 更改字符（box→ fox）

- 删除字符（black→ lack）

- 插入字符（sic→ sick）

- 转置两个相邻字符（act→ cat）

~~~
GET /test-dsl-term-level/_search
{
  "query": {
    "fuzzy": {
      "remarks": {
        "value": "hell"
      }
    }
  }
}
~~~

  

## 复合查询

### bool query(布尔查询)

~~~
POST _search
{
  "query": {
    "bool" : {
      "must" : {
        "term" : { "user.id" : "kimchy" }
      },
      "filter": {
        "term" : { "tags" : "production" }
      },
      "must_not" : {
        "range" : {
          "age" : { "gte" : 10, "lte" : 20 }
        }
      },
      "should" : [
        { "term" : { "tags" : "env1" } },
        { "term" : { "tags" : "deployed" } }
      ],
      "minimum_should_match" : 1,
      "boost" : 1.0
    }
  }
}

~~~

### boosting query(提高查询)

不同于bool查询，bool查询中只要一个子查询条件不匹配那么搜索的数据就不会出现。而boosting query则是降低显示的权重/优先级（即score)。

**准备数据**

~~~
POST /test-dsl-boosting/_bulk
{ "index": { "_id": 1 }}
{ "content":"Apple Mac" }
{ "index": { "_id": 2 }}
{ "content":"Apple Fruit" }
{ "index": { "_id": 3 }}
{ "content":"Apple employee like Apple Pie and Apple Juice" }

~~~



~~~
GET /test-dsl-boosting/_search
{
  "query": {
    "boosting": {
      "positive": {
        "term": {
          "content": "apple"
        }
      },
      "negative": {
        "term": {
          "content": "pie"
        }
      },
      "negative_boost": 0.5
    }
  }
}
~~~

### constant_score（固定分数查询）

查询某个条件时，固定的返回指定的score；显然当不需要计算score时，只需要filter条件即可，因为filter context忽略score

**准备数据**

~~~
POST /test-dsl-constant/_bulk
{ "index": { "_id": 1 }}
{ "content":"Apple Mac" }
{ "index": { "_id": 2 }}
{ "content":"Apple Fruit" }
~~~

~~~
GET /test-dsl-constant/_search
{
  "query": {
    "constant_score": {
      "filter": {
        "term": { "content": "apple" }
      },
      "boost": 1.2
    }
  }
}
~~~

### dis_max(最佳匹配查询）

分离最大化查询（Disjunction Max Query）指的是： 将任何与任一查询匹配的文档作为结果返回，但只将最佳匹配的评分作为查询的评分结果返回 。

**准备数据**

~~~
POST /test-dsl-dis-max/_bulk
{ "index": { "_id": 1 }}
{"title": "Quick brown rabbits","body":  "Brown rabbits are commonly seen."}
{ "index": { "_id": 2 }}
{"title": "Keeping pets healthy","body":  "My quick brown fox eats rabbits on a regular basis."}
~~~

~~~
GET /test-dsl-dis-max/_search
{
    "query": {
        "bool": {
            "should": [
                { "match": { "title": "Brown fox" }},
                { "match": { "body":  "Brown fox" }}
            ]
        }
    }
}
~~~

