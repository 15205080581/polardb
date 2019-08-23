# Client error codes {#reference_dg3_g5p_yfb .reference}

## Common errors {#section_wch_ymn_12b .section}

|Error code|Error message|HTTP status code|
|:---------|:------------|:---------------|
|MissingParameter|The input parameter "parameter name" that is mandatory for processing this request is not supplied.|400|
|InvalidParameter|The specified parameter "Action or Version" is not valid.|400|
|InvalidAccessKeyId.NotFound|The Access Key ID provided does not exist in our records.|404|
|IncompleteSignature|The request signature does not conform to Aliyun standards.|400|
|IllegalTimestamp|The input parameter "Timestamp" that is mandatory for processing this request is not supplied.|400|
|InvalidOwnerId|The specified OwnerId is not valid.|400|
|InvalidOwnerAccount|The specified OwnerAccount is not valid.|400|
|InvalidOwner|OwnerId and OwnerAccount can't be used at one API access.|400|
|Throttling|Request was denied due to request throttling.|400|
|InvalidAction|The specified action is not valid.|403|
|ActionUnauthorized|The specified action is not available for you|403|
|UnsupportedHTTPMethod|This http method not supported.|403|
|UnsupportedParameter|The parameter "<parameter name\>" is not supported.|400|
|Forbidden.ClusterNotFound|The specified DB Cluster does not exist.|404|
|Forbidden.RAM|The user is not authorized to operate the specified resource, or this operation does not support RAM.|403|
|Forbedden.NotSupportRAM|This action does not support accessed by RAM mode.|403|
|Forbidden.RiskControl|This operation is forbidden by Aliyun Risk Control system.|403|
|InsufficientBalance|Your account does not have enough balance.|400|
|Forbidden.Authentication|This operation is forbidden by Aliyun Realname Authentication system.|403|
|Invalid<parameter name\>.ValueNotSupported|The specified parameter "parameter name" is not valid.|400|
|Invalid<parameter name\>.Malformed|The specified parameter "parameter name n" is not valid.|400|
|InvalidParameter|The specified parameter "parameter name n" is not valid.|400|

## Specific errors {#section_ppn_2nn_12b .section}

