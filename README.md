# xmblog

# **部署到GitHub**

1、新建仓库一： username.github.io （不用克隆到本地）
注意！
username 必须是你 Github 的账号名称，要保证和Github账号名一模一样！

新建仓库，Repository name 就填写为：`username.github.io`

2、这个仓库建好后，不用克隆到本地，内容更新修改都在下面的仓库中进行。

新建仓库二：随便起一个名字，比如：xmblog（克隆到本地）
这个项目是用来开发博客的，以后只需要改这个项目就够了。

3、自己从头搭建的项目，将项目文件夹的内容拷贝到仓库二xmblog，并在根目录下创建 deploy.sh 文件，内容如下：

```shell
#!/usr/bin/env sh
# 确保脚本抛出遇到的错误
set -e
# 生成静态文件
npm run build
# 进入生成的文件夹
cd docs/.vuepress/dist
# 如果是发布到自定义域名
# echo 'www.yourwebsite.com' > CNAME
git init
git add -A
git commit -m 'deploy'
# 如果你想要部署到 https://USERNAME.github.io
# git push -f git@github.com:USERNAME/USERNAME.github.io.git master
# 如果发布到 https://USERNAME.github.io/<REPO>  REPO=github上的项目
# git push -f git@github.com:USERNAME/<REPO>.git master:gh-pages
# 例如我部署到下边这个
git push -f git@github.com:xiaomengu/xmblog.git master:gh-pages
cd -
rm -rf docs/.vuepress/dist
```

这样仓库二和仓库一就建立了关联。会在xmblog项目下自动新建一个分支 gh-pages，项目会部署到这个分支

4、在 package.json 文件夹中添加发布命令

```json
"scripts": {  
    "dev": "vuepress dev docs",
    "build": "vuepress build docs",
    "deploy": "bash deploy.sh",
}
```

5、使用Git bash在项目根目录下运行发布命令

`npm run deploy`

6、此时打开 Github Settings 中下面的链接:
https://xiaomengu.github.io/xmblog 即可看到自己的主页啦~

# 本地库的内容推送到远程库上，Git中出现Fatal:Could not read from remote repository.的问题。

问题：把本地库的内容推送到远程库上执行完命令`git push –u origin master`出现以下问题

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal1.png)

解决办法：

1、执行命令`ssh-keygen –t rsa –C “你的邮箱”`，如下图，图中邮箱是我自己的邮箱

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal2.png)

2、执行完之后，在本地的C：Users\你自己的用户名\.ssh文件夹下，有id_rsa和id_rsa.pub文件，如图：

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal3.png)

3、打开GitHub的**Settings**设置，接着打开**SSH and GPG Keys**，再点击**New SSH Key**按钮，title可随意填写，用**记事本打开id_rsa.pub**文件，将内容全部复制，然后粘贴到**Key**中，再点击**add ssh key**按钮。

4、接着再执行`git push –u origin master`命令，依然出现下面的问题：

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal4.png)

5、考虑是本地用用户名和邮箱和GitHub账户不一致的问题，更改用户名：

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal5.png)

6、更改邮箱

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal6.png)

7、再执行git push –u origin master命令，如下：

![image](https://github.com/xiaomengu/xmblog/blob/gh-pages/img/fatal7.png)
