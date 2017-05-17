title: 【原创】如何使用hexo的NexT主题
date: 2017-05-15 13:57:41
tags:
- hexo
- next
- how
- 第三方插件
categories: 随笔
description: 之前使用的hexo的jacman,但是发现还是没hexo的nexT的简约，而且nexT本身就自配置了各种第三方插件，你需要开启和设置对应一些你的参数即可。所以果断选他。这篇博客主要是简单带过并且补充一些我走过坑和一些注意事项。欢迎搭建评论和谈论交流。

---
## 概念
[NexT](http://theme-next.iissnan.com): 是hexo的一个主题，你可以换各种hexo主题，而保持原有内容不变。

[Hexo](https://hexo.io/zh-cn/): 是高效的静态站点生成框架，基于 Node.js。 通过 Hexo 你可以轻松地使用 Markdown 编写文章，除了 Markdown 本身的语法之外，还可以使用 Hexo 提供的 标签插件 来快速的插入特定形式的内容。

　　特点：超快速度(渲染速度)，支持markdown,一键部署，丰富的插件
   
[npm](https://www.npmjs.com/): 是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题

1. 允许用户从NPM服务器下载别人编写的第三方包到本地使用。  
2. 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。 
3. 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。


<font style="background-color:#2780e3;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">站点配置文件</font>:一份位于站点根目录下，主要包含 Hexo 本身的配置。位置：your-hexo-site/_config.yml


<font style="background-color:#9954bb;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">主题配置文件</font>:位于主题目录下，这份配置由主题作者提供，主要用于配置主题相关的选项。位置: your-hexo-site/themes/主题名/\_config.yml。例如next的就是your-hexo-site/themes/next/_config.yml


---
## Hexo安装指南
###条件
　　先安装好Git和Node.js
　　（详细的安装过程见[官方教程](https://hexo.io/zh-cn/docs/)）

### Hexo的安装
#### 1.安装Hexo
　　所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。



```
＄npm install -g hexo-cli
```
#### 2.初始化Hexo
　　先转到自己自定的文件，作为Hexo的根目录（这时候可以省略<folder>的参数）

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```





---
### Hexo主题安装

　　Hexo 安装主题的方式非常简单，只需要将主题文件拷贝至站点目录的 themes 目录下， 然后修改下配置文件即可。

### Hexo目录简介
详细看图片：

![image](/images/pages/hexo_desciption.png)


## NexT主题安装指南
### 条件
　　先安装好Git和hexo
　　（详细的安装过程可参考[官方教程](http://theme-next.iissnan.com/getting-started.html)）（本人的是mac os x，直接brew install指令即可）
### 主题安装步骤
#### 1.下载主题
【方式一:Git的方式】
　在终端窗口下，定位到 Hexo 站点目录下。使用 Git checkout 代码：　　
　
（推荐此方式，之后的更新可以通过 git pull 来快速更新， 而不用再次下载压缩包替换。）

```
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
【方式二:下载稳定版本】

1. 前往 NexT 版本 [发布页面](https://github.com/iissnan/hexo-theme-next/releases)。

2. 选择你所需要的版本，下载 Download 区域下的 Source Code (zip) 到本地。例如，下载 v5.1.1 版本

3. 解压所下载的压缩包至站点的 themes 目录下， 并将 解压后的文件夹名称（hexo-theme-next-5.1.1）更改为 next


#### 2.站点配置主题
打开<font style="background-color:#2780e3;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">站点配置文件</font>找到 theme 字段，并将其值更改为 next。

```
    theme: next
```
到此，NexT 主题安装完成。下一步我们将验证主题是否正确启用。在切换主题之后、验证之前， 我们最好使用 hexo clean 来清除 Hexo 的缓存。

**注意事项**：yml每项配置冒号:后面需要加空格的


#### 3.验证主题
在hexo站点目录下，启动本地站点

```
    hexo server
```
可简写"**hexo s**", 可以开启debug模式 "**hexo server -debug**".

此时即可使用浏览器访问 http://localhost:4000，检查站点是否正确运行。


### 使用
（可参考[官方教程](https://hexo.io/zh-cn/docs/commands.html）
#### 1.新建一篇文章 
```
    hexo new [layout] <title>

```
　　新建一篇文章。如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

#### 2.发表草稿
```
    hexo publish [layout] <filename>     #发表草稿
    hexo --draft                         #显示草稿的文章
```
#### 3.生成静态文件
　　把markdown、主题等生成静态文件

```
    hexo generate
```
可简写 "**hexo g**"， 通过""**hexo deploy -g**"也是生成静态文件。
   "**hexo generate -d**" 生成后立即部署。
   

#### 4.启动服务器
```
    hexo server
```
　　启动服务器。可简写 ""**hexo s**"，默认情况下，访问网址为： http://localhost:4000/。
   选项**-p, --port**--重设端口，
   **-s, --static**--只使用静态文件
，**-l, --log**启动日记记录，使用覆盖记录格式


#### 5.部署网站

```
    hexo deploy
```
　　部署网站到github上。选项**-g, --generate**部署之前预先生成静态文件

#### 6.清除缓存文件 (db.json) 和已生成的静态文件 (public)。
```
    hexo clean
```
清除缓存文件 (db.json) 和已生成的静态文件 (public)。
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。
#### 7.列出网站资料
```
    hexo list <type>

```



## NexT主题定制化以及第三方配置指南
### 我的主题定制的情况：
　　修改<font style="background-color:#9954bb;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">主题配置文件</font>的。本身NexT主题里面有配置很多的第三方插件配置，所以只需要打开和对应配置你的一些App_ID即可。
#### 1.修改主题scheme
    scheme: Pisce
#### 2.设置代码高亮
    highlight_theme: night bright
#### 3.修改侧边栏链接
链接放置在 social 字段下，一行一个链接。其键值格式是 显示文本: 链接地址

```
social:
  #LinkLabel: Link
  GitHub: https://github.com/jamfliu
  微博: http://weibo.com/jamfliu
  豆瓣: http://douban.com/people/jamfliu
  知乎: http://www.zhihu.com/people/jamfliu
```

#### 4.设置头像和site的favicon
  修改字段 avatar， 值设置成头像的链接地址。其中，头像的链接地址可以是：
  
```
avatar: images/lzf.png
```
下面是设置favicon。

```
favicon: images/lzffavicon.ico
```


### 我的第三方插件定制的情况：
#### 1.统计阅读量
　　原本我是申请了leancloud的appId和appKey，后面发现不蒜子统计中也包含了阅读量，所以我就配置但没用。
 
 **方式一**：使用leancloud
  首先申请它的AppID以及AppKey，在next的主题配置文件中找到leancloud，然后配置，主要是配置**enable: true**,然后填入你的AppID以及AppKey
  
 **方式二**：使用不蒜子统计中的page_pv项
    直接使用**enable: true**即可
    
 
#### 2.增加评论功能
 之前使用的多说已经要停了，所以改用了DISQUS，但是发现在国内的网络加载它的js老超时，果断换了一个，本想还网易云跟帖的，但是注册老有问题，而且支持的社交少。选了韩国的来必力，还算挺好用的，注册都不麻烦，就是获取验证码的时候是韩文有点恶心，不是全程中文的。
    
   申请[来必力](https://livere.com/)的你自己的安装代码，注册完取data-uid里面的代码。然后设置livere_uid

```
 livere_uid: MTAyMC8y11222Y3NS800000
```
#### 3.统计自己网站的流量情况
**  1) 不蒜子统计 **
  
这个不需要去注册，打开即可可以统计本站点的总的pv和uv量，也可以统计单个页面的pv量。

编辑<font style="background-color:#9954bb;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">主题配置文件</font>中的busuanzi_count的配置项。
 当"**enable: true**"时，代表开启全局开关。若site_uv、site_pv、page_pv的值均为false时，不蒜子仅作记录而不会在页面上显示。

**  2) 百度统计 **
  
为了后续方便分析，增加了百度统计，使用了百度统计，并不会给网站速度带慢的情况。
   
申请你的自己的错误码，然后设置"**baidu_analytics**"为你自己的脚本ID即可
 
 
#### 4.增加搜索功能,即站内搜索
 NexT主题支持集成 Swiftype、 微搜索、Local Search 和 Algolia,Swiftype和Algolia都只有一段时间的试用期，可以采用Hexo提供的Local Search,原理是通过hexo-generator-search插件在本地生成一个search.xml文件，搜索的时候从这个文件中根据关键字检索出相应的链接。
 
** 1） 安装 hexo-generator-searchdb，在站点的根目录下执行以下命令**

```
npm install hexo-generator-searchdb --save
npm install hexo-generator-search --save
```
现在官方文档漏了下面一条语句，会导致生成不了search.xml


** 2） 在<font style="background-color:#2780e3;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">站点配置文件</font>末尾中新增下面的配置项**
    
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
** 3） 在<font style="background-color:#9954bb;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">主题配置文件</font>启动本地搜索**
    
```
local_search:
  enable: true
```

【过程中遇到的问题】：查不了，发现是无生成search.xml
 也没有报错，似乎是node的版本不支持，我通过 npm upgrade和更新brew upgrade node[我的是mac os]来解决
 
 
 
 
#### 5.内容分享功能
　　百度分析在https好像有点问题，使用了JiaThis，但是好像也不稳定，暂时先开着。

　　编辑 <font style="background-color:#9954bb;display: inline;padding: .2em .6em .3em;font-size: 85%;font-weight: 700;line-height: 1;color: #fff;
    text-align: center; white-space: nowrap;vertical-align: baseline;border-radius: .25em;">主题配置文件</font>， 添加/修改字段 jiathis，值为 true。

#### 6.字数统计功能

** 1） 安装hexo-wordcount，在站点的根目录下执行以下命令**

```
npm install hexo-wordcount --save
```
 **2）修改配置文件**
 
 为了方便地开启和关闭字数统计功能，我们需要在配置文件（站点配置文件或主题配置文件均可）中添加一个键值对：
 
```
# 开启字数统计
word_count: true
```


 **3）修改主题的swig布局，themes/next/layout/_macro/post.swig**

  (看了这个swig，似乎默认支持的，虽然字段和结构不一样，但是我怎么配都不成功，所以新增了)
 
```
{% if theme.word_count %}
  <span class="post-letters-count">
    &nbsp; | &nbsp;
    <span>{{ wordcount(post.content) }} 字</span>
  </span>
{% endif %}
```

 



### 出现过的问题汇总：
出现解决较久的问题有：

#### **1.启动的时候发起请求的时候报错ENOENT, no such file or directory **

```
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
Unhandled rejection Error: ENOENT, no such file or directory '/Users/liuzhenfeng/git/blog_hexo/themes/next/layout/_scripts/schemes/.swig'
    at Error (native)
    at Object.fs.openSync (fs.js:500:18)
    at Object.fs.readFileSync (fs.js:352:15)
    at Object.ret.load (/Users/liuzhenfeng/git/blog_hexo/node_modules/hexo/node_modules/swig/lib/loaders/filesystem.js:55:15)
    ....
    at process._tickCallback (node.js:355:11)
        
```
##### **==>原因：**
  配置项的冒号后面无空格，比如错误的配置：（后面少了一个空格）
  
```
AppID:XXX
```
正确的配置是冒号后面加空格，如下：

```
AppID: XXX
```

#### 2.执行 "**npm install hexo-generator-searchdb --save**"时，报如下的错误

```
npm WARN engine hexo-generator-searchdb@1.0.7: wanted: {"node":">= 4.2.2"} (current: {"node":"0.12.7","npm":"2.11.3"})
hexo-generator-searchdb@1.0.7 node_modules/hexo-generator-searchdb
├── utils-merge@1.0.0
├── striptags@3.0.1
└── ejs@1.0.0
```
我通过 npm upgrade和更新brew upgrade node[我的是mac os]来解决，发现都是失败了，后来确定node是指nodejs就找了nodejs的更新方式：


```
#第一步：首先安装n模块：
npm install -g n
#第二步：升级node.js到最新稳定版
n stable
```
网上说这种解决办法有问题，所以要卸载干净之后重装

```
brew uninstall node  #卸载，但是重新安装是会提示卸载不干净，需要额外删除一些
#以下是额外删除，主要根据错误提示
rm -f /usr/local/lib/dtrace/node.d
rm -f /usr/local/share/systemtap/tapset/node.stp
rm /usr/local/share/man/man1/node.1
rm -rf /usr/local/lib/node_modules
```


#### 3.执行hexo操作时，报ERROR Script load failed(exturl.js)
情况：执行hexo操作时，报ERROR Script load failed: themes/next/scripts/tags/exturl.js
解决办法：重新安装hexo-util模块
```
 $ npm install -- save-dev hexo-util
```

#### 4.报错：ERROR Plugin load failed: hexo-git-backup
解决办法：重新安装hexo-git-backup模块
```
 $ npm install hexo-git-backup --save
```

#### 5.报错：ERROR Deployer not found: git

```
 $ npm install hexo-deployer-git --save
```
 

#### 6.报错：Template render error: (unknown path) 
```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 55, Column 232]
  unknown block tag: endif
    at Object.exports.prettifyError (/Users/liuzhenfeng/git/blog_hexo/node_modules/nunjucks/src/lib.js:34:15)
```
报这个错误的时候，比较容易确定是我心中md文件出问题了，但是具体是什么错误，一头雾水，严重影响到我的进度，m这个错误所指向的js我是没接触过的。最终我用了打印md文件前多少行，来确定第几行出错了。

##### **==>原因：**
在字数统计功能的说明修改swig文件的的代码不小心动了一个字符，把那个统计文章字数的那段代码的"{" --> ">"导致的报错 。改回去即可修复。

<br />


*PS:有任何关于的问题，欢迎来评论讨论交流。*

## 参考网站
1. [Hexo的官方文档](https://hexo.io/zh-cn/)
2. [NexT的官方文档](http://theme-next.iissnan.com)
3. [为Hexo NexT主题添加字数统计功能](https://eason-yang.com/2016/11/05/add-word-count-to-hexo-next/)

