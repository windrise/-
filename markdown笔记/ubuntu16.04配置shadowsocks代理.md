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



Ubuntu自带的PDF阅读器不太好用，做笔记也不方便，推荐使用Okular这款PDF阅读软件

打开Ubuntu软件中心，搜索“okular”，点击“安装”即可

然后修改打开PDF文件的默认应用程序为“okular”：

右键任一个PDF文件——“属性”——“打开方式”——选择“okular”——“设为默认值”  即可

小巧的Kazam也是蛮好用的

在命令行键入 sudo apt-get install kazam等待安装完成即可用

