七牛API服务的命名行测试工具，参考文档 七牛开发者中心 [命令行工具(qshell)
](https://developer.qiniu.com/kodo/tools/1302/qshell#4)。

示例中 bucket 为 test-pub

## 目录

<!-- MarkdownTOC -->

- qshell config
- stat
- fput/rput/qdownload/prefop
    - fput
    - rput
    - qdownload
    - prefop
- chgm/copy/move/delete/
    - chgm
    - copy
    - move
    - delete
- fetch/sync/prefetch/cdnrefresh/
    - fetch
    - sync
    - prefetch
    - cdnrefresh
    - cdnprefetch
- qupload
- buckets/listbucket/domains/ip/unzip/qetag
    - buckets
    - listbucket
    - domains
    - ip
    - unzip
    - qetag
- b64encode/b64decode/urlencode/urldecode
    - b64encode
    - b64decode
    - urlencode
    - urldecode
- ts2d/tms2d/d2ts
    - ts2d
    - tms2d
    - d2ts\(useless\)

<!-- /MarkdownTOC -->


## qshell config

Mac 版操作步骤如下

1. 下载 [qshell](http://devtools.qiniu.com/qshell-v2.1.8.zip)
2. 移动qshell到`/usr/local/bin/qshell`
3. 配置AK、SK：qshell acount ak sk

## stat

查看文件状态

qshell -d stat test-pub test/test-fput.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/78416146.jpg)

## fput/rput/qdownload/prefop

### fput

以文件表单的方式上传一个文件  

qshell fput test-pub test-fput.mp4 /Users/jingliu/Desktop/test-fput.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/15642456.jpg)

前缀，路径，上传入口 覆盖 低频

qshell fput test-pub test/test-fput.ppt /Users/jingliu/Desktop/test-fput.mp4 http://upload.qiniu.com true 1

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/86278012.jpg)

### rput

以分片上传的方式上传一个文件，前缀，路径，上传入口 覆盖 低频

qshell rput test-pub test/qiniu-introduce-4M.pdf /Users/jingliu/Desktop/qshell-test/fput/test-fput.mp4 http://upload.qiniu.com true 1

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/94256562.jpg)

### qdownload

从七牛空间同步数据到本地，支持只同步某些前缀的文件，支持增量同步    

### prefop

查询七牛数据处理的结果，通过处理的结果id

## chgm/copy/move/delete/

### chgm

### copy

### move

### delete

删除七牛空间中的一个文件    



## fetch/sync/prefetch/cdnrefresh/

### fetch

批量刷新cdn的访问外链

### sync

### prefetch

### cdnrefresh

### cdnprefetch

批量预取cdn的访问外链


## qupload

qupload是用来将本地目录中的文件同步到七牛空间中的命令，可以同步父子目录下的所有文件到七牛的对象存储空间中。

1. [参考文档](https://github.com/qiniu/qshell/blob/master/docs/qupload.md) 

2. 示例

输入命令

qshell qupload  1 /Users/jingliu/Desktop/config.json

配置文件

```
{
  "src_dir" : "/Users/jingliu/Desktop/test-dir",
  "bucket" : "test-pub"
}
```

示例图片

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/26274624.jpg)

3. 结果展示

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/28071824.jpg)

## buckets/listbucket/domains/ip/unzip/qetag

### buckets

获取当前账号下所有的空间名称  

qshell buckets

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/6215037.jpg)

### listbucket

获取test-pub的文件列表

qshell listbucket test-pub test-pub-listbucket.txt

获取/mp4开头的文件列表

qshell listbucket test-pub '/mp4' test-pub-mp4-listbucket.txt

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/18191475.jpg)

### domains

获取指定空间的所有关联域名   

qshell domains test-pub

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/1227515.jpg)

### ip

根据淘宝的公开API查询ip地址的地理位置   

qshell ip 112.74.185.158

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/66944200.jpg)

### unzip

解压zip文件，支持UTF-8编码和GBK编码 

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/63011895.jpg)


### qetag

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/32634388.jpg)



## b64encode/b64decode/urlencode/urldecode

### b64encode

base64编码工具，可选是否使用UrlSafe方式，默认UrlSafe

qshell b64encode 'hello world'

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/92149660.jpg)

### b64decode

base64解码工具，可选是否使用UrlSafe方式，默认UrlSafe    

qshell b64decode aGVsbG8gd29ybGQ=

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/26464891.jpg)

### urlencode

url编码工具 

qshell urlencode url带中文

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/75297090.jpg)

### urldecode

url解码工具 

qshell urldecode url%E5%B8%A6%E4%B8%AD%E6%96%87

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/18451328.jpg)

## ts2d/tms2d/d2ts

### ts2d

qshell ts2d 1427252311

将timestamp(单位秒)转为UTC+8:00中国日期，主要用来检查上传策略的deadline参数 

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/23191037.jpg)

### tms2d

将timestamp(单位毫秒)转为UTC+8:00中国日期  

qshell tms2d 1427252311000

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/98203473.jpg)

### d2ts(useless)

该命令用来生成一个Unix时间戳（单位秒），值是当前时间加上指定的秒数的和。
如果可以设置指定时间就好了。

qshell d2ts 3600
qshell d2ts -3600

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/93798932.jpg)# qshell-test
# qshell-test
