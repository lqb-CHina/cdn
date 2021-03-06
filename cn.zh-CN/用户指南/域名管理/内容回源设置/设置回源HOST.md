# 设置回源HOST {#task_261642 .task}

如果您需要自定义CDN节点回源时需要访问的具体服务器域名，可以参照本文档，设置回源HOST的域名类型。回源HOST可选域名类型包括：加速域名、源站域名和自定义域名。

回源HOST指CDN节点在回源过程中，在源站访问的站点域名。

**说明：** 如果您的源站绑定了多个域名或站点时，您需要在自定义域名中，指定具体域名，否则回源会失败。

源站和回源HOST的区别：

-   源站：源站决定了回源时请求到的具体IP。
-   回源HOST：回源HOST决定了回源请求访问到该IP上的具体站点。

回源HOST的默认值为：

-   在您源站类型是**IP**的情况下，您的回源HOST类型默认为**加速域名**。
-   在您源站类型是**OSS域名**的情况下，您的回源HOST类型默认为**源站域名**。

示例：

-   在您的源站是域名源站`www.a.com`的情况下，您选择将回源HOST设置为`www.b.com`， 则实际回源的是`www.a.com`解析到的IP站点`www.b.com`。
-   在您的源站是IP源站`1.1.1.1`的情况下，您选择将回源HOST设置为`www.b.com`，则实际回源的是`1.1.1.1`对应的主机上的站点`www.b.com`。

1.  登录[CDN控制台](https://cdnnext.console.aliyun.com)。
2.  单击**域名管理**。
3.  在域名管理页面，单击目标域名后的**管理**。
4.  单击**回源配置**。
5.  在**回源HOST**区域框，单击**修改配置**。
6.  打开**回源HOST**开关，选择**域名类型**，单击**确定**，配置成功。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/5145/15585920403347_zh-CN.png)


