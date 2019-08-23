# Signature mechanism {#concept_kcb_vb3_yfb .concept}

ApsaraDB for POLARDB authenticates each user who sends an API request. Therefore, no matter whether you send an HTTP or HTTPS request, the request must contain signature information. ApsaraDB for POLARDB performs symmetric encryption by using the AccessKey ID and AccessKey secret to authenticate each request sender. The AccessKey ID and AccessKey secret are officially issued by Alibaba Cloud to users. You can request and manage them on the Alibaba Cloud official website. The AccessKey ID indicates the identity of a user. The AccessKey secret is the key used to encrypt the signature string and verify the signature string on the server. The AccessKey secret must be kept strictly confidential and be known only to Alibaba Cloud and the user.

When you send an API request, you need to generate a signature for the request as follows:

1.  Use request parameters to construct a canonicalized query string.
    1.  Sort all request parameters \(including the common request parameters described in the "Common parameters" topic and the operation-specific parameters, but excluding the Signature parameter\) in the lexicographic order of parameter names.

        **Note:** If you use the GET method to submit a request, the request parameters are included in the request URL. They are connected by an ampersand \(&\) after the question mark \(?\) in the request URL.

    2.  Encode the name and value of each request parameter. Use UTF-8 to perform URL encoding. The URL encoding rules are as follows:
        1.  1.  Do not encode uppercase letters \(A-Z\), lowercase letters \(a-z\), digits \(0-9\), and characters including the hyphen \(-\), underscore \(\_\), period \(.\), and tilde \(~\).
2.  Encode other characters into the %XY format, where XY is the hexadecimal value of the ASCII code corresponding to a character. For example, a double quotation mark \("\) is encoded as %22.
3.  Encode the extended UTF-8 characters into the %XY%ZA… format.
4.  Encode a space \( \) as %20 but not the plus sign \(+\).

    **Note:** Generally, all the libraries that support URL encoding \(for example, java.net.URLEncoder\) perform encoding according to the rule of the "application/x-www-form-urlencoded" MIME type. If you use this encoding method, you can replace the plus sign \(+\) with %20, the asterisk \(\*\) with %2A, and %7E with the tilde \(~\) in the encoded string to obtain the required string.

    3.  Use an equal sign \(=\) to connect the name and value of each URL encoded request parameter as a key-value pair.
    4.  Sort the key-value pairs of the URL encoded request parameters in the lexicographic order of parameter names and connect them with an ampersand \(&\) to obtain the canonicalized query string.
2.  Use the canonicalized query string obtained in step 1 to construct the StringToSign string according to the following rules:

    ```
    StringToSign=
    HTTPMethod + "&" +
    percentEncode("/") + "&" +
    percentEncode(CanonicalizedQueryString)
    ```

    The parameters are described as follows:

    -   -   HTTPMethod: the HTTP method used to submit the request, such as GET.
-   percentEncode\("/"\): the encoded value of a forward slash \(/\) according to the URL encoding rules described in 1.b. The encoded value is %2F.
-   percentEncode\(CanonicalizedQueryString\): the string encoded by using the canonicalized query string constructed in step 1. The encoding follows the URL encoding rules described in 1.ii.
3.  Use the StringToSign string to calculate the HMAC value of the signature as defined by RFC2104.

    **Note:** The key used for signature calculation is your AccessKey secret appended with an ampersand \(&\) \(ASCII code: 38\). The hash algorithm used is SHA1.

4.  Encode the HMAC value into a string according to the Base64 encoding rules to obtain the signature string.
5.  Add the signature string as the value of the Signature parameter to the request parameters to complete the signature generation process.

    **Note:** 

    Before submitting the Signature parameter to the ApsaraDB for POLARDB server as a request parameter, you must also perform URL encoding for the name and value of the Signature parameter according to RFC3986.

    For example, the request URL without a signature for the DescribeCdnService operation is:

    ```
    http://polardb.aliyuncs.com/?Timestamp=2013-06-01T10:33:56Z&Format=XML&AccessKeyId=testid&Action=DescribeDBClusters&SignatureMethod=HMAC-SHA1&RegionId=region1&SignatureNonce=NwDAxvLU6tFE0DVb&Version=2014-08-15&SignatureVersion=1.0
    ```

    The constructed StringToSign string is:

    ```
    GET&%2F&AccessKeyId%3Dtestid&Action%3DDescribeDBClusters&Format%3DXML&RegionId%3Dregion1&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3DNwDAxvLU6tFE0DVb&SignatureVersion%3D1.0&TimeStamp%3D2013-06-01T10%253A33%253A56Z&Version%3D2014-08-15
    ```

    Assume that the AccessKey ID is testid and the AccessKey secret is testsecret. Then, the Key used to calculate the HMAC value of the signature is testsecret&. The calculated signature string is `BIPOMlu8LXBeZtLQkJTw6iFvw1E=`.

    The request URL with the Signature parameter added is as follows:

    ```
    http://polardb.aliyuncs.com/?Timestamp=2013-06-01T10%3A33%3A56Z&Format=XML&AccessKeyId=testid&Action=DescribeDBClusters&SignatureMethod=HMAC-SHA1&RegionId=region1&SignatureNonce=NwDAxvLU6tFE0DVb&SignatureVersion=1.0&Version=2014-08-15&Signature=BIPOMlu8LXBeZtLQkJTw6iFvw1E%3D
    ```


