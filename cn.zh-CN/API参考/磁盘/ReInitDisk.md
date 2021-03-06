# ReInitDisk {#doc_api_1030734 .reference}

重新初始化云盘到创建时的初始状态。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   云盘的状态必须为 使用中（In\_use），且挂载的 ECS 实例的状态必须为 已停止 （Stopped）。
-   实例首次启动前，不能重新初始化挂载在其上的云盘。
-   对于系统盘，初始化到镜像的最初状态。若创建云盘的源镜像被删除，则无法初始化。
-   对于直接创建的数据盘，初始化到空盘状态。
-   对于通过快照创建的数据盘，初始化到快照状态。若源快照已被删除，则无法初始化并返回错误。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ReInitDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|指定的云盘 ID。

 |
|Action|String|否|ReInitDisk|系统规定参数。取值：ReInitDisk。

 |
|AutoStartInstance|Boolean|否|true|重新初始化云盘后是否启动实例。

 |
|KeyPairName|String|否|JoshuaCentOS|密钥对名称。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|Password|String|否|EcsV587!|密码。

 |
|SecurityEnhancementStrategy|String|否|Active|当指定的云盘为系统盘时，您可以设置是否开启安全加固，加载云服务器 ECS 安全组件云盾等。取值范围：

 -   Active：启用安全加固，免费安装云盾。该值仅支持公共镜像。
-   Deactive：不启用安全加固，卸载云盾等安全组件。该值支持所有镜像。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ReInitDisk
&DiskId=d-diskid1
&Password=EcsV587!
&KeyPairName=JoshuaCentOS
&AutoStartInstance=true
&SecurityEnhancementStrategy=Active
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ReInitDiskResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReInitDiskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|InvalidSnapshot.TooOld|The disk is created from a snapshotId made before 2013-07-15, it cannot be re-initiated the specified disk any more since the detached first time.|指定的快照创建时间不能晚于2013年7月15日。|
|403|OperationDenied|The snapshot which is used to create the specified disk has been deleted.|用来创建指定磁盘的快照不存在。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|InvalidSourceSnapshot|The snapshot which is used to create the specified disk has been deleted.|用于创建指定磁盘的快照已被删除。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|404|InvalidDiskId.OperationNotSupported|The operation is not supported due to image not exist.|指定的镜像不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

