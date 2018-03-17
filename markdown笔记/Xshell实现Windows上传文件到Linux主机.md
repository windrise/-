# Xshell实现Windows上传文件到Linux主机

总结：xshell有一个优点就是能够直接把window的文件拉进linux,感觉比secureCRT用起来更方便简单接下来看我转载的！！！

Xshell很好用,然后有时候想在windows和linux上传或下载某个文件,其实有个很简单的方法就是rz,sz。
首先你的Linux上需要安装安装lrzsz工具包，(如果没有安装请执行以下命令,安装完的请跳过)

yum  install lrzsz
安装完毕即可使用。

rz，sz是便是Linux/Unix同Windows进行ZModem文件传输的命令行工具，所以要在Xshell连接属性中的设置上传协议为Zmodem和接受的文件路径等。







windows端需要支持ZModem的telnet/ssh客户端(xshell支持,好像putty不支持)，SecureCRT就可以用SecureCRT登陆到Unix/Linux主机（telnet或ssh均可）。

运行命令rz，即是接收文件（上传到Linux上），xshell就会弹出文件选择对话框，选好文件之后关闭对话框，文件就会上传到linux里的当前目录。也可以直接把要上传的文件拖到xshell上完成上传。



运行命令sz file 就是发文件到windows上（保存的目录是可以配置） 比ftp命令方便多了，而且服务器不用再开FTP服务了。