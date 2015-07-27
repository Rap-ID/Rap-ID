Web API Document
=====

Version: `v1.1.1`

Draftsman: coderfox

Reviewer: coderfox

/api/reg
-----

`POST`Registry a user.

### Parameters

Parameters should be packed in form or JSON.

|Type|Name|Explanation|Required|
|-|-|-|-|
|string|username|username|*|
|string|password|password|*|

### Result

`JSON`

```
{
    "data" : 0,
    "error" : {
        "id" : 0,
        "msg" : "OK"
    }
}
```

|XPath|Type|Explanation|
|-|-|-|
|/data|int|0 represents ok.|
|/error|object|See [Error Reference](Error_Reference_Web_API).|

/api/login
-----

`POST`Login.

### Parameters

Parameters should be packed in form or JSON.

|Type|Name|Explanation|Required|
|-|-|-|-|
|string|username|username|*|
|string|password|password|*|
|string|iccid|ICCID||

### Result

`JSON`

```
{
    "data" : "420e57b017066b44e05ea1577f6e2e12",
    "error" : {
        "id" : 0,
        "msg" : "OK"
    }
}
```

|XPath|Type|Explanation|
|-|-|-|
|/data|string|token|
|/error|object|See [Error Reference](Error_Reference_Web_API).|

/api/user
-----

`GET`Get the data with a token.

### Parameters

Parameters should be packed in query string.

|Type|Name|Explanation|Required|
|-|-|-|-|
|string|token|token|*|

### Result

`JSON`

```
{
    "data" : {
        "uid" : 1,
        "username" : "foobar",
        "identity" : {
            "name" : "Zhao Si",
            "identity" : "21010119491001001X"
        }
    },
    "error" : {
        "id" : 0,
        "msg" : "OK"
    }
}
```

|XPath|Type|Explanation|
|-|-|-|
|/data|object|User information|
|/data/uid|int|UID|
|/data/username|string|username|
|/data/identity|object|Real-name information|
|/data/identity/name|string|Real name|
|/data/identity/identity|string|ID card no.|
|/error|object|See [Error Reference](Error_Reference_Web_API).|

### Notes

In the result, `/data/identity` can be null if no real-name data is found in the database. In this case, the `/error` would be not 0.

/api/auth
-----

`GET/POST`Displays a simple page guiding user to Rap-ID desktop version.

### Parameters

|Type|Name|Explanation|Required|
|-|-|-|-|
|string|app|Application key|*|
|string|callback|Callback url|*|

### Notes

The web page will start the authentication in 1 second with the URI API provided by
Rap-ID-Windows.