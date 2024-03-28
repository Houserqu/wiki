## 常用请求

```apl
# 集群
GET /_cluster/health
GET /_cluster/allocation/explain
{
  "index": "laravel_test.tp_mentor_evaluation", 
  "shard": 0, 
  "primary": true 
}
PUT /_settings
{
  "number_of_replicas": 0
}
GET /_cat/indices?v

# 创建索引
PUT /laravel_test.tp_mentor_evaluation
{
  "settings": {
    "number_of_replicas": 0
  }, 
  "mappings": {
    "properties": {
      "id": {
        "type": "integer"
      },
      "content": {
        "type": "text",
        "analyzer": "ik_max_word"
      },
      "research_funding": {
        "type": "integer",
        "index": false
      },
      "teacher_student_relationship": {
        "type": "integer",
        "index": false
      },
      "student_future": {
        "type": "integer",
        "index": false
      },
      "mentor_id": {
        "type": "integer"
      },
      "view_count": {
        "type": "integer"
      },
      "creator": {
        "type": "integer"
      }
    }
  }
}
# 查索引的结构
GET /laravel_test.tp_mentor_evaluation/_mapping
# 修改索引结构
PUT /laravel_test.tp_mentor_evaluation/_mapping
{
  "properties": {
    "content": {
      "type": "text",
      "analyzer": "ik_max_word"
    }
  }
}
# 删除索引
DELETE /laravel_test.tp_mentor_evaluation

# 查文档总数
GET /laravel_test.tp_mentor_evaluation/_count
# 查单个文档
GET /laravel_test.tp_mentor_evaluation/_doc/2623
# 查文档字段分词
POST /laravel_test.tp_mentor_evaluation/_analyze
{
  "field": "content",
  "text": "  push型老师，对学生冷嘲热讽是常事。学术能力很差，想学数据挖掘方向的不用来了。强行挂作者，抱的一手好大腿。"
}

GET /laravel_test.tp_mentor_evaluation/_search
{
  "query": {
    "match": {
      "content": "，老师人脉广，毕业给推荐"
    }
  }
}

```

