##python3中的修改内容
首先，需要安装configparser，否则代码无法使用。读取配置文件的在python3中有ConfigParser改成了configparser,需要安装。

此版本的修改，将上传到七牛上面是文件的key进行了修改，对原文件名进行md5之后，对md5之后的文件名进行截取和拼装组成了存到七牛的key，组成之后是类似image/0/25/13e20badc41e1f72176ce31aaf4a0.jpg这种文件名。

> 另外需要注意的是，在启动qiniu4blog之前，监视的文件夹中已经存在的文件，是不会上传到七牛的。所以使用FastStone Capture的自动保存截图之前需要先启动监控服务。若有已经存在的文件（不是通过FastStone Capture自动保存的截图）需要上传，建议先拷贝出去后在启动qiniu4blog之后，再拷贝到监控目录。

#打造自己的图床(qiniu)

![](http://voyager91.qiniudn.com/2.gif)

*修复中文文件名*
![](http://7qnct6.com1.z0.glb.clouddn.com/Screenshot%202015-04-21%2022.39.38.jpg)

*增加自定义url  在`custom_url`里设置*
![](http://voyager91.qiniudn.com/2015-04-22_%E4%B8%AD%E6%96%8700008.jpg)

#UPDATE

##2015-04-21:

* 支持中文
* 支持自定义 URL

###流程

> python 监控文件夹 --> 文件新增(FS capture 截图自动保存该目录)
--> 使用 qiniu sdk 上传到 qiniu 云存储 --> 生成外链到粘贴板 --> 复制图片外链到博客



##安装步骤
pip install qiniu4blog

> windows ,Mac os 下 python2.7.9 下验证通过,其它版本还未测试


##配置

登录[https://portal.qiniu.com/](https://portal.qiniu.com/)
新建一个**bucket**,获取以下相关信息`bucket` , `accessKey` ,`secretKey`, 

![](http://voyager91.qiniudn.com/2015-04-16_00001.jpg)


在home目录下新建配置文件`qiniu.cfg` 例如`C:\Users\leeyoung\qiniu.cfg`
`path_to_watch` 为截图自动保存的目录
`qiniu.cfg`内容如下
```
[config]
bucket = your-bucket-name
accessKey = qzA***********************sa
secretKey = P5G***********************wq
path_to_watch = D:\install\qiniu\uploadimage2qiniu

[custom_url]
enable = false 或者 true
addr = http://7qnct6.com1.z0.glb.clouddn.com/

```

> mac 系统设置截图自动保存文件夹

```
defaults write com.apple.screencapture location /Users/leeyoung/Desktop/up2qiniu
killall SystemUIServer
```

##运行
 
打开终端或cmd
```
qiniu4blog
```

##相关下载
* [FastStone Capture.rar](http://pan.baidu.com/s/1o6mjrmi)

> 设置自动保存路径 settings -> Auto Save -> Output folder
