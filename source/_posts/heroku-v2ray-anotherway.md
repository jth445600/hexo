# heroku搭建v2ray教程
所需账号:
1.一个heroku的账号
2.一个cloudflare的账号（非必须）
## 教程开始
介绍：
注册heroku账号：[点击进入](https://signup.heroku.com/)

申请vps地址：[点击进入](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Fbclswl0827%2Fv2ray-heroku)

github项目地址：[点击进入](https://github.com/xueliqq/v2ray-heroku/blob/master/README.md)

开始：

如图所示：输入一个可用的用户名，点击deploy app进入下一步
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909180314.png)

接下来就是耐心等待约1-2分钟，部署v2ray安装程序
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909180618.png)

进入之后点击设置按钮，
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909180716.png)

点击Reveal config vars查看自己的v2ray的uuid
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909180752.png)

点击右上角OPEN app找到我们的ip地址，也就是分配给我们的域名：

![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909181032.png)
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909181222.png)

搭建完成，接下来就把我们的这些信息导入我们的v2ray客户端
![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909181440.png)

按照以上格式填写就可以正常使用！

## cloudflare加速（需cloudflare账号）
对速度有要求的人群可以看一下；主要是使用Cloudflare Workers加速，免费套餐有调用限制，大家悠着点用就行了

1.在Cloudflare Workers中创建一个Workers
![avatar](https://i.loli.net/2020/07/26/a3hNf65UD2rsGYT.png)
![avatar](https://i.loli.net/2020/07/26/ZsGLCQNhjYlzgap.png)

2.将原有的示例代码全部删除，复制如下代码，并将第四行的汉字替换为你的V2Ray的地址

```addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="应用名称.herokuapp.com";
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```

点击右侧的发送按钮，看最后一行是否出现了Bad Request，出现则代表成功

![avatar](https://i.loli.net/2020/07/26/Qsd43hIbvXUFYLi.png)


成功后，点击保存并部署，并记下你的Workers二级域名

其实到第四步已经可以了，把V2Ray中原来的域名改为现在的Workers域名就行了，但是毕竟会有人追求极致完美嘛

对速度有更高追求以及不怕折腾的人可以接着往下看
### 对Cloudflare节点的筛选

[点击下载IP自选程序，解压，在Windows系统下运行](https://www.goyywp.xyz/uploads/kexueshangwang/better-cloudflare-ip-win32.zip)

自动筛选ip最准确的方法是关闭代理，网线直连去测试，否则容易不准确！

```也可以手动筛选cloudflare支持各宽带的ip段，*号代表1-255之间任意数字

CloudFlare 百度云合作 ip：
 
162.159.208.4-162.159.208.103
 
162.159.209.4-162.159.209.103
 
162.159.210.4-162.159.210.103
 
162.159.211.4-162.159.211.103
 
各线路推荐列表：

电信：推荐走圣何塞，例：104.16.160.* 或者上面的百度云合作 ip。

移动：推荐走移动香港，例：172.64.32.*、141.101.115.* 或者 104.23.240.0-104.23.243.254。

联通：没发布什么好线路，可走圣何塞。例：104.16.160.* 或者 104.23.240.0-104.23.243.254。

也可以试一下走亚特兰大 108.162.236.*(日前不可用)

```


最后，配置V2Ray：
![avatar](https://i.loli.net/2020/07/26/cbnmyoiXAwDMVrE.png)


### 注意事项
由于各地的网络情况每天都不同，所以每天（甚至是每半天）的最优节点都不尽相同；但对于一个应急用的已经足够了

## 教程完毕！

下面放几张速度图

![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200909181850.png)

![avatar](https://i.loli.net/2020/07/26/is243ERcjyqGuhX.png)

![avatar](https://wxf2088.xyz/wp-content/uploads/2020/09/QQ%E6%88%AA%E5%9B%BE20200910092121.png)

# 图片来源
此教程的图片来自于[王晓峰部落阁](https://wxf2088.xyz/577.html)以及[道之遠兮](https://www.skxlz.top/2020/07/26/25/)