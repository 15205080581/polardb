# API overview {#reference_gsw_ych_yfb .reference}

The following tables list API operations available for use in ApsaraDB for POLARDB. For more information, see OpenAPI Explorer.

## Regions {#section_nby_h4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#)|Queries available regions and zones.|

## Cluster management {#section_arh_n4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[CreateDBCluster](intl.en-US/API Reference/Cluster management/CreateDBCluster.md#)|Creates a POLARDB cluster.|
|[DescribeDBClusters](intl.en-US/API Reference/Cluster management/DescribeDBClusters.md#)|Queries POLARDB clusters.|
|[DescribeDBClusterAttribute](intl.en-US/API Reference/Cluster management/DescribeDBClusterAttribute.md#)|Queries the detailed information of a specified POLARDB cluster.|
|[DescribeAutoRenewAttribute](intl.en-US/API Reference/Cluster management/DescribeAutoRenewAttribute.md#)|Queries the auto renewal attribute of subscription POLARDB clusters.|
|[ModifyAutoRenewAttribute](intl.en-US/API Reference/Cluster management/ModifyAutoRenewAttribute.md#)|Sets the auto renewal attribute for a specified subscription POLARDB cluster.|
|[ModifyDBClusterMaintainTime](intl.en-US/API Reference/Cluster management/ModifyDBClusterMaintainTime.md#)|Modifies the maintenance window of a specified POLARDB cluster.|
|[ModifyDBClusterDescription](intl.en-US/API Reference/Cluster management/ModifyDBClusterDescription.md#)|Modifies the description of a specified POLARDB cluster.|
|[DeleteDBCluster](intl.en-US/API Reference/Cluster management/DeleteDBCluster.md#)|Deletes a specified POLARDB cluster.|

## Node management {#section_jwf_cbv_yfb .section}

|Operation|Description|
|:--------|:----------|
|[CreateDBNodes](intl.en-US/API Reference/Node management/CreateDBNodes.md#)|Adds a node to a specified POLARDB cluster.|
|[ModifyDBNodeClass](intl.en-US/API Reference/Node management/ModifyDBNodeClass.md#)|Changes the node specifications of a specified POLARDB cluster.|
|[RestartDBNode](intl.en-US/API Reference/Node management/RestartDBNode.md#)|Restarts a specified node of a POLARDB cluster.|
|[DeleteDBNodes](intl.en-US/API Reference/Node management/DeleteDBNodes.md#)|Deletes a node from a specified POLARDB cluster.|

## Cluster parameters {#section_ydc_t4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[DescribeDBClusterParameters](intl.en-US/API Reference/Cluster parameters/DescribeDBClusterParameters.md#)|Queries the parameters of a specified POLARDB cluster.|
|[ModifyDBClusterParameters](intl.en-US/API Reference/Cluster parameters/ModifyDBClusterParameters.md#)|Modifies the parameters of a specified POLARDB cluster.|

## Connection points {#section_i41_s4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[DescribeDBClusterEndpoints](intl.en-US/API Reference/Connection points/DescribeDBClusterEndpoints.md#)|Queries the connection point information of a specified POLARDB cluster.|
|[CreateDBEndpointAddress](intl.en-US/API Reference/Connection points/CreateDBEndpointAddress.md#)|Creates a public connection point for a specified POLARDB cluster.|
|[CreateDBClusterEndpoint](intl.en-US/API Reference/Connection points/CreateDBClusterEndpoint.md#)|Creates a custom connection point for a specified POLARDB cluster.|
|[ModifyDBClusterEndpoint](intl.en-US/API Reference/Connection points/ModifyDBClusterEndpoint.md#)|Modifies the connection point attributes of a specified POLARDB cluster.|
|[ModifyDBEndpointAddress](intl.en-US/API Reference/Connection points/ModifyDBEndpointAddress.md#)|Modifies the prefix of the default connection point for a specified POLARDB cluster.|
|[DeleteDBEndpointAddress](intl.en-US/API Reference/Connection points/DeleteDBEndpointAddress.md#)|Releases a public connection point for a specified POLARDB cluster.|
|[DeleteDBClusterEndpoint](intl.en-US/API Reference/Connection points/DeleteDBClusterEndpoint.md#)|Releases a custom connection point for a specified POLARDB cluster.|

## Account management {#section_f35_p4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[CreateAccount](intl.en-US/API Reference/Account management/CreateAccount.md#)|Creates a database account for a specified POLARDB cluster.|
|[DescribeAccounts](intl.en-US/API Reference/Account management/DescribeAccounts.md#)|Queries the database accounts of a specified POLARDB cluster.|
|[ModifyAccountDescription](intl.en-US/API Reference/Account management/ModifyAccountDescription.md#)|Modifies the description of a database account for a specified POLARDB cluster.|
|[ModifyAccountPassword](intl.en-US/API Reference/Account management/ModifyAccountPassword.md#)|Changes the password of a database account for a specified POLARDB cluster.|
|[GrantAccountPrivilege](intl.en-US/API Reference/Account management/GrantAccountPrivilege.md#)|Grants access permissions on one or more databases in a specified POLARDB cluster to a database account.|
|[RevokeAccountPrivilege](intl.en-US/API Reference/Account management/RevokeAccountPrivilege.md#)|Revokes access permissions on one or more databases for a database account of a specified POLARDB cluster.|
|[ResetAccount](intl.en-US/API Reference/Account management/ResetAccount.md#)|Resets the permissions of a database account for a specified POLARDB cluster.|
|[DeleteAccount](intl.en-US/API Reference/Account management/DeleteAccount.md#)|Deletes a database account for a specified POLARDB cluster.|

## Database management {#section_tdx_q4h_yfb .section}

|Operation|Description|
|:--------|:----------|
|[CreateDatabase](intl.en-US/API Reference/Database management/CreateDatabase.md#)|Creates a database for a specified POLARDB cluster.|
|[DescribeDatabases](intl.en-US/API Reference/Database management/DescribeDatabases.md#)|Queries the databases of a specified POLARDB cluster.|
|[ModifyDBDescription](intl.en-US/API Reference/Database management/ModifyDBDescription.md#)|Modifies the description of a database for a specified POLARDB cluster.|
|[DeleteDatabase](intl.en-US/API Reference/Database management/DeleteDatabase.md#)|Deletes a database for a specified POLARDB cluster.|

## Tag management {#section_1nx_20e_xog .section}

|Operation|Description|
|:--------|:----------|
|[TagResources](intl.en-US/API Reference/Tag management/TagResources.md#)|Creates tags for POLARDB clusters.|
|[UntagResources](intl.en-US/API Reference/Tag management/UntagResources.md#)|Deletes tags for POLARDB clusters.|

