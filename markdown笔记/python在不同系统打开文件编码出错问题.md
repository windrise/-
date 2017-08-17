## python在不同系统打开文件编码出错问题

```
import codecs
txtpath=r"userdict.txt"
fp = codecs.open(txtpath,'rb','utf-8')
for line in fp.readlines():
	line
fp.close
```