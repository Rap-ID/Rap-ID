Rap-ID Windows API文档
=====

Version: `v1.0-RC`

Draftsman: coderfox

Reviewer:

请求方式
-----

1. URL Protocol
2. CLI

URL Protocol
-----

### Definition

The program have registered a URL Protocol of `rapid://`.

### 请求流程

1. 链接到URL Protocol页面
2. Rap-ID进行授权
3. Rap-ID打开指定回调的页面

### URL

页面的URL应当形如：

```
rapid://authorize/?app=APPLICATIONKEY&callback=CALLBACK
```

#### 说明

`APPLICATIONKEY`为应用标识码，可以确定一个应用的名称。请向平台维护者索要。

`CALLBACK`为回调页面的URL经过URL Encode的结果。

执行回调时Rap-ID会将`token`附加在`CALLBACK`后。如果授权出现问题，回复的token将为`ERROR`

#### 示例

打开的URL应当形如：

```
rapid://authorize/http%3a%2f%2fexample.com%2fRap-ID-callback.html%3ftoken%3d
```

而Rap-ID打开的回调页为：

```
http://example.com/Rap-ID-callback.html?token=aj5b1s02eokusotu0ej0l9c5m1
```

CLI
-----

### How

You may start `auth.exe` with only one parameter of your application name, and
then listen to the standard output. You may get something starting like this:

```
#Rap-ID-Windows/CLI/1.0d/Auth/
```

For example,

```
#Rap-ID-Windows/CLI/1.0d/Auth/result=ok;token=foobar
```

As this line defined 2 variables, result and token, you may get the token and the
result. The `result` can be `ok` or `fail`. If the `result` is `fail`, you may be
provided another variable called `error` providing details.

### Notes

You may get the absolute path of `auth.exe` in the registry. The path of the record
is `HKEY_CLASSES_ROOT/rapid/dir/auth`.

You may get the install path of Rap-ID at path `HKEY_CLASSES_ROOT/rapid/dir`.