# Reality + Xhttp

可以在 codespaces https://github.com/codespaces 中进行编译测试。

然后登陆 docker push 上传到仓库

手动操作，加深理解。

构建完成后，填上 IP 就可以使用。

这个仓库，仅仅是个例子。不提供镜像。

需要自己构建。

仅供参考！

## 构建

```
git clone https://github.com/comeyna/reality-xhttp
docker build -t xray:xhttp .
```

## docker-compose 

```
services:
  xray_xhttp:
    image: xray:xhttp
    container_name: xray_xhttp
    restart: always
    ports:
      - "40010:443"
    logging:
      options:
        max-size: "10m"
        max-file: "3"
```

## 配置信息

```bash
vless://0d313615-60c3-4978-9748-92ff453018a6@ip:40010?encryption=none&security=reality&sni=www.apple.com&fp=chrome&pbk=RgtyXjg_wMpoX4W9COE9KOuxiVFEjFUF6cD6X32wrkA&sid=b1e0&spx=%2F&type=xhttp&path=%2F0d313615&mode=auto#xhttp-c-clone
```

## 修改配置

 生成 UUID 钥匙 私钥 修改掉 config.json 的值 

 修改后需要重启容器

```bash
docker exec -it xray_xhttp sh

UUID="$(/xray uuid)" && echo "UUID: $UUID"

/xray x25519 >/key && PRIVATEKEY=$(cat /key | grep "Private" | awk -F ': ' '{print $2}') && PUBLICKEY=$(cat /key | grep "Public" | awk -F ': ' '{print $2}') && echo "Private key: $PRIVATEKEY" && echo "Public key: $PUBLICKEY"
```

## 总结

原来都有，参照写就行！

https://github.com/lxhao61/integrated-examples/tree/main
