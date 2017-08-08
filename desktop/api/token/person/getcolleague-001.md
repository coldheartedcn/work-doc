# 指定企业人员列表（请求人在该企业下）

## 场景描述
使用token请求数据，带有参数bgId，并进行分页获取。

## 业务逻辑
依据请求人的token信息，解析出其personId，查询该personId是否在对应的企业下，不在则抛出异常。  
依据bgId、pageSize、pageIndex三个参数，关联表v3_user和tzpf_bg_person，获取人员信息。  

## 请求路径
**/desktop/token/api/person/getcolleagues**

## 请求方式
**GET**

## 请求参数
|参数|名称|类型|必填|备注|
|---|---|:---:|:---:|---|
|bgId|企业ID|String|true|用于查询该企业ID下的人员|
|pageSize|每页大小|int|true|用于标注每页数据条数|
|pageIndex|页码|int|true|用于标注查询的页码数|


## 返回信息
```
{
    "result": "SUCCESS",
    "returnTag": null,
    "returnObject": [
        {
            "emailAddress": "******",   --邮箱
            "mobilePhone": "******",    --手机
            "nickname": "******",       --人员昵称
            "personId": "******",       --人员ID
            "employeeNumber": "******"  --账号
        },
        ......
    ],
    "serverId": "196.8.9.86",
    "objectClassName": "AbstractModel$$BeanGeneratorByCGLIB$$6b55399e"
}
```

## 业务异常
```
{
    "result": "FAIL",
    "serverId": "196.8.9.86",
    "returnObject": "你不属于该企业，无法查询该企业人员信息！",
    "returnTag": null,
    "objectClassName": null
}
```