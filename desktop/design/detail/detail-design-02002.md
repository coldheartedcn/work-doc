# 企业应用管理
- **功能：** 让企业管理员用于管理企业应用相关信息，现阶段只是用于企业应用管理员的设置
- **使用角色：** 企业管理员
- **Axure指向：** 2.2 企业应用查询

## 1、流程图
![](./img/2/2/企业应用管理流程图.png)

图0-1

## 2、模块详细设计

### 2.1、企业应用查询模块
使用查询配置出相应界面

#### 2.1.1、界面
![](./img/2/2/企业应用查询界面.png)

图1-1

#### 2.1.2、业务规则

##### 条件元素
|ID|名称|是否必填|查询类型|字段|备注|
|---|---|:-----:|:-----:|---|---|
|bgId|企业名称|否|精准查询|tb.bg_id|动态对象——[企业信息(BA)](dynobj/企业信息(BA).md)——CODELABEL2ID|
|appId|应用名称|否|精确查询|tah.app_id|动态对象——[应用信息(BA)](dynobj/应用信息(BA).md)——CODELABEL2ID|

##### SQL:
```
SELECT
  teh.erp_id        AS erpId,--企业应用ID  隐藏
  tb.bg_no          AS bgNo,--企业编号
  tb.bg_name        AS bgName,--企业名称
  tah.app_no        AS appNo,--应用编号
  tah.app_loc_name  AS appName,--应用名称
  tal.level_no      AS levelNo,--应用级别编号
  tal.level_name    AS levelName,--应用级别名称
  vu.nickname--企业应用管理员
FROM tzpf_bg tb
  INNER JOIN tzpf_erp_header teh ON (teh.user_type = '1' AND teh.user_id = tb.bg_id)
  INNER JOIN tzpf_app_header tah ON (tah.app_status = '1' AND tah.app_id = teh.app_id)
  INNER JOIN tzpf_app_level tal ON (tal.level_id = teh.level_id)
  LEFT JOIN v3_user vu ON (vu.person_id = teh.admin_person_id)
WHERE tb.admin_person_id = ${session_personId} AND ${bgId} AND ${appId}
ORDER BY tb.bg_no, tah.app_no, tal.level_no;
```

##### 字段元素
|字段|名称|hidden|
|:---:|:---:|:---:|
|erpId|企业应用ID|true|
|bgNo|企业编号|false|
|bgName|企业名称|false|
|appNo|应用编号|false|
|appName|应用名称|false|
|levelNo|应用级别编号|false|
|levelName|应用级别名称|false|
|nickname|企业应用管理员|false|

##### 右击菜单逻辑
|菜单|操作逻辑|
|:---:|-----|
|设置企业应用管理员|打开[设置企业应用管理员界面](#22设置企业应用管理员界面)，传输条件erpId|

### 2.2、设置企业应用管理员界面
主键为erpId，所有的操作以erpId进行贯穿

#### 2.2.1、界面
![](./img/2/2/企业应用管理员界面.png)

图2-1


#### 2.2.2、业务规则

##### 图2-1界面元素
|名称|字段|备注|
|:---:|:---:|---|
|企业名称|bgName| |
|应用名称|appName| |
|应用级别|levelName| |
|管理员|adminPersonId|动态对象——[人员账号_bgId](dynobj/人员账号_bgId.md)——CODELABEL2ID|

##### 界面逻辑
|规则|描述|
|:---:|---|
|打开|依据erpId从数据库中获取到bgName／appName／levelName／adminPersonId，并填入对应的field内，同时返回bgId用于管理员的动态对象传入参数|
|选择管理员|动态对象的选择，展现：[employeeNumber]nickname，提交：personId|
|设置|提交erpId和adminPersonId，依据erpId修改对应adminPersonId，并需要把其保存到日志表tzpf_erp_admin_change_log|
|设置错误|提示错误信息|
|设置正确|提示设置成功，点击确定后关闭窗口，并刷新外面的查询|
|关闭逻辑|关闭窗口|