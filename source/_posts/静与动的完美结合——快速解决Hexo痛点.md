---
abbrlink: ''
categories:
- - 技术
copyright: 原创
cover: /images/uploads/post_45965.jpg
date: '2023-06-08T19:35:43.777122+08:00'
locate: ''
recommend: ''
tags:
- 关于小站
thumbnail: /images/uploads/post_45965.jpg
title: 静与动的完美结合——快速解决Hexo痛点
top: true
updated: 2023-7-12T21:21:8.95+8:0
swiper_index: 1
top_group_index: 1
---
## 写在前面

这是我正式更换博客引擎（Jekyll-Hexo）后的第一篇文章，也是我很少写的技术类的文章，与其说是教程，还不如说是**我为什么要用 Hexo**

让我们直接步入正题

正如我之前在 ⟪博客大揭秘——“什么？你问我为什么用Jekyll”⟫ 这篇文章里所说的一样：

* Can1425：但jekyll比它们方便
* **Q：**咋方便（好奇）
* **Can1425：**因为Github直接支持jekyll，所以仓库里是jekyll的源文件。如果用hexo的话，多端写文章很不方便，我总不能在这个电脑部署一次，那个电脑再部署一次吧
* **Q：**确实，但是可以clone，也能实现分布式呀
* **Can1425：**但是jekyll的话，只需要在另外一端登陆github就行了。
* **Can1425：**其实我也想用hexo，但最后还是选择了jekyll，就是因为“方便”二字
* **Can1425：**只可惜好主题太少了
* **Q：**话说如果可以的话我还是建议体验一下hexo（可以deploy到gitee gitee有一个镜像仓库的功能 可以把推送到gitee的推送到github 然后手动设置一下action也能用
* Can1425：未来有期吧，当下就当jekyll钉子户

是的，这些都是我在试水 Hexo 时遇到的问题

**那我为什么现在有用了 Hexo 呢？**

## 第一步——Qexo

Hexo 对于我来说最大的痛点就是

* 不能像 Jekyll 一样在线编辑

经过在网上的疯狂冲浪，我发现了个好东西——

* Qexo

是的，让我们来看看他的官方介绍

### 介绍

**Qexo** 是一个快速、强大、美观的在线 **静态博客编辑器**。使用 GPL3.0 **开源**协议。支持包括且不限于在 **Vercel** 等平台部署, 为您的静态博客添加**动态**的元素

### 安装 Qexo

这里以Vercel 部署 (MySQL/PlanetScale)为例？

你可以通过使用 PlanetScale 提供的免费数据库

### 申请 PlanetScale 数据库[#](https://www.oplog.cn/qexo/start/build.html#%E7%94%B3%E8%AF%B7-planetscale-%E6%95%B0%E6%8D%AE%E5%BA%93)

