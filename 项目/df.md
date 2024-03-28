```sql
# 更新旧版迁移过来的解析视频地址到新的字段，原字段作为了题干视频地址
update tiku_question set resolve_movie_address = movie_address where category_id in (select id from tiku_category where parent_id = 137286);
update tiku_question set movie_address = NULL where category_id in (select id from tiku_category where parent_id = 137286);

# 删除答案解析中的：号
update tiku_question set answer_resolve =replace(answer_resolve,'<b>[答案解析]</b><br/>：','<b>[答案解析]</b><br/>') where answer_resolve like '<b>[答案解析]</b><br/>：%';
```

