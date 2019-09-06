# OpenJump访问Ganos {#task_2022234 .task}

OpenJUMP是一套基于Java桌面GIS应用程序，其内置了地图可视化功能，可以用来实现特定的空间分析计算，包括Buffer缓冲区分析、Intersection叠加求交、Union叠加求和等空间分析功能，并可以通过插件方式为OpenJUMP进行功能的定制或拓展。

## 创建Ganos连接 {#section_xv3_kou_4f9 .section}

1.  在软件界面选择**文件** \> **打开**，选择**数据存储层**。
2.  在**连接管理器**中选择**新增**。
3.  在添加连接对话框中填入连接参数。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605559/156773815958804_zh-CN.png)

    参数说明如下。

    |参数|说明|
    |--|--|
    |名称|自定义的连接名称。|
    |驱动程序|指定为**PostGIS**。|
    |Server|数据库实例的IP地址或RDS/POLARDB外网地址，可以从控制台中获得。|
    |Port|数据库实例的端口地址，可以从控制台中获得。|
    |Database|需要连接的数据库名。|
    |User|数据库用户名。|
    |Password|密码。|

4.  单击**确定**后可以看到ganos库中所有的图层信息。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605559/156773815958806_zh-CN.png)


## 数据浏览与操作 {#section_e90_jbf_pw9 .section}

连接后可以对数据进行浏览，可以进行放大，缩小，漫游等基本操作，也可以进行符号化渲染等。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605559/156773816058807_zh-CN.png)

也可以对几何对象进行属性查询。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605559/156773816058808_zh-CN.png)

