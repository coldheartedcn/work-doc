# 应用信息(BA)
- **功能：** 用于应用信息查询和展现，里面加入BA的权限条件

## 1、界面
![](./../img/dynobj/应用信息(BA).png)

注：墨绿色为隐藏字段

## 2、SQL：
```
SELECT
  tah.app_id       AS appId,
  tah.app_no       AS appNo,
  tah.app_loc_name AS appName 
WHERE tah.app_id = teh.app_id
      AND teh.user_id = tb.bg_id
      AND teh.user_type = '1'
      AND tah.app_status = '1'
      AND tb.admin_person_id = ${session_personId}
GROUP BY tah.app_id, tah.app_no, tah.app_loc_name
ORDER BY tah.app_no; 
```

## 3、字段元素
|字段|名称|key|search|hidden|
|---|---|:---:|:---:|:---:|
|appId|应用ID|ID|true|true|
|appNo|应用编号|CODE|true|false|
|appName|应用名称|LABEL|true|false|


