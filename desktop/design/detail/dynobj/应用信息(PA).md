# 应用信息(BA)
- **功能：** 用于应用信息查询和展现，里面加入BA的权限条件

## 1、界面
![](./../img/dynobj/应用信息(PA).png)

注：墨绿色为隐藏字段

## 2、SQL：
```
SELECT
  tah.app_id       AS appId,
  tah.app_no       AS appNo,
  tah.app_loc_name AS appName
FROM tzpf_app_header tah
WHERE  tah.app_status = '1'
ORDER BY tah.app_no; 
```

## 3、字段元素
|字段|名称|key|search|hidden|
|---|---|:---:|:---:|:---:|
|appId|应用ID|ID|true|true|
|appNo|应用编号|CODE|true|false|
|appName|应用名称|LABEL|true|false|


