# deleteVqdTemplate


## 描述
删除视频质检模板

## 请求方式
DELETE

## 请求地址
https://vqd.jdcloud-api.com/v1/vqdTemplates/{templateId}


## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**templateId**|String|True| |模板ID，路径参数|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**requestId**|String|请求ID|


## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Invalid parameter|
|**401**|Authentication failed|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|

## 请求示例
DELETE
```
https://vqd.jdcloud-api.com/v1/vqdTemplates/10000

```
