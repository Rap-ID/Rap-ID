Rap-ID Intranet Communication Specification
=====

起草：小傅Fox

复核：小傅Fox

终审：

版本：0.5-draft2

加密
-----

参考*Rap-ID Encryption Key Generation Spec.*。

广播
-----

### 网络协议

UDP，端口49160

### 连接双方

手机端：广播`广播数据包`，范围为同网段

电脑端：侦听

### 广播数据包

```
$UNAME
```

#### 解释

`$UNAME` 用户名/昵称

#### 其他

广播数据包时间间隔：`1s`

#### 示例

```
UDP 192.168.1.255
小傅Fox
```

配对
-----

### 网络协议

TCP，端口49161

### 连接双方

手机端：侦听

电脑端：发起连接

### 步骤

1. 电脑端发送`配对请求数据包`
2. 手机端回应配对请求，发送`配对响应数据包`
3. 手机端主动关闭连接

### 配对请求数据包

```
PAIR$KEY
```

#### 说明

**注意：**数据包以`CRLF`结尾。

`$KEY`为指定的配对密钥，由手机端随机生成。

#### 示例

```
TCP 192.168.1.2--->>>192.168.1.3
PAIR1234
```

### 配对响应数据包

```
PAIROK$KEY_SENT
```

或

```
PAIRFAIL$KEY_SENT
```

#### 说明

**注意：**数据包以`CRLF`结尾。

`$KEY_SENT`为电脑端发送的`配对请求数据包`中提出的`$KEY`。

当配对成功时反馈第一种数据包，失败时反馈第二种数据包。

#### 示例

```
TCP 192.168.1.3--->>>192.168.1.2
PAIROK1234
```

#### 其他

本数据包指定的超时时限为`5s`

### 密钥交换数据包

```
$PASS
```

#### 说明

**注意：**数据包以`CRLF`结尾。

`$PASS`为生成的*the original seed*，按16进制HEX文本加密后发送。

#### 示例

```
TCP 192.168.1.3--->>>192.168.1.2
cf166a138a5b6ad5
```

#### 其他

本数据包指定的超时时限为`5s`

授权
-----

### 网络协议

TCP，端口49162

### 连接双方

手机端：侦听

电脑端：发起连接

### 步骤

1. 电脑端发送`授权请求数据包`
2. 手机端回应配对请求，发送`授权响应数据包`
3. 手机端主动关闭连接

### 配对请求数据包

```
AUTH$KEY
```

#### 说明

**注意：**数据包以`CRLF`结尾。

`$KEY`为指定的配对密钥，由手机端随机生成，存储在电脑端中。

#### 示例

```
TCP 192.168.1.2--->>>192.168.1.3
AUTH
```

### 配对响应数据包

```
AUTHOK$TOKEN
```

或

```
AUTHFAIL
```

#### 说明

**注意：**数据包以`CRLF`结尾。

`$TOKEN`为从服务器获得的token(参考服务器文档)。

当授权成功时反馈第一种数据包，失败时反馈第二种数据包。

#### 示例

```
TCP 192.168.1.3--->>>192.168.1.2
AUTHOKaj5b1s02eokusotu0ej0l9c5m1
```

#### 其他

本数据包指定的超时时限为`5s`