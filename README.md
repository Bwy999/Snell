# Snell
**用带sftp的ssh工具直接将下面的这一段复制到docker-compose.yml里去**
```
version: "3.8" 
services:
  snell:
    image: accors/snell:latest
    container_name: snell
    restart: always
    network_mode: host
    volumes:
      - ./snell-conf/snell.conf:/etc/snell-server.conf
    environment:
      - SNELL_URL=https://dl.nssurge.com/snell/snell-server-v4.0.1-linux-amd64.zip
  shadow-tls:
    image: ghcr.io/ihciah/shadow-tls:latest
    container_name: shadow-tls
    restart: always
    network_mode: "host"
    environment:
      - MODE=server
      - FASTOPEN=1
      - V3=1
      - LISTEN=0.0.0.0:8443   # ipv6的话改成[::]:8443 ，8443不用改动
      - SERVER=127.0.0.1:2100  # ipv6的话改成[::1]:xxx ，xxx是你snell节点的端口
      - TLS=mp.weixin.qq.com:443 #这里可以自己选，下面放了作者推荐的链接
      - PASSWORD=Gm8UXm6aridZ  # 这里是密码，随便改
```