|Error code|Error message|HTTP status code|
|:---------|:------------|:---------------|
|InvalidRegionId.NotFound|The DBClusterId provided does not exist in our records.|404|
|InvalidSecurityIPs.Duplicate|The Security IP address is not in the available range or occupied.|400|
|InvalidSecurityIPsLength.Malformed|The security IP address is beyond the available range or is already used.|400|
|InvalidEngineVersionInRegion.NotAvailable|The EngineVersion in the Region is not available.|403|
|InvaildEngineInRegion.NotAvailable|The Engine in the Region is not available.|403|
|OperationDenied|The resource is out of usage.|403|
|RegionUnauthorized|There is no authority to create Cluster in the specified region.|403|
|QuotaExceeded.CreateDBCluster|The quota of create Cluster exceeds.|403|
|InvalidDBClusterId.NotFound|The specified DBClusterId does not exist.|404|
|OperationDenied.DBClusterStatus|The operation is not permitted due to Cluster status.|403|
|InvalidConnectionStringPrefix.Duplicate|The connection string is not in the available range or occupied.|400|
|QuotaExceeded.SwitchTime|The quota of switch time exceed.|400|
|OperationDenied.LockMode|The operation is not permitted due to lock of Cluster.|403|
|InvalidSecurityIps.Duplicate|The quota of security ip exceeds.|400|
|OperationDenied.CurrentEngineVersion|The operation is not permitted due to specified current version.|400|
|QuotaExceeded.DBName|The quota of db exceeds.|400|
|InvalidDBName.Duplicate|The specified DB name is invalid or already exists.|400|
|InvalidParameter.Keyword|The specified DBName is a reserved keyword.|400|
|OperationDenied.DBStatus|The status of the database does not support this operation.|403|
|OperationDenied.DBClusterEngine|The operation is not permitted due to engine of Cluster.|403|
|InvalidDBInfo.Malformed|The specified parameter "DBInfo" is not valid or db not exist.|400|
|OperationDenied.Region|The operation is not permitted due to different region.|403|
|OperationDenied.Engine|The operation is not permitted due to different engine.|403|
|InvalidTaskId.NotFound|The ImportId provided does not exist in our records.|400|
|OperationDenied.IncorrectTaskStatus|The operation is not permitted due to status of import.|403|
|InvalidAccountName.keyword|The specified AccountName is a reserved keyword.|400|
|InvalidAccountName.Duplicate|The specified AccountName already exists.|400|
|QuotaExceeded.AccountName|The quota of account exceeds.|403|
|OperationDenied.AccountStatus|The status of the account does not support this operation.|403|
|InvalidDBName.NotFound|The specified database does not exist.|404|
|OperationDenied.AccountType|The operation is not permitted due to type of account.|403|
|OperationDenied.BackupJobExists|You cannot perform this operation; a backup job exists.|403|
|OperationDenied.NoDatabase|The operation is not permitted due to no database.|403|
|InvalidStartTimeAndEndTime.Malformed|The EndTime must be later than or equal to the StartTime.|400|
|OperationDenied.BackupJobExists|You cannot perform this operation; a backup job exists.|403|
|InvalidBackupId.NotFound|The BackupId provided does not exist in our records.|404|
|OperationDenied.NotFoundBackup|The operation is not permitted due to no backup.|403|
|OperationDenied.BackupStatus|The operation is not permitted due to type of backup.|403|
|OperationDenied.BackupMethod|The operation is not permitted method of backup.|403|
|Forbidden.Authentication|The operation is forbidden by Aliyun Realname Authentication System.|403|
|IncorrecttVpcId.Mismatch|The specified parameter "VpcId" is not valid.|400|
|IntranetNetTypeNotExists|Current DB Cluster net type does not support this operation.|404|
|InvalidDBCluster.NotFound|The DBClusterId provided does not exist in our records.|403|
|InvalidConnectionString.Duplicate Specified|connection string or port want to be modified is the same with current net type.|400|
|InvalidConnectionStringPrefix.Duplicated|The specified connection string already exists.|403|
|InvalidCurrentConnectionString.NotFound|Specified current connection string doesn't exist.|400|
|InvalidDBClusterId.NotFound|The specified DBClusterId does not exist.|400|
|InvalidDBClusterNetType.NotFound|The Specified DB Cluster net type is not found.|404|
|InvalidEngineVersion.Malformed|The specified parameter "EngineVersion" is not valid.|400|
|InvalidClusterNetworkType.ValueNotSupported|The specified parameter "ClusterNetworkType" is not valid.|400|
|InvalidPort.Malformed|Specified port is not valid.|400|
|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|400|
|InvalidPrivateIpAddress.Mismatch|Specified private IP address is not in the CIDR block of virtual switch.|400|
|InvalidVPCId.NotFound|The specified connection string or port does not match the current network type.|400|
|InvalidVSwitchId.Mismatch|Specified Cluster and virtual switch are not in the same zone.|400|
|InvalidVSwitchId.NotFound|Specified virtual switch is not found in specified VPC.|400|
|NetTypeExists|Specified net type already existed.|400|
|NetTypeExists|Specified public net type already existed.|403|
|OperationDenied.DBClusterNetType|The network type of the specified Cluster does not support this operation.|403|
|OperationDenied.LockMode|The Cluster is locked.|403|
|OperationDenied|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|403|
|OperationDenied|The vpc cloudClusterIp is use, please check params.|406|
|OperationDenied|The vpc service is error, please check params.|400|
|PublicConnectionExists|PublicConnection exists.|403|
|IncorrectDBClusterState|CurrentDB Cluster state does not support this operation.|403|
|IncorrectDBClusterLockMode|CurrentDB Cluster lock mode does not support this operation.|400|
|EngineVersionNotSupported|EngineVersion specified cannot be replicate with the source DB Cluster.|400|
|EngineNotSupported|Engine specified cannot be supported the operation..|400|

