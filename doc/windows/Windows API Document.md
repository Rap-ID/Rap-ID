Rap-ID Windows API文档
=====

Version: `v1.0`

Draftsman: coderfox

Reviewer: coderfox

Working Method
-----

1. URL Protocol
2. CLI

URL Protocol
-----

### Definition

The program have registered a URL Protocol of `rapid://`.

### Step

1. Open *URL Protocol Page*
2. Rap-ID handles request
3. Rap-ID opens callback page

### URL

The URL looks like:

```
rapid://authorize/?app=APPLICATIONKEY&callback=CALLBACK
```

#### Explanation

`APPLICATIONKEY`is the identity of an application, which tells the name of the application.

`CALLBACK` is the callback page URL.

When calling back, Rap-ID will attach `token` after `CALLBACK`. If there is any problems, the result will be `ERROR`.

### Example

When launching the URL below:

```
rapid://authorize/http%3a%2f%2fexample.com%2fRap-ID-callback.html%3ftoken%3d
```

You will be called back to:

```
http://example.com/Rap-ID-callback.html?token=aj5b1s02eokusotu0ej0l9c5m1
```

### HINT

You can open a user-friendly page with the Rap-ID Web API. See [Web API Document v1.1.1](https://github.com/Rap-ID/Rap-ID/blob/c73704e18350e1300af0bbfc6bfd3d7e81c7c493/doc/server/Web%20API%20Document.md#apiauth)

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
