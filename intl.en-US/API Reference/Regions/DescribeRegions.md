# DescribeRegions {#reference_rwv_12s_xfb .reference}

You can call this operation to query regions and zones that are available for ApsaraDB for POLARDB.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeRegions.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|Regions|List|The list of regions.|

## Region {#section_ilc_b3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|RegionId|String|The ID of the region. For example, cn-hangzhou.|
|Zones|List|The list of zones.|

## Zone {#section_snj_c3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|ZoneId|String|The ID of the zone. For example, cn-hangzhou-g.|
|VpcEnabled|String|Indicates whether the zone supports VPC.|

## Sample request {#section_gkx_v2f_1gb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeRegions
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DescribeRegionsResponse>
	<Regions>
		<Region>
			<RegionId>cn-beijing</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-beijing-e</ZoneId>
				</Zone>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-beijing-g</ZoneId>
				</Zone>
			</Zones>
		</Region>
		<Region>
			<RegionId>cn-hangzhou</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-hangzhou-g</ZoneId>
				</Zone>
			</Zones>
		</Region>
		<Region>
			<RegionId>cn-shanghai</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-shanghai-d</ZoneId>
				</Zone>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-shanghai-e</ZoneId>
				</Zone>
			</Zones>
		</Region>
		<Region>
			<RegionId>cn-shenzhen</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-shenzhen-e</ZoneId>
				</Zone>
			</Zones>
		</Region>
		<Region>
			<RegionId>cn-hongkong</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-hongkong-c</ZoneId>
				</Zone>
			</Zones>
		</Region>
		<Region>
			<RegionId>cn-huhehaote</RegionId>
			<Zones>
				<Zone>
					<VpcEnabled>true</VpcEnabled>
					<ZoneId>cn-huhehaote-a</ZoneId>
				</Zone>
			</Zones>
		</Region>
	</Regions></DescribeRegionsResponse>
```

JSON format

```
{
    "Regions": {
        "Region": [
            {
                "RegionId": "cn-beijing", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-beijing-e"
                        }, 
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-beijing-g"
                        }
                    ]
                }
            }, 
            {
                "RegionId": "cn-hangzhou", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-hangzhou-g"
                        }
                    ]
                }
            }, 
            {
                "RegionId": "cn-shanghai", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-shanghai-d"
                        }, 
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-shanghai-e"
                        }
                    ]
                }
            }, 
            {
                "RegionId": "cn-shenzhen", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-shenzhen-e"
                        }
                    ]
                }
            }, 
            {
                "RegionId": "cn-hongkong", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-hongkong-c"
                        }
                    ]
                }
            }, 
            {
                "RegionId": "cn-huhehaote", 
                "Zones": {
                    "Zone": [
                        {
                            "VpcEnabled": true, 
                            "ZoneId": "cn-huhehaote-a"
                        }
                    ]
                }
            }
        ]
    }
}
```

