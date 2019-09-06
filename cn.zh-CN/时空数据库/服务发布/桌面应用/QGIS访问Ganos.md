# QGIS访问Ganos {#task_2022215 .task}

QGIS（原称Quantum GIS）是一个用户界面友好的开源桌面端软件，支持多种矢量、栅格格式以及数据库作为数据源，同时支持数据的可视化、管理、编辑、分析以及印刷地图的制作。

## 创建Ganos连接 {#section_xv3_kou_4f9 .section}

1.  直接创建PostGIS Connection，填入必要项参数，点击**Test Connection**。 

    ![](images/58794_zh-CN.jpeg)

    参数说明如下。

    |参数|说明|
    |--|--|
    |Name|自定义连接名。|
    |Host|数据库实例的IP地址或RDS/POLARDB外网地址，可以从控制台中获得。|
    |Port|数据库实例的端口地址，可以从控制台中获得。|
    |Database|需要连接的数据库名。|
    |SSL Mode|SSL加密状态，选择**Disable**。|

2.  找到建立的Ganos数据源，显示出已有的数据库实例以及实例下的空间图层，双击指定的空间图层，即可浏览、查看、编辑Ganos中的空间数据。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605527/156773819058795_zh-CN.png)


