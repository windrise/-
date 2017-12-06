### python数据集处理

采集

> import urllib
>
> target_url = "http://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-red.csv"
> data = urllib.request.urlopen(target_url).read().decode('utf-8')
>
> 

