---
title: hexo blog的备份与恢复
date: 2024-07-04 18:11:53
tags: 
       - 博客
       - 功能
categories: 网络
---
## 为什么我们需要备份博客？
- 在你更换新电脑时，或在你博客出现报错而不知所措时，如果你拥有了会“备份”的超

能力，你只需要动动你的手指输入几个命令，你便会回到那一刻。你便不会感到原来的博
客已经报废了的伤心与无奈。不过别担心，这里有我，我出现了！
- 想必你点开这个博客，可能已经出现了这个处境，没关系的。那么不废话，请往下看：

## 第一步
这里我用Github作示范
首先我们得需要配置一个SSH-Key
- 在本地博客中打开git
输入：
{% codeblock %}
ssh-keygen -t ed25519 -C <你的邮箱>
{% endcodeblock %}
- 输入后：我们要按三次回车，第二次时会问你是否要覆盖，输入“y”即可
![](https://img.rolude.icu/a.png)
- 然后我们接着输入：
{% codeblock %}
cat ~/.ssh/id_rsa.pub
{% endcodeblock %}
- 获取key（显示出的信息即为密钥，如图打码所示）
![](https://img.rolude.icu/b.png)

## 第二步：配置key
- 打开github（按图一步一步来）
![](https://img.rolude.icu/1.png)
![](https://img.rolude.icu/2.png)
![](https://img.rolude.icu/3.png)
- 最后点击“Add SSh key”即可

## 第三步-创建分支和备份文件
- 创建分支
进行git初始化
{% codeblock %}
git init
{% endcodeblock %}
创建hexo的分支，用处是用来存放源码
{% codeblock %}
git checkout -b hexo
{% endcodeblock %}

- 备份文件
文件添加
{% codeblock %}
git add .
{% endcodeblock %}
- 然后提交
{% codeblock %}
git commit -m <这里为分支的名称，可以设置为"hexo">
{% endcodeblock %}
- 在github的博客仓库中添加远程的仓库
{% codeblock %}
git remote add origin <你_config.yml中的repository>
{% endcodeblock %}
- 最后部署到github
{% codeblock %}
git push origin hexo
{% endcodeblock %}

恭喜你完成了备份，接下来是怎么恢复

## 恢复博客
- 首先你得有安装hexo的环境，这里不详细讲
- 在github中下载你所创建的分支里的源文件（就是上述备份的那个）
或者在本地hexo文件夹中打开git输入：
{% codeblock %}
git clone -b hexo  <你的远程仓库地址>
{% endcodeblock %}
- 最后安装
{% codeblock %}
npm install hexo-cli
{% endcodeblock %}
{% codeblock %}
npm install
{% endcodeblock %}
{% codeblock %}
npm install hexo-deployer-git
{% endcodeblock %}
- 完成操作

之后备份博客的方法：
{% codeblock %}
git add .
git commit -m <分支的名称>
git push origin hexo
hexo g -d
{% endcodeblock %}

## 检查
- 生成博客，查看是否有报错
{% codeblock %}
hexo g
{% endcodeblock %}
- 运行博客
{% codeblock %}
hexo s
{% endcodeblock %}
- 或者
  上传博客
{% codeblock %}
hexo d
{% endcodeblock %}

## 最后
感谢您能看到最后，希望我这篇文章能够帮助你！
如果你喜欢，并且想一直支持我，赞助我可以为我提供动力
[赞助页面](/about)