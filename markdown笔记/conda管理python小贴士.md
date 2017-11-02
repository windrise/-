# virtualenv/conda管理python小贴士

> 指定python版本：
>
> virtualenv  -p  /usr/bin/python版本  targetDirectory   
>
> 或者： conda  create -n  tensorflow python=3.5 numpy scipy



> conda 显示所有环境
>
> conda info -e  或者 conda env list



> conda 显示环境安装的包
>
> conda  list -n env_name
>
> 复制虚拟环境
>
> conda create --name new_env_name --clone old_env_name 
>
> 分享虚拟环境：
>
> 首先通过`activate target_env`要分享的环境`target_env`，然后输入下面的命令会在当前工作目录下生成一个`environment.yml`文件
>
> conda env export \> environment.yml
>
> 对方拿到environment.yml文件后，将改文件放在工作目录下，可以通过一下命令创建
>
> conda env create -f environment.yml