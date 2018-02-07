---
title: 记录搭建Hexo的问题修订
date: 2018-02-07 13:40:35
tags:
---


*这个版本主要是为了修复本地图片不显示的问题，找了一些答案是说Hexo作者的图片Markdown语法与普通的不一样，不能使用![]()这个，我在网上找到一些解决的方法，其中这篇[[Hexo发布博客引用自带图片的方法](https://www.jianshu.com/p/cf0628478a4e)]有两种解决办法，我选择了安装插件的方法。且千万要记住![DSC](url)中url不要带当前目录`./`，有了这个图片也不会显示的，这是试了好几次才终于领悟的结果。*
```

我使用的是虚拟机VMware--ubuntu 16.04 LTS--i386版本

​第一步是在github建立新的仓库: heatyux.github.io，步骤写的是**空的仓库**，我因为习惯了直接初始化仓库，建立了.git、md等，这是错误的，这也导致了和后面的步骤冲突了

​接着是要使用npm包安装hexo手脚架，因为我这个ubuntu系统并没有nodejs，所以是先要安装nodejs。因为要使用命令行安装，目前我对于cl掌握不够，只能google“ubuntu 16.04 安装 nodejs”，找到了[[Ubuntu16.04安装最新版nodejs](https://www.jianshu.com/p/2b24cd430a7d)]，这个步骤很详细，我之前更换了清华大学软件源，所以只需要前面3个步骤就安装好了nodejs。在普通用户下似乎并不能安装这个npm包：![npm-hexo-err](记录搭建Hexo的问题修订\npm-hexo-err.png)

遇到错误怎么办？直接放弃了。当然不行，有困难找google啊，所以又继续在google寻求答案，终于找到了在命令前面加`sudo` 也就是让管理群组来安装即可:

```
sudo npm install -g hexo-cli
```

​继续执行下面的3个步骤，似乎并没有error提示出来，一切都是那么的自然。当然了，问题总是伴随着成功必不可少的一步。回到第一步的步骤，我说了犯了一个错误，就是这个仓库并不是一个空仓库，我已经初始化了这个仓库，里面已经有了一些文件。执行`hexo new 开博大吉` 就出现问题了，当时我是直接忽略了，因为我没有看到有err的字眼，导致了并没有成功生成`开博大吉.md` 文件，也没有`INFO`提示这里我又犯了一个错误，就是粗心，这里有图例都没有好好确认是否一致。

​因为没有成功生成`*.md`文件，而且又初始化了仓库的`README.md`文件，当时我以为是要编辑仓库的`md`文件，所以直接是`gedit README.md`，随便编辑了点内容。当然了，这些当时我都以为是正常的进行。

​到了编辑网站设置，我又因为粗心吃了大亏，`gedit _config.yml`到是没什么问题，但是在步骤iv中，原文是**在最后一行后面新增一行，左边与 type 平齐，加上一行 `repo: 仓库地址`**，我因没有好好理解清楚，无以为是`在最后一行添加一行，与type平齐，加上repo:仓库地址` ，所以 正确的操作应该是

```
deploy:
  type: git 
  repo: git@github.com:heatyux/heatyux.github.io.git
```

我编辑为了:

```
deploy:
  type: git repo: git@github.com:heatyux/heatyux.github.io.git
```

​	到了最后两步都是有报错提示的，我有些预感是此次做hexo博客是失败的，果不其然，虽然最后，我在仓库里面看到Github Page自动生成了地址，也能打开，但并不是正确的Hexo博客，只不过是我的readme文件罢了

------

​至此第一次创建Hexo博客已失败告终，当然对于我而言失败是件好事，因为失败了，才能加深对其步骤的理解，知道哪些地方出错是要避免的。重新创建一次Hexo博客，删除原来的heatyux.github.io仓库，在ubuntu的hexo-git目录删除，重新执行:

- 新建仓库`heat-yux.github.io`，点击`Create repository`后放置，不做任何操作
- 在ubuntu里新建Document目录，进入
- 执行`sudo npm install -g hexo-cli`，别忘了在普通用户中加上`sudo`
- 继续`hexo init myBlog` 创建并初始化myBlog目录
- `npm i` 安装模块
- 前面已创建空仓库，执行`hexo new 开博大吉`，生成`开博大吉.md`文件
- 编辑 `gedit 开博大吉.md`，内容编辑"这是我第二次做hexo博客"
- 编辑`gedit _config.yml`, 修改title、author、type
- 在`_config.yml`中，在`type`后面**回车**，新增一行为`repo地址`
- 执行`npm install hexo-deployer-git --save`
- 执行`hexo deploy`
- 到浏览器新建`heat-yux.github.io` 仓库中，刷新到Github Page中生成了https://heatyux.github.io/
- 进入访问成功，是正确的Hexo博客页面

![second-create-hexo](记录搭建Hexo的问题修订\second-create-hexo.png)

第二篇博客根据文章提示，加上新的命令`hexo generate`也成功创建了博客:

![second-hexo-two](记录搭建Hexo的问题修订\second-hexo-two.png)

​**总结**：此次Hexo之行中，我真的觉得看别人操作和自己操作是完全不一样的，首先别人的使用环境就跟你的不一样，所以当你在执行命令的时候，会遇到各种各样的错误，但别担心，这些问题已经有前辈领教了，你只要能搜索关键词就能找到解决的方法，这也是一种关键的技能，不是吗？还有一定要尽可能多次尝试，不要被问题所击败，要能客观面对错误，不是自己的无能的答案。希望你能够保持耐心和对问题的不急躁，一步一步来，一步一步重新来，面对的问题多了，一步步解决，自然也就会慢慢减少，到时品尝了胜利的果实就觉得之前的问题都不是问题，而且这种感觉真的很好，想到被问题困扰的自己和现在的自己，真的很奇妙呢。
