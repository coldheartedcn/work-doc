# 企业信息(BA)
- **功能：** 用于企业信息查询和展现，里面加入BA的权限条件

## 1、界面
![](./../img/dynobj/企业信息(BA).png)

注：墨绿色为隐藏字段

## 2、SQL：
```
SELECT
  tb.bg_id   AS bgId,
  tb.bg_no   AS bgNo,
  tb.bg_name AS bgName 
FROM tzpf_bg tb
WHERE tb.admin_person_id = ${session_personId}
ORDER BY tb.bg_no;
```

## 3、字段元素
|字段|名称|key|search|hidden|
|---|---|:---:|:---:|:---:|
|bgId|企业ID|ID|true|true|
|bgNo|企业编号|CODE|true|false|
|bgName|企业名称|LABEL|true|false|


