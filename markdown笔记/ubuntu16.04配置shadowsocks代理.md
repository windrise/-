## ubuntu16.04配置shadowsocks代理

> apt-get  install python-pip
>
> pip install shadowsocks  

然后配置好json文件

然后启动

> sslocal -c /etc/shadowsocks.json
>
> (sslocal -c /etc/shadowsocks.json -d start (后台启动)  -d stop 停止)

然后浏览器设置 部分代理  automatic proxy configuration URL:

```
https://raw.githubusercontent.com/breakwa11/gfw_whitelist/master/proxy.pac 
```

**如果不可以访问Google**

> apt-get install proxychains
>
> vim /etc/proxychains.conf（查看最后一行 是不是 socks5 127.0.0.1 1080）
>
> proxychains curl cip.cc(下面有ip归属地，说明ss正常)
>
> proxychains firefox(启动浏览器)

**设置开机自启动**

> 编辑/etc/rc.local文件 在exit之前加入sslocal -c /etc/ss.json -d start