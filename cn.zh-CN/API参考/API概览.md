# API概览 {#reference_gsw_ych_yfb .reference}

本文汇总了云数据库POLARDB所有可调用的API，各API的具体信息请参见相关文档。

## 地域 {#section_nby_h4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeRegions](cn.zh-CN/API参考/地域/DescribeRegions.md#)|查看区域信息|

## 集群管理 {#section_arh_n4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateDBCluster](cn.zh-CN/API参考/集群管理/CreateDBCluster.md#)|创建数据库集群|
|[DescribeDBClusters](cn.zh-CN/API参考/集群管理/DescribeDBClusters.md#)|查看集群列表|
|[DescribeDBClusterAttribute](cn.zh-CN/API参考/集群管理/DescribeDBClusterAttribute.md#)|查看数据库集群的属性|
|[DescribeAutoRenewAttribute](cn.zh-CN/API参考/集群管理/DescribeAutoRenewAttribute.md#)|查询包年包月集群自动续费状态|
|[ModifyAutoRenewAttribute](cn.zh-CN/API参考/集群管理/ModifyAutoRenewAttribute.md#)|设置包年包月集群自动续费状态|
|[ModifyDBClusterMaintainTime](cn.zh-CN/API参考/集群管理/ModifyDBClusterMaintainTime.md#)|修改集群可运维时间|
|[ModifyDBClusterDescription](cn.zh-CN/API参考/集群管理/ModifyDBClusterDescription.md#)|修改数据库集群的备注名|
|[DeleteDBCluster](cn.zh-CN/API参考/集群管理/DeleteDBCluster.md#)|删除数据库集群|

## 节点管理 {#section_jwf_cbv_yfb .section}

|API|描述|
|:--|:-|
|[CreateDBNodes](cn.zh-CN/API参考/节点管理/CreateDBNodes.md#)|增加集群节点|
|[ModifyDBNodeClass](cn.zh-CN/API参考/节点管理/ModifyDBNodeClass.md#)|修改集群节点|
|[RestartDBNode](cn.zh-CN/API参考/节点管理/RestartDBNode.md#)|重启集群节点|
|[DeleteDBNodes](cn.zh-CN/API参考/节点管理/DeleteDBNodes.md#)|删除集群节点|

## 集群参数 {#section_ydc_t4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeDBClusterParameters](cn.zh-CN/API参考/集群参数/DescribeDBClusterParameters.md#)|查看集群的参数|
|[ModifyDBClusterParameters](cn.zh-CN/API参考/集群参数/ModifyDBClusterParameters.md#)|修改集群的参数|

## 访问地址 {#section_i41_s4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeDBClusterEndpoints](cn.zh-CN/API参考/访问地址/DescribeDBClusterEndpoints.md#)|查询集群地址|
|[CreateDBEndpointAddress](cn.zh-CN/API参考/访问地址/CreateDBEndpointAddress.md#)|创建集群地址|
|[CreateDBClusterEndpoint](cn.zh-CN/API参考/访问地址/CreateDBClusterEndpoint.md#)|创建自定义集群地址|
|[ModifyDBClusterEndpoint](cn.zh-CN/API参考/访问地址/ModifyDBClusterEndpoint.md#)|修改集群地址属性|
|[ModifyDBEndpointAddress](cn.zh-CN/API参考/访问地址/ModifyDBEndpointAddress.md#)|修改集群默认访问地址前缀|
|[DeleteDBEndpointAddress](cn.zh-CN/API参考/访问地址/DeleteDBEndpointAddress.md#)|删除集群地址（非自定义集群地址）|
|[DeleteDBClusterEndpoint](cn.zh-CN/API参考/访问地址/DeleteDBClusterEndpoint.md#)|释放自定义集群地址|

## 账号管理 {#section_f35_p4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateAccount](cn.zh-CN/API参考/账号管理/CreateAccount.md#)|创建账号|
|[DescribeAccounts](cn.zh-CN/API参考/账号管理/DescribeAccounts.md#)|查看账号列表|
|[ModifyAccountDescription](cn.zh-CN/API参考/账号管理/ModifyAccountDescription.md#)|修改账号备注|
|[ModifyAccountPassword](cn.zh-CN/API参考/账号管理/ModifyAccountPassword.md#)|修改账号密码|
|[GrantAccountPrivilege](cn.zh-CN/API参考/账号管理/GrantAccountPrivilege.md#)|账号授权|
|[RevokeAccountPrivilege](cn.zh-CN/API参考/账号管理/RevokeAccountPrivilege.md#)|撤销账号权限|
|[ResetAccount](cn.zh-CN/API参考/账号管理/ResetAccount.md#)|重置账号权限|
|[DeleteAccount](cn.zh-CN/API参考/账号管理/DeleteAccount.md#)|删除账号|

## 数据库管理 {#section_tdx_q4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateDatabase](cn.zh-CN/API参考/数据库管理/CreateDatabase.md#)|创建数据库|
|[DescribeDatabases](cn.zh-CN/API参考/数据库管理/DescribeDatabases.md#)|查看数据库列表信息|
|[ModifyDBDescription](cn.zh-CN/API参考/数据库管理/ModifyDBDescription.md#)|修改数据库描述|
|[DeleteDatabase](cn.zh-CN/API参考/数据库管理/DeleteDatabase.md#)|删除数据库|

## 标签管理 {#section_1nx_20e_xog .section}

|API|描述|
|:--|:-|
|[TagResources](cn.zh-CN/API参考/标签管理/TagResources.md#)|创建标签|
|[UntagResources](cn.zh-CN/API参考/标签管理/UntagResources.md#)|删除标签|

