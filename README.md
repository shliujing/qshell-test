## 实践目的

1. 熟悉存储API、熟悉qshell全部命令的使用
2. 方便快速解答客户提出的任何有关qshell的FAQ
3. 记录了输入命令和输出结果图，方便理解，也可以作为他人快速理解的材料
4. 为后期集成到内部测试的 web 系统做准备

七牛API服务的命名行测试工具，参考文档 七牛开发者中心 [命令行工具(qshell)
](https://developer.qiniu.com/kodo/tools/1302/qshell#4)

## 目录

<!-- MarkdownTOC -->

- account/stat 账号文件类
    - account
    - stat
- buckets/listbucket/domains/ip/unzip/qetag bucket等通用类
    - buckets
    - listbucket
    - domains
    - ip
    - unzip
    - qetag
- fput/rput/qdownload/prefop/qupload 上传下载类
    - fput
    - rput
    - qdownload
    - prefop
    - qupload
- chgm/copy/move/delete 文件操作类
    - chgm
    - copy
    - move
    - delete
- fetch/sync/prefetch/cdnrefresh 刷新预取类
    - fetch
    - sync
    - prefetch
    - cdnrefresh
    - cdnprefetch
- b64encode/b64decode/urlencode/urldecode 编码解码类
    - b64encode
    - b64decode
    - urlencode
    - urldecode
- ts2d/tms2d/d2ts 时间戳日期类
    - ts2d
    - tms2d
    - d2ts\(useless\)

<!-- /MarkdownTOC -->


## account/stat 账号文件类

### account

Mac 版操作步骤如下，其他系统参考 [命令行工具(qshell)
](https://developer.qiniu.com/kodo/tools/1302/qshell#4)

1. 下载 [qshell](http://devtools.qiniu.com/qshell-v2.1.8.zip)
2. 移动qshell到`/usr/local/bin/qshell`
3. 配置AK、SK：qshell acount ak sk。配置后在会生成`/Users/jingliu/.qshell/account.json`文件，保存ak、sk（加密）

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/46180546.jpg)

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/92455126.jpg)

### stat 

查看文件状态

qshell stat test-pub test/test-fput.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/78416146.jpg)

## buckets/listbucket/domains/ip/unzip/qetag bucket等通用类

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

qshell unzip 1.txt.zip

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/63011895.jpg)

### qetag

根据七牛的qetag算法来计算文件的hash

qshell qetag ~/Desktop/11111.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/32634388.jpg)

## fput/rput/qdownload/prefop/qupload 上传下载类

### fput

以文件表单的方式上传一个文件  

qshell fput test-pub test-fput.mp4 /Users/jingliu/Desktop/test-fput.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/15642456.jpg)

前缀，路径，上传入口 覆盖 低频

qshell fput test-pub test/test-fput.ppt /Users/jingliu/Desktop/test-fput.mp4 http://upload.qiniu.com true 1

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/86278012.jpg)

### rput

以分片上传的方式上传一个文件，前缀，路径，上传入口 覆盖 低频

qshell rput test-pub test/qiniu-introduce-4M.pdf /Users/jingliu/Desktop/

qshell-test/fput/test-fput.mp4 http://upload.qiniu.com true 1

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/94256562.jpg)

### qdownload

从七牛空间同步数据到本地，支持只同步某些前缀的文件，支持增量同步    

qshell qdownload 3 config.conf

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/72856531.jpg)

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/71844580.jpg)

### prefop

查询七牛数据处理的结果，通过处理的结果id

qshell prefop z0.5b0b8a8538b9f324a5ea1b3a

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/66318191.jpg)

### qupload

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

## chgm/copy/move/delete 文件操作类

修改七牛空间中的一个文件的MimeType，文件类型。

### chgm

qshell chgm test-pub 11.mp4 video/mov

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/35737345.jpg)

### copy

复制七牛空间中的一个文件，可以是同一个控件

