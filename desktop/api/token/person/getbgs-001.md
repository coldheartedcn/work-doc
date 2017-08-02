# 登陆人员所属企业列表

## 场景描述
使用token返回该token对应人员的所属所有企业的列表

## 业务逻辑
依据请求人的token信息，解析出其personId，再根据personId从数据库中查询。
关联tzpf_bg_person和tzpf_bg表，查询出该personId所属所有企业的列表，返回给请求方。

## 请求路径
**/desktop/token/api/person/getbgs**

## 请求方式
**GET**

## 请求参数
**无**

## 返回信息
```
{
    "result": "SUCCESS",
    "serverId": "196.8.9.86",
    "returnObject": [
        {
            "bgName": "******",   ——企业名称
            "bgId": "******",     ——企业ID
            "bgNo": "******",     ——企业编号
            "dbVersion": **,      ——版本控制（忽略）
            "knownAs": "******"   ——企业别名（可能为空）
        },
        ......
    ],
    "returnTag": null,
    "objectClassName": "TzpfBg"
}
```

## 业务异常
**无**