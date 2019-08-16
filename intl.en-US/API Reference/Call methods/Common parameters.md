# Common parameters {#reference_ug4_y4h_yfb .reference}

Common parameters, which consist of common request parameters and common response parameters, are required by all API operations.

## Common request parameters {#section_yld_tth_yfb .section}

The following table describes common request parameters required by all API requests.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Format|String|No|The format of the response. Valid values: JSON and XML. Default value: JSON.|
|Version|String|Yes|The API version, in YYYY-MM-DD format. The current version is 2017-08-01.|
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Yes|The calculated signature string. For more information about how to calculate a signature, see [Signature mechanism](intl.en-US/API Reference/Call methods/Signature mechanism.md#).|
|SignatureMethod|String|Yes|The signature algorithm. Currently, only HMAC-SHA1 is supported.|
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. For example, a value of `2013-08-15T12:00:00Z` indicates 20:00:00 on August 15, 2013, UTC+8.|
|SignatureVersion|String|Yes|The version of the signature algorithm. The current version is 1.0.|
|SignatureNonce|String|Yes|The unique random number that is used to prevent replay attacks. You must use different random numbers for different requests.|

## Common response parameters {#section_afh_15h_yfb .section}

The system returns a unique ID \(RequestId\) for each API request, regardless of the request result.

## Sample request {#section_pw5_d5h_yfb .section}

```
https://rds.aliyuncs.com/
? Format=xml
&Version=2014-08-15
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D 
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=key-test
&OwnerId=12345678
&Timestamp=2014-10-10T12:00:00Z
```

## Sample response {#section_fqw_g5h_yfb .section}

After you send an API request, the system returns a response in a uniform format. A returned HTTP status code 2xx indicates that the request is successful. A returned HTTP status code 4xx or 5xx indicates that the request fails. The system returns a success response in XML or JSON format. You can specify the format of the response in request parameters. The default format is XML. For the sake of readability, lines in all sample responses are wrapped and indented in the API reference. Note that lines are not formatted in actual responses.

Sample success response

XML format

```
<? xml version="1.0" encoding="utf-8"? > 
<!—Result root node-->
<Operation+Response>
    <!—Tag of the response to the request-->
    <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
    <!—Result data-->
</Operation+Response>
```

JSON format

```
{
    "RequestId": "4C467B38-3910-447D-87BC-AC049166F216",
    /* Result data */
}
```

Sample error response

If an error occurs during an API operation, the system does not return result data. You can identify the cause of the error according to [Client error codes](intl.en-US/API Reference/Appendixes/Client error codes.md#).

If you send an HTTP request, the system returns an HTTP status code 4xx or 5xx to indicate an error. The returned response body contains the specific error code and error message. It also contains the globally unique request ID \(RequestId\) and the requested host ID \(HostId\). If you cannot identify the cause of the error, you can contact the Alibaba Cloud customer service staff and provide the returned HostId and RequestId to help the staff resolve the error.

XML format

```
<? xml version="1.0" encoding="UTF-8"? >
<Error>
   <RequestId>8906582E-6722-409A-A6C4-0E7863B733A5</RequestId>
   <HostId>rds.aliyuncs.com</HostId>
   <Code>UnsupportedOperation</Code>
   <Message>The specified action is not supported. </Message>
</Error>
```

JSON format

```
{
    "RequestId": "7463B73D-35CC-4D19-A010-6B8D65D242EF",
    "HostId": "rds.aliyuncs.com",
    "Code": "UnsupportedOperation",
    "Message": "The specified action is not supported."
}
```

