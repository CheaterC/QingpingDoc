
## 3. 设备相关接口

### 3.1 绑定设备
- **接口说明：** 绑定设备
- **接口方法：** POST
- **接口地址：** /v1/apis/devices

#### 3.1.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格
&emsp;Content-Type				|application/json	|固定值

#### 3.1.2 请求参数
  
参数名称					    |类型		|出现要求	    |描述  
:----						|:---		|:------	|:---
&emsp;device_token		    |string		|R			|配对码
&emsp;product_id		    |int		|R			|产品id


请求示例：
```
https://apis.cleargrass.com/v1/portal/apis/devices
// json body
{
    "device_token": "143412",
    "product_id": "1001"
}
```

#### 3.1.3 返回结果
参数名称				        |类型		|出现要求	|描述  
:----						|:---		|:------	|:---
info				        |object	    |R			|设备信息
&emsp;name				    |string		|R			|设备名称
&emsp;mac				    |string		|R			|设备mac地址
&emsp;sn				    |string		|R			|设备序列号
&emsp;version				|string		|R			|设备版本
&emsp;created_at			|string		|R			|设备注册时间
&emsp;status			    |[]string	|R			|设备状态 offline(离线) online(在线) alarm(警报) 
&emsp;product			    |object		|R			|产品信息
&emsp;&emsp;id			    |string		|C			|产品id
&emsp;&emsp;desc			|string		|C			|产品描述
data				        |object	    |C			|设备数据
&emsp;battery				|object		|C			|电量
&emsp;humidity		        |object		|C			|湿度
&emsp;pressure		        |object		|C			|气压
&emsp;temperature			|object		|C			|温度
&emsp;timestamp			    |object		|C			|时间
&emsp;&emsp;value		    |float		|C			|数值

```
{
    "info":{
        "name": "温湿度气压计",
        "mac": "582D34460442",
        "imei": "82869B172C688BED",
        "version": "1.0.1_0049",
        "created_at": 1573034091,
        "status":["offline"],
        "product": {"id":"10", "desc":"青萍温湿度气压计"}
    },
    "data":{
        "battery": {"value": 70},
        "humidity": {"value": 22.2},
        "pressure": {"value": 103.29},
        "temperature": {"value": 20.8},
        "timestamp": {"value": 1574565267}
    }
}
```

### 3.2 删除设备
- **接口说明：** 删除设备
- **接口方法：** DELETE
- **接口地址：** /v1/apis/devices

#### 3.2.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格
&emsp;Content-Type				|application/json	|固定值

#### 3.2.2 请求参数
  
参数名称					    |类型		|出现要求	    |描述  
:----						|:---		|:------	|:---
&emsp;mac		            |[]string   |R			|mac地址


请求示例：
```
https://apis.cleargrass.com/v1/portal/apis/devices
// json body
{
    "mac": ["582D34460442"]
}
```

### 3.3 设备列表
- **接口说明：** 设备列表
- **接口方法：** GET
- **接口地址：** /v1/apis/devices

#### 3.3.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格

#### 3.3.2 请求参数
  
参数名称						    |类型		|出现要求	    |描述  
:----						    |:---		|:------	|:---
&emsp;timestamp				    |int		|R			|时间戳
&emsp;offset				    |int		|O			|偏移量
&emsp;limit				        |int		|O			|最大返回数据条数 不得超过50	

请求示例：

```
https://apis.cleargrass.com/v1/apis/devices?timestamp=1573612191
```

#### 3.3.3 返回结果

