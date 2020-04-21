# Windows+Hugo+GithubPage搭建简单个人博客




## 安装 hugo

1. 二进制安装(推荐：简单、快速)，到 [hugo Releases](https://github.com/gohugoio/hugo/releases) 下载对应的操作系统版本的 `hugo` 二进制文件（ `hugo` 或者 `hugo.exe` ）；
2. 创建文件夹。此处举例： `F` 盘创建 **`hugo/bin`** ，将解压后的 **`hugo.exe`** 放到 **`bin`** 目录下；
3. 配置系统环境变量。将 **`F:\hugo\bin`** 加到 **path** 变量中

以上设置好后，就可以在 `cmd` 中查看是否安装成功。执行命令：

```bash
$ hugo version
Hugo Static Site Generator v0.69.0-4205844B windows/amd64 BuildDate: 2020-04-10T09:11:37Z
```

## 生产站点

进入 `F:\hugo` 下，打开命令窗口。(可用 `cmd` ，也可选择下载安装 [Git](https://git-scm.com/downloads) ，推荐安装 `git` ，敲命令很方便)

```bash
$ hugo new site 文件名称 (如blog)
```

执行后，在 **hugo目录** 下就会生成一个 名叫 `blog` 的站点文件夹

进入 `blog` ，显示以下目录结构：

> archetypes　  (存放`default.md`，头文件格式，每次新建文章默认显示的头部信息在此修改)
>
> content 　　  (存放博客文章，`markdown`格式文件)
>
> data         (存放自定义或者导入的模板)
>
> layouts      (存放网站的数据模板)
>
> static       (存放图片、`css`、`js`等静态资源)
>
> themes       (存放主题文件，每个主题都是一个独立的文件夹)
>
> config.toml  (网站配置文件)

创建第一篇文章，放到 `post` 目录，方便之后生成聚合页面。

```bash
$ hugo new post/first.md
```

打开编辑 `post/first.md` ：

```toml
+++
date: "2015-10-25T08:36:54-07:00"
title: "first"
 
+++

### Hello Hugo

 1. aaa
 1. bbb
 1. ccc
```

## 安装皮肤

到 [皮肤列表](https://www.gohugo.org/theme/) 挑选一个心仪的皮肤，比如你觉得 `Hyde` 皮肤不错，找到相关的 `GitHub` 地址，创建目录 `themes`，在 `themes` 目录里把皮肤 `git clone` 下来：

```bash
# 创建 themes 目录
$ cd themes
$ git clone https://github.com/spf13/hyde.git
```

此时可回到站点目录下打开 `config.toml` 配置指定主题。如 `theme = "hyde"` 没有 `theme` 参数就自己写上

```toml
baseURL = "https://shaopus.github.io/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "hyde"
```

## 运行hugo

在你的**站点根目录**执行 `hugo` 命令进行调试：

```bash
$ hugo server
```

浏览器里打开： http://localhost:1313

## 部署GithubPage

假设你需要部署在 `GitHub Pages` 上，首先在`GitHub`上创建一个`Repository`，命名为：`shaopus.github.io` （`shaopus`替换为你的`github`用户名）。

在站点目录**`config.toml`**中**`baseURL`**要换成自己建立的仓库，如 `baseURL =` "https://yourname.github.io/"

进入**站点根目录**下，执行：

```bash
$ hugo
```

执行后，站点根目录下会生成一个`public`文件夹，该文件下的内容即 `hugo` 生成的整个静态网站。每次更新内容后，将 `pubilc` 目录里所有文件 `push `到 `GitHub` 即可。

首次使用的时候要执行以下命令：

```bash
$ cd public

$ git remote add origin https://github.com/yourname/yourname.github.io.git (换成自己的)　　将本地目录链接到远程服务器的代码仓库

$ git add -A

$ git commit -m "first commit"

$ git push -u origin master
```

以后每次**站点目录**下执行 `hugo` 命令后，再到 `public` 下执行推送命令：

```bash
$ git add -A

$ git commit -m "修改内容什么的"

$ git push orgin master (此处较易出错，error了就百度吧，问题可能千奇百怪)
```

之后就可以到 `GitHub`上看提交到分支的内容，也可访问 `YOURNAME.github.io` 看页面了。

## 总结

以上整个环境部署好之后，接下来的常用命令就是以下几个：

**站点目录**下，新建文章，执行：

```bash
$ hugo new post/文章名.md
```

添加文章内容或修修改改，包括修改主题之类的，在本地都可以实时看到

修改完成，确定要上传到 `GitHub` 上后，**站点目录** `blog` 下执行：

```bash
$ hugo
```

进行编译，没错误的话修改的内容就顺利同步到 `public` 下了，然后 **`cd public`** 下，执行提交命令：

```bash
$ git add -A

$ git commit -m "修改了啥"

$ git push -u origin master
```

至此 **OK** ，顺利的话应该是一步到位的。若是遇到问题的话再查资料
