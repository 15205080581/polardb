# API概览 {#reference_gsw_ych_yfb .reference}

本文汇总了云数据库POLARDB所有可调用的API，各API的具体信息请参见相关文档。

## 地域 {#section_nby_h4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)|查看区域信息|

## 集群管理 {#section_arh_n4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateDBCluster](intl.zh-CN/API参考/集群管理/CreateDBCluster.md#)|创建数据库集群|
|[DescribeDBClusters](intl.zh-CN/API参考/集群管理/DescribeDBClusters.md#)|查看集群列表|
|[DescribeDBClusterAttribute](intl.zh-CN/API参考/集群管理/DescribeDBClusterAttribute.md#)|查看数据库集群的属性|
|[DescribeAutoRenewAttribute](intl.zh-CN/API参考/集群管理/DescribeAutoRenewAttribute.md#)|查询包年包月集群自动续费状态|
|[ModifyAutoRenewAttribute](intl.zh-CN/API参考/集群管理/ModifyAutoRenewAttribute.md#)|设置包年包月集群自动续费状态|
|[ModifyDBClusterMaintainTime](intl.zh-CN/API参考/集群管理/ModifyDBClusterMaintainTime.md#)|修改集群可运维时间|
|[ModifyDBClusterDescription](intl.zh-CN/API参考/集群管理/ModifyDBClusterDescription.md#)|修改数据库集群的备注名|
|[DeleteDBCluster](intl.zh-CN/API参考/集群管理/DeleteDBCluster.md#)|删除数据库集群|

## 节点管理 {#section_jwf_cbv_yfb .section}

|API|描述|
|:--|:-|
|[CreateDBNodes](intl.zh-CN/API参考/节点管理/CreateDBNodes.md#)|增加集群节点|
|[ModifyDBNodeClass](intl.zh-CN/API参考/节点管理/ModifyDBNodeClass.md#)|修改集群节点|
|[RestartDBNode](intl.zh-CN/API参考/节点管理/RestartDBNode.md#)|重启集群节点|
|[DeleteDBNodes](intl.zh-CN/API参考/节点管理/DeleteDBNodes.md#)|删除集群节点|

## 集群参数 {#section_ydc_t4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeDBClusterParameters](intl.zh-CN/API参考/集群参数/DescribeDBClusterParameters.md#)|查看集群的参数|
|[ModifyDBClusterParameters](intl.zh-CN/API参考/集群参数/ModifyDBClusterParameters.md#)|修改集群的参数|

## 访问地址 {#section_i41_s4h_yfb .section}

|API|描述|
|:--|:-|
|[DescribeDBClusterEndpoints](intl.zh-CN/API参考/访问地址/DescribeDBClusterEndpoints.md#)|查询集群地址|
|[CreateDBEndpointAddress](intl.zh-CN/API参考/访问地址/CreateDBEndpointAddress.md#)|创建集群地址|
|[CreateDBClusterEndpoint](intl.zh-CN/API参考/访问地址/CreateDBClusterEndpoint.md#)|创建自定义集群地址|
|[ModifyDBClusterEndpoint](intl.zh-CN/API参考/访问地址/ModifyDBClusterEndpoint.md#)|修改集群地址属性|
|[ModifyDBEndpointAddress](intl.zh-CN/API参考/访问地址/ModifyDBEndpointAddress.md#)|修改集群默认访问地址前缀|
|[DeleteDBEndpointAddress](intl.zh-CN/API参考/访问地址/DeleteDBEndpointAddress.md#)|删除集群地址（非自定义集群地址）|
|[DeleteDBClusterEndpoint](intl.zh-CN/API参考/访问地址/DeleteDBClusterEndpoint.md#)|释放自定义集群地址|

## 账号管理 {#section_f35_p4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateAccount](intl.zh-CN/API参考/账号管理/CreateAccount.md#)|创建账号|
|[DescribeAccounts](intl.zh-CN/API参考/账号管理/DescribeAccounts.md#)|查看账号列表|
|[ModifyAccountDescription](intl.zh-CN/API参考/账号管理/ModifyAccountDescription.md#)|修改账号备注|
|[ModifyAccountPassword](intl.zh-CN/API参考/账号管理/ModifyAccountPassword.md#)|修改账号密码|
|[GrantAccountPrivilege](intl.zh-CN/API参考/账号管理/GrantAccountPrivilege.md#)|账号授权|
|[RevokeAccountPrivilege](intl.zh-CN/API参考/账号管理/RevokeAccountPrivilege.md#)|撤销账号权限|
|[ResetAccount](intl.zh-CN/API参考/账号管理/ResetAccount.md#)|重置账号权限|
|[DeleteAccount](intl.zh-CN/API参考/账号管理/DeleteAccount.md#)|删除账号|

## 数据库管理 {#section_tdx_q4h_yfb .section}

|API|描述|
|:--|:-|
|[CreateDatabase](intl.zh-CN/API参考/数据库管理/CreateDatabase.md#)|创建数据库|
|[DescribeDatabases](intl.zh-CN/API参考/数据库管理/DescribeDatabases.md#)|查看数据库列表信息|
|[ModifyDBDescription](intl.zh-CN/API参考/数据库管理/ModifyDBDescription.md#)|修改数据库描述|
|[DeleteDatabase](intl.zh-CN/API参考/数据库管理/DeleteDatabase.md#)|删除数据库|

## 标签管理 {#section_1nx_20e_xog .section}

|API|描述|
|:--|:-|
|[TagResources](intl.zh-CN/API参考/标签管理/TagResources.md#)|创建标签|
|[UntagResources](intl.zh-CN/API参考/标签管理/UntagResources.md#)|删除标签|