参数名称						    |类型		|出现要求	|描述  
:----						    |:---		|:------	|:---
total				            |int		|R			|设备总数
devices				            |[]object	|R			|设备数据
&emsp;info				        |object	    |R			|设备信息
&emsp;&emsp;name				|string		|R			|设备名称
&emsp;&emsp;mac				    |string		|R			|设备mac地址
&emsp;&emsp;sn				    |string		|R			|设备序列号
&emsp;&emsp;version				|string		|R			|设备版本
&emsp;&emsp;created_at			|string		|R			|设备注册时间
&emsp;&emsp;status			    |[]string	|R			|设备状态 offline(离线) online(在线) alarm(警报) 
&emsp;&emsp;product			    |object		|R			|产品信息
&emsp;&emsp;&emsp;id			|string		|C			|产品id
&emsp;&emsp;&emsp;desc			|string		|C			|产品描述
&emsp;data				        |object	    |C			|设备数据
&emsp;&emsp;battery				|object		|C			|电量
&emsp;&emsp;humidity		    |object		|C			|湿度
&emsp;&emsp;pressure		    |object		|C			|气压
&emsp;&emsp;temperature			|object		|C			|温度
&emsp;&emsp;tvoc			    |object		|C			|挥发物质
&emsp;&emsp;co2			        |object		|C			|二氧化碳
&emsp;&emsp;pm25			    |object		|C			|pm25
&emsp;&emsp;timestamp			|object		|C			|时间
&emsp;&emsp;&emsp;value		    |float		|C			|数值

示例：

```
{
    "total": 2,
    "devices":[
        {
            "info":{
                "name": "温湿度气压计",
                "mac": "582D34460442",
                "imei": "82869B172C688BED",
                "version": "1.0.1_0049",
                "created_at": 1573034091,
                "status":["offline"],
                "product": {"id":1001, "desc":"青萍温湿度气压计"}
            }
            "data":{
                "battery": {"value": 70},
                "humidity": {"value": 22.2},
                "pressure": {"value": 103.29},
                "temperature": {"value": 20.8},
                "timestamp": {"value": 1574565267}
            }
        },
        {
            "info":{
                "name": "温湿度气压计",
                "mac": "582D34460442",
                "imei": "82869B172C688BED",
                "version": "1.0.1_0049",
                "created_at": 1573034091,
                "status":["offline"],
                "product": {"id":1001, "desc":"青萍温湿度气压计"}
            }
            "data":{
                "battery": {"value": 70},
                "humidity": {"value": 22.2},
                "pressure": {"value": 103.29},
                "temperature": {"value": 20.8},
                "timestamp": {"value": 1574565267}
            }
        }
    ]
}
```



### 3.4 设备历史数据
- **接口说明：** 设备历史数据
- **接口方法：** GET
- **接口地址：** /v1/apis/devices/data

#### 3.4.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格

#### 3.4.2 请求参数
  
参数名称				        |类型		|出现要求	|描述  
:----						|:---		|:------	|:---	
&emsp;mac				    |string		|R			|设备id
&emsp;start_time		    |int		|R			|开始时间
&emsp;end_time				|int		|R			|结束时间
&emsp;timestamp				|int		|R			|时间戳
&emsp;asc				    |bool		|O			|排序 正序or倒叙
&emsp;offset				|int		|O			|偏移量
&emsp;limit				    |int		|O			|最大返回数量 不得超过200条

请求示例：

```
 https://apis.cleargrass.com/v1/apis/devices/data?mac=582D3446029C&end_time=1573527615&limit=200&start_time=1573354814&timestamp=1573527615
```


#### 3.4.3 返回结果

参数名称						            |类型		|出现要求	|描述  
:----						            |:---		|:------	|:---	
total						            |int		|R			|总条数
data						            |object		|R			|数据正文
&emsp;battery				            |object		|C			|电量 
&emsp;humidity				            |object		|C			|湿度 
&emsp;pressure				            |object		|C			|气压 
&emsp;temperature			            |object		|C			|温度 
&emsp;timestamp			                |object		|R			|时间戳
&emsp;&emsp;value			            |float		|R			|数值

示例：