qshell copy [-overwrite] <SrcBucket> <SrcKey> <DestBucket> [<DestKey>]

不同区域，报错400

qshell copy -overwrite test-pub 11.mp4 test-pub1 test-pub/mp4/11.mp4

同区域

qshell copy -overwrite test-pub 11.mp4 test-pub-hd test-pub/mp4/11.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/71880599.jpg)

### move

移动或重命名七牛空间中的一个文件    

qshell move -overwrite test-pub 11.mp4 test-pub 22.mp4

qshell move -overwrite test-pub 22.mp4 test-pub-hd test-pub/mp4/22-move.mp4

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/19518748.jpg)

### delete

删除七牛空间中的一个文件  

qshell delete test-pub-hd test-pub/mp4/22-move.mp4  

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/98029616.jpg)

## fetch/sync/prefetch/cdnrefresh 刷新预取类

### fetch

从Internet上抓取一个资源并存储到七牛空间中。适合于中小文件的抓取，根据实际经验，基本上适合50MB以下的文件抓取。

如果指定的Key都是一样的，那么会默认覆盖这个Key所对应的文件。

不指定名称则保存hash值。

功能同接口 [第三方资源抓取](https://developer.qiniu.com/kodo/api/1263/fetch )

qshell fetch https://www.baidu.com/img/bdlogo.png test-pub bpng/dlog.png

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/31441600.jpg)

### sync

从Internet上抓取一个资源并存储到七牛空间中，适合大文件的场合，比如1G,100G。

sync指令的基本原理是使用Range方式按照4MB一个块从资源服务器获取数据，然后使用七牛支持的分片上传功能直接传到七牛存储空间中。并不用担心网络中断导致的同步中断，因为采用了分片上传的机制，我们会把每一个成功上传的块的位置记录下来，当下次网络恢复的时候，只需要运行原始命令即可从断点处恢复。

qshell sync <SrcResUrl> <Bucket> <Key> [<UpHostIp>]

```
UpHostIp #获取，指定ip可减少DNS环节，提升同步速度

华东机房
$ dig up.qiniu.com

华北机房
$ dig up-z1.qiniu.com

华南机房
$ dig up-z2.qiniu.com

北美机房
$ dig up-na0.qiniu.com
```

qshell sync https://www.baidu.com/img/bdlogo.png test-pub bpng/dlog2.png 115.238.101.35

如下图，可见sync不支持覆盖，必须加上https协议（fetch可忽略）

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/81060811.jpg)

### prefetch

更新七牛空间中从源站镜像过来的文件，配置了镜像存储的空间，在一个文件首次回源源站拉取资源后，就不再回源了。如果源站更新了一个文件，那么这个文件不会自动被同步更新到七牛空间。

同接口文档：[镜像资源更新 (prefetch)](http://developer.qiniu.com/docs/v6/api/reference/rs/prefetch.html)

qshell prefetch test-pub demo/iconfont/miga/iconfont.css

qshell prefetch test-pub demo/iconfont/miga/demo.css

下图分别是更新和拉新，效果是一样的

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/97111282.jpg)

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/67864574.jpg)

### cdnrefresh

批量刷新cdn的访问外链，可刷新文件 或 目录。刷新是把cdn节点上的缓存刷新到cdn节点。

注意需要刷新的目录，必须以/结尾。

qshell cdnrefresh torefresh.txt

cat torefresh.txt

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/36985032.jpg)

### cdnprefetch

批量预取cdn的访问外链。可刷新文件 或 目录。预取是把cdn节点上的数据，从源站拉取到cdn节点。

qshell cdnprefetch torefresh.txt

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-28/91496696.jpg)

## b64encode/b64decode/urlencode/urldecode 编码解码类

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

## ts2d/tms2d/d2ts 时间戳日期类

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

![](http://img-lj.oss-cn-hangzhou.aliyuncs.com/18-5-25/93798932.jpg)