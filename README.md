# Reality + Xhttp

手动操作，加深理解。

私有化之后，以后都可以一键使用。

仅供参考！

## 构建

```
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
vless://36f68b25-5d7d-46fb-a8c3-392581a3f6c9@ip:40010?encryption=none&security=reality&sni=www.apple.com&fp=chrome&pbk=RgtyXjg_wMpoX4W9COE9KOuxiVFEjFUF6cD6X32wrkA&sid=b1e0&spx=%2F&type=xhttp&path=%2F0d313615&mode=auto#xhttp-c-clone
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

效果实现了，但没有系统的学习过，缺乏确定性。