[注册 PlanetScale 账号](https://www.planetscale.com/) 创建免费 MySQL 数据库(不支持大陆IP), 区域**一定要选择 AWS / N. Virginia (us-east-1)**, 并记录数据库连接信息

### 一键部署[#](https://www.oplog.cn/qexo/start/build.html#%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2)

[![部署到 Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/am-abudu/Qexo)

首次部署会报错, 请无视并重新进入项目, 在项目设置界面添加环境变量 Environment Variables

其中 `PLANETSCALE` 用于禁用外键约束, 以防止PlanetScale数据库部署失败, 若你自备数据库且没有特殊需求请**不要填写**

在 Deployments 点击 Redeploy 开始部署, 若没有 Error 信息即可打开域名进入初始化引导

更多方式详见([Qexo | Qexo (oplog.cn)](https://www.oplog.cn/qexo/start/build.html#vercel-%E9%83%A8%E7%BD%B2-mongodb)

没错，这就成了

## 第二步——设置 Github Actions 自动化部署

### 介绍

在使用GitHub Actions之前，它的几个基本概念必须要了解一下：

* **Workflows（工作流程）**

持续集成的运行过程称为一次工作流程，也就是我们项目开始自动化部署到部署结束的这一段过程可以称为工作流程，一个工作流程中由一个或者多个任务（job）组成。

* **Jobs（任务）**

一个工作流程中包含多个任务，简单来说就是一次自动部署的过程中，需要完成一个或多个任务，这些任务里面又包含了多个步骤（step）。

* **Step（步骤）**

我们开发项目需要按照一个一个的步骤来进行，自动部署也一样，在一个任务中，步骤需要一步步的完成。

* **Action（动作）**

每个步骤（step）可以包含一个或多个动作，比如我们在一个步骤中执行打包命令这个Action。

上面4点是GitHub Actions中几个大的概念，也很好理解，大家可以把它想象为一条完整的流水线，流水线包含的几个操作要点如下：

**workflow->job->step->action**

### 语法简介

上面的概念介绍只是从宏观层面解读的，具体如何实现还需要我们了解具体的额语法，就好比一个工人修房子，具体步骤是知道了，那么具体工具还需要确定，这些工具就是我们需要了解的GitHub Actions语法。

#### **1 name**

定义workflow的名称，如果没有定义，则会默认使用执行脚本文件名作为workflow名称，实例代码如下：

```yaml
name: GitHub Actions Demo
```

#### **2 on**

触发workflow的条件或者事件，比如push的时候就像执行workflow，实例代码如下：

```yaml
# 单个事件
on: push

# 多个事件列表
on: [push, pull_request]

# 当main分支发生push操作时执行workflow
on:
  push:
    branches:
      - main
```

#### **3 jobs**

jobs是一个workflow的核心任务，我们大部分的操作在jobs中完成，我们的任务（job）放在jobs这个集合下，每一个job有以下几个核心的字段组成：

**（1）jobs.<job\_id>**

jobs中每一项任务都有任务id，实例代码如下：

```yaml
jobs:
  my_first_job:   // 任务id
    name: My first job
  my_second_job:
    name: My second job
```

**（2）jobs.<job\_id>.name**

每一项任务具有任务名称，好比我们做每一项工作时都有一个工作名称，实例代码如下：

```yaml
jobs:
  my_first_job:  
    name: My first job  // 任务任务名称
  my_second_job:
    name: My second job
```

**（3）jobs.<job\_id>.needs**

needs字段用来指定当前任务的一些依赖关系，比如一个任务依赖于另外两个任务，实例代码如下：

```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

上面代码展示了三个任务之间的依赖关系，所以执行顺序应该是job1、job2、job3.

**（3）jobs.<job\_id>.runs-on**

该字段用来指定命令的运行虚拟机环境，可以理解为我们的任务要在哪个环境中执行，实例代码如下：

```yaml
runs-on: ubuntu-18.04
```

GitHub Actions给我们提提供的运行环境主要有以下几种：

* `ubuntu-latest`，`ubuntu-18.04`或 `ubuntu-16.04`
* `windows-latest`，`windows-2019`或 `windows-2016`
* `macOS-latest`或 `macOS-10.14`

**（4）jobs.<job\_id>.steps**

step是job中的重点，一个job可以包含多个步骤，比如一个项目就是一个任务，我们需要分为多个步骤来完成这个项目，实例代码如下：

每个步骤包含下面三个字段：

```text
jobs.<job_id>.steps.name：步骤名称。
jobs.<job_id>.steps.run：该步骤运行的命令或者 action。
jobs.<job_id>.steps.env：该步骤所需的环境变量。
```

上面代码中run就是我们该步骤需要执行的命令，比如打包命令：npm run build。当然也可以使用人家造好的轮子，直接使用人家的action。

---

以上只是简单介绍了GitHub Actions中重要的一些概念和语法，以满足我们基本的自动化部署操作，更多详细语法可以移步官网：

[GitHub Actions](https://docs.github.com/cn/actions)

### 理论结束，实践开始

#### 生成秘钥

如果你的 Hexo 可以正常地部署到 GitHub，那么实际上你原来的秘钥是可以正常使用的。

但是我的私钥还用于不同的服务器的 SSH 访问和其他身份验证，因此，我们生成一个新的秘钥对来专门部署 Hexo。

以下为 macOS 下的操作，Linux 下操作方法相同，Windows 10 用户可以在市场中安装 Ubuntu 以后执行：

```bash
ssh-keygen -t rsa -b 4096 -C "Hexo Deploy Key" -f github-deploy-key -N ""
```

这会在当前目录生成两个文件：

* github-deploy-key —— 私钥
* github-deploy-key.pub —— 公钥

#### GitHub 配置秘钥

我们把 `私钥`放到我们存放 Hexo 原始文件的代码仓库里面，用于触发 Actions 时使用。

把 `公钥`放到 GitHub Pages 对应的代码仓库里面，用于 Hexo 部署时的写入工作。

##### 配置私钥

首先在 GitHub 上打开保存 Hexo 的仓库，访问 `Settings -> Secrets`，画面如下：

![](https://pic3.zhimg.com/80/v2-78fca9d3aecf4fef4cdbc759dd4d827e_720w.webp)

然后选择 `New secret`

![](https://pic1.zhimg.com/80/v2-9c37b4488b83579e01e58ef3b0f34fd8_720w.webp)

名字部分填写：`HEXO_DEPLOY_KEY`，注意大小写，这个后面的 GitHub Actions Workflow 要用到，一定不能写错。

在 `Value` 的部分填入 `github-deploy-key` 中的内容：

![](https://pic3.zhimg.com/80/v2-d963d2f26452fa39ec6b7187926a48de_720w.webp)

添加了私钥以后的界面显示如下：

![](https://pic4.zhimg.com/80/v2-e7990155f2bf12eecb521c3968379987_720w.webp)

##### 添加公钥

接下来我们需要访问存放网页的仓库，也就是 Hexo 部署以后的仓库，比如：`yourname.github.io` 这种，访问 `Settings -> Deploy keys`：

![](https://pic1.zhimg.com/80/v2-f8d27de9af570b8a3bcb70ca0a4983fc_720w.webp)

按 `Add deploy key` 来添加一个新的公钥：

![](https://pic1.zhimg.com/80/v2-1f3873d498087fb7334dd49b16bc0d48_720w.webp)

在 `Title` 中输入：`HEXO_DEPLOY_PUB` 字样，当然也可以填写其它自定义的名字。

在 `Key` 中粘贴 `github-deploy-key.pub` 文件的内容。

> 注意：一定要勾选 `Allow write access` 来打开写权限，否则无法写入会导致部署失败。

![](https://pic3.zhimg.com/80/v2-247aaf40961d62979658d47abfb56686_720w.webp)

最后添加好了公钥的界面如下：

![](https://pic2.zhimg.com/80/v2-e85375698b274f6bc6b61d10c7609019_720w.webp)

#### 创建 Workflow

首先在 Hexo 的仓库中创建一个新文件：`.github/workflows/deploy.yml`，文件名可以自己取，但是一定要放在 `.github/workflows` 目录中，文件的内容如下：

```yaml
name: Hexo Deploy

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-18.04
    if: github.event.repository.owner.id == github.event.sender.id

    steps:
      - name: Checkout source
        uses: actions/checkout@v2
        with:
          ref: master

      - name: Setup Node.js
        uses: actions/setup-node@v1
        with:
          node-version: '12'

      - name: Setup Hexo
        env:
          ACTION_DEPLOY_KEY: ${{ secrets.HEXO_DEPLOY_KEY }}
        run: |
          mkdir -p ~/.ssh/
          echo "$ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
          chmod 700 ~/.ssh
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          git config --global user.email "john@doe.com"
          git config --global user.name "John Doe"
          npm install hexo-cli -g
          npm install

      - name: Deploy
        run: |
          hexo clean
          hexo deploy
```

简单解释一下，当我们推送内容到远程 `master` 分支的时候，就会触发这个 Workflow。

使用 `Ubuntu 18.04` 作为 `hexo deploy` 的系统。

首先 checkout 源代码，然后设置使用最新的 Node.js v12 LTS 作为 node 解释器。

接下来就是创建 SSH 相关的配置文件，注意 `secrets.HEXO_DEPLOY_KEY` 就是对应我们之前设置的私钥，所以名字一定不要搞错。

`git config` 相关的名字和邮件地址替换成大家自己使用的就好了。

最后就是安装 Hexo CLI，各个依赖模块和部署了。

#### 验证

下面就是 GitHub Actions 页面显示的运行结果：

![](https://pic1.zhimg.com/80/v2-3046f9fb7bae9e4c528574ecdd253778_720w.webp)

前面有绿色钩钩的，就表示部署成功，红色叉叉的表示失败。如果部署失败，还会收到 GitHub 的邮件提醒。

## 第三步——Qexo初始化

访问你部署在 Vercel 项目的访问链接

一般是 xxx.vercel.app

会自动进入初始化页面，按照步骤配置好后就可以快乐的写文章了

![Happy](https://user-images.githubusercontent.com/51912589/159258766-19a1ce22-d34b-4b29-b291-7d70e8942859.png)

## 真正的正片

上面的这些东西实在有些不好理解（我是怎么写出来的？），以下的方法才是我真正在使用的方法：

### 介绍

额(⊙﹏⊙)，我是真说不清楚，总之你照着做就行了（悲

### 理论结束，正片开始

先 Fork 这个仓库

[xiaohao8/xiaohao8.github.io](https://github.com/xiaohao8/xiaohao8.github.io)

然后随便命个名

然后

就行了（￣︶￣）↗　

### 部署 Qexo

太懒了，懒得再写了（悲，就直接看上面的吧

![Happy](https://user-images.githubusercontent.com/51912589/159258766-19a1ce22-d34b-4b29-b291-7d70e8942859.png)

## 结语

博客，是一个留给自己的一个网络上的家，它也要以实用为主，如果你只有轻度的博客需求，你可以尝试用用 Jekyll ，Hexo 更适合爱折腾得的朋友们，总之，只要自己觉得舒服就好

码字不易，可以在下方留点评论或转发吗？

希望一个 Hexo 小白整理的教程能对你有帮助

## 鸣谢

[会飞的猪 - 知乎 (zhihu.com)](https://www.zhihu.com/people/luhongquan)

[Tommy - 知乎 (zhihu.com)](https://www.zhihu.com/people/tommy_lau)

[Qexo (github.com)](https://github.com/Qexo)
