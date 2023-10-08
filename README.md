# Test SSL

### 证书创建（Ubuntu）



证书权限必须与程序权限一致，要么证书降权要么程序提权。否则认证失败\无法签名

可以单独将misc文件夹直接cp 到工作目录,然后创建自签名根证书

```bash
./CA.pl -newca
```

服务器证书与客户端证书common name必须不同，organizationName必须一致。

服务器证书与客户端证书RSA长度不能太小低于1024，最好是2048

**创建请求**

```bash
openssl req -newkey rsa:2048 -out req1.pem -keyout sslclientkey.pem
openssl req -newkey rsa:2048 -out req2.pem -keyout sslserverkey.pem
```

**生成证书**

```bash
openssl ca -in req1.pem -out sslclientcert.pem 
openssl ca -in req2.pem -out sslservercert.pem
```

如果OpenSSL拒绝生成证书，可能是因为请求中的名称与CA的名称不匹配。匹配规则在配置文件中指定（查看[策略匹配]部分）。可以更改请求的名称以符合策略，也可以更改策略。配置文件还包含另一个策略（称为任意策略），该策略的限制较少。可以通过更改以下行来选择该策略：

```bash
“policy = policy_match” change to “policy = policy_anything”.
```

