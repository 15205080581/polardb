# DescribeRegions {#reference_rwv_12s_xfb .reference}

该接口用于查询POLARDB支持的地域和可用区。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeRegions。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)|
|RequestId|String|RequestId|
|Regions|List|返回Region列表。|

## region参数 {#section_ilc_b3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|RegionId|String|地域ID，如cn-hangzhou。|
|Zones|List|可用区列表。|

## Zones参数 {#section_snj_c3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|ZoneId|String|可用区ID，如cn-hangzhou-g。|
|VpcEnabled|String|支持VPC。|

## 请求示例 {#section_gkx_v2f_1gb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeRegions
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

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

JSON格式

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

