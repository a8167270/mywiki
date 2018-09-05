---
title: "mysql"
date: 2018-08-13 15:16
---

# Mysql操作

## 查找每组的top N

### 连表查询

```mysql
select type, variety, price
from fruits
where (
   select count(*) from fruits as f
   where f.type = fruits.type and f.price <= fruits.price
) <= 2;
```

### UNION ALL
```mysql
(select * from fruits where type = 'apple' order by price limit 2)
union all
(select * from fruits where type = 'orange' order by price limit 2)
union all
(select * from fruits where type = 'pear' order by price limit 2)
union all
(select * from fruits where type = 'cherry' order by price limit 2)
```

## 根据某字段自定义排序

```mysql
order by field(value,str1,str2,str3,str4,,,,,,strn)

# 例子
SELECT * from wc_university_special_major order by FIELD(remark,"A+", "A", "A-", "B+", "B", "B-", "C+", "C", "C-")
```