```
{
    "total": 22,
    "data": [
        {
            "battery": {"value": 70},
            "humidity": {"value": 22.2},
            "pressure": {"value": 103.29},
            "temperature": {"value": 20.8},
            "timestamp": {"value": 1574565267}
        },
        {
            "battery": {"value": 70},
            "humidity": {"value": 22.2},
            "pressure": {"value": 103.29},
            "temperature": {"value": 20.8},
            "timestamp": {"value": 1574565267}
        }
    ]
}
```

### 3.5 设备历史事件
- **接口说明：** 设备历史事件
- **接口方法：** GET
- **接口地址：** /v1/apis/devices/events

#### 3.5.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格

#### 3.5.2 请求参数
  
参数名称					    |类型		|出现要求	|描述  
:----						|:---		|:------	|:---
&emsp;mac				    |string		|R			|设备id
&emsp;start_time		    |int		|R			|开始时间
&emsp;end_time				|int		|R			|结束时间
&emsp;timestamp				|int		|R			|时间戳
&emsp;offset				|int		|O			|偏移量
&emsp;limit				    |int		|O			|最大返回数量 不得超过200条



请求示例：

```
https://apis.cleargrass.com/v1/portal/apis/devices/events?mac=582D3446029C&end_time=1573527615&limit=200&start_time=1573354814&timestamp=1573527615
```

#### 3.5.3 返回结果

参数名称						            |类型		|出现要求	|描述  
:----						            |:---		|:------	|:---	
total						            |int		|R			|总条数
events						            |object		|R			|数据正文
&emsp;data				                |object		|C			|电量 
&emsp;&emsp;battery				        |object		|C			|电量 
&emsp;&emsp;humidity				    |object		|C			|湿度 
&emsp;&emsp;pressure				    |object		|C			|气压
&emsp;&emsp;temperature			        |object		|C			|温度
&emsp;&emsp;timestamp			        |object		|R			|时间戳
&emsp;&emsp;&emsp;value			        |float		|R			|数值
&emsp;alert_config				        |object		|C			|触发条件
&emsp;&emsp;metric_name			        |string		|R			|选项(温度、湿度、气压...)
&emsp;&emsp;operator			        |string		|R			|操作符(大于gt、小于lt)
&emsp;&emsp;threshold			        |float		|R			|阈值

示例：

```
{
    "total":20,
    "events":[
        {
            "data": {
                "battery": {"value": 70},
                "humidity": {"value": 22.2},
                "pressure": {"value": 103.29},
                "temperature": {"value": 20.8},
                "timestamp": {"value": 1574565267}
            },
            "alert_config": {
                "metric_name": "temperature",
                "operator": "gt",
                "threshold": 15,
            }
        },
        {
            "data": {
                "battery": {"value": 70},
                "humidity": {"value": 22.2},
                "pressure": {"value": 103.29},
                "temperature": {"value": 20.8},
                "timestamp": {"value": 1574565267}
            },
            "alert_config": {
                "metric_name": "temperature",
                "operator": "gt",
                "threshold": 16,
            }
        }
    ]
}
```


### 3.6 修改设备配置
- **接口说明：** 修改设备配置
- **接口方法：** PUT
- **接口地址：** /v1/apis/devices/settings

#### 3.6.1 请求头
参数名称						    |参数值		        |描述 
:----						    |:---		        |:---
&emsp;Authorization				|token		        |格式为 "Bearer YouToken",注意Bearer与token直接有一个空格
&emsp;Content-Type				|application/json	|固定值

#### 3.6.2 请求参数
  
参数名称					    |类型		    |出现要求	    |描述  
:----						|:---		    |:------	|:---
&emsp;mac		            |[]string		|R			|mac地址
&emsp;report_interval		|int		    |R			|上报时间(秒)
&emsp;collect_interval		|int		    |R			|采集时间(秒)

请求示例：
```
https://apis.cleargrass.com/v1/portal/apis/devices/settings
// json body
{
    "mac": ["582D34460442"],
    "report_interval": 10,
    "collect_interval": 5
}
```