> 本文用一首诗的版本控制，简单认识一下Git,[源码可见](https://github.com/toly1994328/Poem-GitTest):  
Git的安装，环境配置什么的我就不废话了(新手请进,高手慎入...)

---

#### 一、创建与提交

##### 1.《应龙》: v0.01 
>捷特写了一首诗《应龙》 如下：`J:\git\捷特诗集\应龙.txt`

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5efeda2ece473?w=568&h=131&f=png&s=14357)

---

##### 2.将`J:\git\捷特诗集`文件夹作为repository(版本库)
>然后打开git-bash (相比cmd而言,git-bash可以识别Linux的命令)

```
$ cd /j/git/捷特诗集

$ git init
Initialized empty Git repository in J:/git/捷特诗集/.git/
```

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f0e6dba6c263?w=1027&h=302&f=png&s=25665)


---

##### 3.将刚才写的《应龙》提交

```
$ git add 应龙.txt

$ git commit -m "《应龙》 张风捷特烈第一次提交"
[master (root-commit) c42ecee] 《应龙》 张风捷特烈第一次提交
 1 file changed, 3 insertions(+)
 create mode 100644 "\345\272\224\351\276\231.txt"
```


---

##### 4.《应龙》: v0.02
> 然后发现忘记写大名了,所以修改了一下，再提交

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f1ef949dcabb?w=543&h=122&f=png&s=15214)

```
$ git add 应龙.txt

$ git commit -m "《应龙》v0.0.2 忘记加作者了，已加"
[master 25a0323] 《应龙》v0.0.2 忘记加作者了，已加
 1 file changed, 1 insertion(+), 1 deletion(-)
```

---

##### 5.《应龙》: v0.03
>然后捷特斟酌了一下,稍加修改

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f20ae6d96dfb?w=576&h=124&f=png&s=15524)

```
$ git add 应龙.txt

$ git commit -m "《应龙》v0.0.3 稍微优化措辞"
[master cca5e1b] 《应龙》v0.0.3 稍微优化措辞
 1 file changed, 1 insertion(+), 1 deletion(-)
```


---

#### 二、时空穿梭

##### 1.提交的日志
>是不是很强大，可以将你提交的时间、备注显示出来  
其中每次提交会有一个`SHA1的commit版本号`,用来唯一表识  

```
$ git log
commit cca5e1b9ea7e28dbc608f4191f1b0ea0f15e60e9 (HEAD -> master)
Author: Administrator <1981462002@qq.com>
Date:   Sat Apr 27 22:10:27 2019 +0800

    《应龙》v0.0.3 稍微优化措辞

commit 25a0323bc71a8c8c436d94bcb6c9d472c88d6931
Author: Administrator <1981462002@qq.com>
Date:   Sat Apr 27 22:02:52 2019 +0800

    《应龙》v0.0.2 忘记加作者了，已加

commit c42eceed619d5d90b631fd6587240fdfd04fc1e9
Author: Administrator <1981462002@qq.com>
Date:   Sat Apr 27 21:56:42 2019 +0800

    《应龙》 张风捷特烈第一次提交
```

>那master和HEAD又是什么呢?这里先看下图

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f2b5bea4f1cf?w=756&h=174&f=png&s=10412)

---


##### 2.版本回溯
>现在我想看看V0.0.2版的内容可不可以呢? `reset --hard HEAD~1` 移动头节点 ~移多少个

```
$ git reset --hard HEAD~1
HEAD is now at 25a0323 《应龙》v0.0.2 忘记加作者了，已加
```

>然后你会发现V0.0.2版的内容就回来了,但当你再`git log`时，发现v0.0.3版的木有了,怎么回去呢?


![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f3015d19d45f?w=533&h=126&f=png&s=14756)


```
$ git log
commit 25a0323bc71a8c8c436d94bcb6c9d472c88d6931 (HEAD -> master)
Author: Administrator <1981462002@qq.com>
Date:   Sat Apr 27 22:02:52 2019 +0800

    《应龙》v0.0.2 忘记加作者了，已加

commit c42eceed619d5d90b631fd6587240fdfd04fc1e9
Author: Administrator <1981462002@qq.com>
Date:   Sat Apr 27 21:56:42 2019 +0800

    《应龙》 张风捷特烈第一次提交
```


![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f353d187b3fc?w=765&h=178&f=png&s=12867)

---


##### 3.怎么回到V0.0.3版
>突然想到那个SHA1的提交号应该不是吃干饭的,往上一翻,还在:

```
$ git reset --hard cca5e1b9ea7e28dbc608f4191f1b0ea0f15e60e9
HEAD is now at cca5e1b 《应龙》v0.0.3 稍微优化措辞
```

> 然后你会发现V0.0.3版的内容就回来了,git log 看一下又回到刚才了  
但是我要是关了终端，找不到SHA1值怎么办?

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f3c9ebcdae9b?w=540&h=125&f=png&s=14808)

---

##### 4.`git reflog` 前来救驾
> 这里可以看到v0.0.3提交的信息， `cca5e1b` 就是提交的SHA1开头的几个字母  
注意:`git reset --hard`不须要完整的SHA1值，它会自己找:所以`SHA1手中握,版本任穿梭`

```
$ git reflog
25a0323 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~1
cca5e1b HEAD@{1}: reset: moving to cca5e1b9ea7e28dbc608f4191f1b0ea0f15e60e9
25a0323 (HEAD -> master) HEAD@{2}: reset: moving to HEAD~1
cca5e1b HEAD@{3}: commit: 《应龙》v0.0.3 稍微优化措辞
25a0323 (HEAD -> master) HEAD@{4}: commit: 《应龙》v0.0.2 忘记加作者了，已加
c42ecee HEAD@{5}: commit (initial): 《应龙》 张风捷特烈第一次提交

$ git reset --hard cca5e1b
```


---

#### 三、远程仓库 ： Github 
> 你可以将Github当成一个有图形界面的文件存储服务器，简称`远程仓库`    
> 现在我想邀请远在火星的龙少来帮我推敲一下这首诗  


##### 1.Github 账号上创建一个ssh Key

```
$ ssh-keygen -t rsa -C "1981462002@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/Administrator/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/Administrator/.ssh/id_rsa.
Your public key has been saved in /c/Users/Administrator/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:3uKFITBRP8RXzkgiN9QG1qySSxitzokD2jjHOGKkuJ4 1981462002@qq.com
The key's randomart image is:
+---[RSA 2048]----+
|    .oooO=...    |
|    ...*.+*+     |
|    o+ .o+. o    |
|..  oo+ ..       |
|=* + o.oS        |
|X.* + .o +       |
|o= .    + o      |
|. .    . o       |
|.E      .        |
+----[SHA256]-----+
```

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f68012a332bd?w=1168&h=427&f=png&s=53848)


---

##### 1.将远程仓库项目拷贝到本地

```
$ git clone git@github.com:toly1994328/Poem-GitTest.git
Cloning into 'Poem-GitTest'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
```


---

##### 2.将刚才的诗拷贝一下提交

> 这样龙少就可以用浏览器访问Github看到了

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f7df71ec06ef?w=908&h=312&f=png&s=19000)

```
$ git add 应龙.txt

$ git commit -m "《应龙》v0.0.1 提交远程仓库"
[master 6342daf] 《应龙》v0.0.1 提交远程仓库
 1 file changed, 3 insertions(+)
 create mode 100644 "\345\272\224\351\276\231.txt"

|--- 现在只是本地提交 ,远程仓库是没有记录的，需要下面:--------------
$ git push -u origin master
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 475 bytes | 475.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:toly1994328/Poem-GitTest.git
   1cd6839..6342daf  master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

---

##### 3.远程协作
> 这时龙少看到了，然后fork一下，改了一个字，然后发起一个requst

![](https://user-gold-cdn.xitu.io/2019/4/28/16a5f94420e47bbc?w=1229&h=545&f=png&s=62795)


---

##### 4. 同意修改 ： Merge requst


![](https://user-gold-cdn.xitu.io/2019/4/28/16a5f987f625f4e3?w=1223&h=265&f=png&s=35629)


---

##### 5. 现在本地和仓库的文件不一致了怎么办?

```
|--- 一句话搞定 ----------
$ git merge origin master # 融合origin远端的master分支
或者：git pull origin master # 拉取远端master分支的资源

|--- 当需要查看一下信息时: ----------
$ git remote -v # 查看远端的名称
origin  git@github.com:toly1994328/Poem-GitTest.git (fetch)
origin  git@github.com:toly1994328/Poem-GitTest.git (push)

$ git diff origin master # 查看本地文件与远端的差异
diff --git "a/\345\272\224\351\276\231.txt" "b/\345\272\224\351\276\231.txt"
index f5dd948..e85e740 100644
--- "a/\345\272\224\351\276\231.txt"
+++ "b/\345\272\224\351\276\231.txt"
@@ -1,3 +1,3 @@
 应龙  ---- 张风捷特烈
-一游小池两岁月，洗却凡世几闲尘。
-时逢雷霆风会雨，应乘扶摇化入云。
+戏游小池两岁月，洗却凡世几闲尘。
+时逢雷霆风会雨，应乘扶摇化入云。
```

> OK,这样就完成了一次简单的多人协作

---

##### 6.冲突与解决
>捷特此时改了一下本地文件，添加了创作日期，暂时没有提交

![](https://user-gold-cdn.xitu.io/2019/4/28/16a614c7a23d64ca?w=562&h=142&f=png&s=15720)


>龙少又改了一下:捷特也merge了,说明服务器仓库的文件已改变

![](https://user-gold-cdn.xitu.io/2019/4/28/16a614d6ae16ce10?w=1223&h=257&f=png&s=27369)


>捷特将本地拉仓库的文件时和本地文件发生冲突,然后本地文件就成这样了:

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6162b249f2d24?w=1006&h=259&f=png&s=28498)

```
$ git add 应龙.txt

$ git commit -m "《应龙》v0.0.2 添加日期"
[master 308dc12] 《应龙》v0.0.2 添加日期
 1 file changed, 1 insertion(+)

$ git pull origin master # 先将服务器上的拉下来
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), done.
From github.com:toly1994328/Poem-GitTest
 * branch            master     -> FETCH_HEAD   # 本地
   55f6a69..0185ee5  master     -> origin/master # 远端的仓库中
Auto-merging 应龙.txt
CONFLICT (content): Merge conflict in 应龙.txt # 发生冲突了
Automatic merge failed; fix conflicts and then commit the result.

---->[提交解决冲突之后的文件]-------------------------------
$ git add 应龙.txt

$ git commit -m "《应龙》--解决冲突"
[master f508868] 《应龙》--解决冲突

$ git push -u origin master #推到服务端仓库
Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 638 bytes | 638.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 2 local objects.
To github.com:toly1994328/Poem-GitTest.git
   0185ee5..f508868  master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```


---


#### 四、分支

##### 1.主分支
>每一次的提交相当于创建了一个节点，它有一个唯一的SHA1值来确定它的唯一  
在一个git项目初始时，会`默认创建分支master`,如果你一直修改/提交,就会成为一条长线  

![](https://user-gold-cdn.xitu.io/2019/4/27/16a5f2b5bea4f1cf?w=756&h=174&f=png&s=10412)


---

##### 2.创建分支：`git branch XXX`
>当v.0.0.3已经符合预期了,现在我有个想法，把这首诗写成8句话  
现在新建一个分支dev来开发这个版本

```
$ git branch # 查看当前分支
* master

$ git branch dev #创建名为dev的分支

$ git branch # 查看当前分支,当前还在master上
  dev
* master

$ git checkout dev #切换到dev分支
Switched to branch 'dev'
```

>注：创建并切换到dev分支`git checkout -b dev`

---

##### 3. 在 dev 分支提交

![](https://user-gold-cdn.xitu.io/2019/4/28/16a619733ccdba1e?w=909&h=258&f=png&s=28746)

```
$ git add 应龙.txt
$ git commit -m "dev 分支第一次提交"
```

![](https://user-gold-cdn.xitu.io/2019/4/28/16a619913d08b28e?w=891&h=234&f=png&s=26918)

![](https://user-gold-cdn.xitu.io/2019/4/28/16a61a91469b6a30?w=867&h=233&f=png&s=29714)

>经过三次提交之后，觉得还行了，于是：

---

##### 4.将dev分支merge到主分支

![](https://user-gold-cdn.xitu.io/2019/4/28/16a628ef69c50fcc?w=772&h=232&f=png&s=21276)

```
$ git checkout master #回到主分支

$ git merge dev # merge到主分支
Updating f508868..78f60b0
Fast-forward
 "\345\272\224\351\276\231.txt" | 2 ++
 1 file changed, 2 insertions(+)
 
$ git push -u origin master #推到服务端仓库
```



> 可以查看记录和Merge的情况

```
$  git log --graph --pretty=oneline --abbrev-commit
* 78f60b0 (HEAD -> master, origin/master, origin/HEAD, dev) dev 分支第三次提交
* e34cd69 dev 分支第二次提交
* 37097fc dev 分支第一次提交
*   f508868 《应龙》--解决冲突
|\
| *   0185ee5 Merge pull request #2 from zfjtl/patch-1
| |\
| | * 38300ed Update 应龙.txt
| |/
* | 308dc12 《应龙》v0.0.2 添加日期
|/
*   55f6a69 Merge pull request #1 from zfjtl/master
|\
| * fe2d3bf Update 应龙.txt
|/
* 6342daf 《应龙》v0.0.1 提交远程仓库
* 1cd6839 Initial commit
```

>`注:回溯某分支的某版本，和上面一样，只要用SHA1就行了`

---


##### 5.将本地分支同步到github

![](https://user-gold-cdn.xitu.io/2019/4/28/16a61fb45ad23431?w=1044&h=245&f=png&s=21785)

```
$ git push origin dev
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/toly1994328/Poem-GitTest/pull/new/dev
remote:
To github.com:toly1994328/Poem-GitTest.git
 * [new branch]      dev -> dev
```


---


##### 6.打标签和同步到github

![](https://user-gold-cdn.xitu.io/2019/4/28/16a620f2c35fe32e?w=1045&h=219&f=png&s=27634)

```
git tag v0.0.4 # 打标签

$ git push origin --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:toly1994328/Poem-GitTest.git
 * [new tag]         v0.0.4 -> v0.0.4


$ git show v0.0.4 #查看标签
commit 78f60b055efb8b7daf59951f3f1558d623b11b1a (HEAD -> master, tag: v0.0.4, origin/master, origin/HEAD)
Author: Administrator <1981462002@qq.com>
Date:   Sun Apr 28 09:56:05 2019 +0800

    dev 分支第三次提交

diff --git "a/\345\272\224\351\276\231.txt" "b/\345\272\224\351\276\231.txt"
index 4fe0222..42858c1 100644
--- "a/\345\272\224\351\276\231.txt"
+++ "b/\345\272\224\351\276\231.txt"
@@ -2,5 +2,6 @@
 一游小池两岁月，洗却凡世几闲尘。
 时逢雷霆风会雨，应乘扶摇化入云。
 蛇虫何力卷波涛，雀鸟焉能平九霄。
+龙鹏所至非宏志，莫以已见比拟之。
                        2018.2.2  捷特作
             2019.4.27 龙少批阅
```

---


##### 7. 遇到bug时
>可见确实有点小问题

![](https://user-gold-cdn.xitu.io/2019/4/28/16a621dfb50b1a3e?w=850&h=206&f=png&s=19763)

```
git checkout -b featrue

$ git add 应龙.txt
$ git commit -m "featrue 分支修复bug"

|--- 合并featrue到dev分支
git checkout dev
git merge featrue

git checkout master
git merge dev

git push -u origin master #推到服务端仓库
git push origin featrue

git tag v0.0.5 # 打标签
git push origin --tags # 标签推到服务端仓库
```

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6232bcbeb40d5?w=951&h=278&f=png&s=31145)

![](https://user-gold-cdn.xitu.io/2019/4/28/16a623168699a30d?w=1143&h=300&f=png&s=30057)


---

##### 8.现在想加新功能
>用markdown的格式来写,就在featrue分支来改吧,将文件名改为`应龙.md`

```
git checkout featrue

$ git add 应龙.md
$ git commit -m "featrue markdown的格式"

git push -u origin featrue # 将修改同步到feature分支
```

![](https://user-gold-cdn.xitu.io/2019/4/28/16a623eeb622ae96?w=1032&h=224&f=png&s=24681)

> 感觉还不错，然后merge到dev上,可以暂时不merge到master，继续开发,就像这样：

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6240a6b860fc3?w=881&h=281&f=png&s=35359)


```
git checkout dev
git merge featrue

dev继续开发...

git checkout master
git merge dev
git push -u origin master # 将修改同步到feature分支

git tag v0.0.6 # 打标签
git push origin --tags # 标签推到服务端仓库
```

---

#### 五、可视化界面

##### 1.TortoiseGit

>命令行写起来不舒服的人可以选择一些可视化的工具

![](https://user-gold-cdn.xitu.io/2019/4/28/16a62733192f235d?w=997&h=218&f=png&s=25559)

> 可以很方便的查看某次提交的修改内容

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6272259463498?w=960&h=311&f=png&s=45238)

> 可以很清晰的看到提交的流程

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6270f2f3644e6?w=942&h=335&f=png&s=46816)

---

##### 2.Idea家族的软件，比如AndroidStudio
>首先在Settings里配置

![](https://user-gold-cdn.xitu.io/2019/4/28/16a62776d7515b2b?w=1038&h=313&f=png&s=30620)

---

>然后将项目导入AndroidStudio(虽然不是Android项目，但是也没关系)

![](https://user-gold-cdn.xitu.io/2019/4/28/16a627909cb03cf0?w=1263&h=510&f=png&s=244758)

---

>修改和push到远程仓库

![](https://user-gold-cdn.xitu.io/2019/4/28/16a62864265a5a9f?w=1217&h=263&f=png&s=60178)


---
>切换分支

![](https://user-gold-cdn.xitu.io/2019/4/28/16a6288b7b68de7b?w=960&h=268&f=png&s=40732)


---

#### 六、小结
>Git 就是`安心丸 + 后悔药`，git一下，何乐不为? 

##### 1.配置相关

```
查看版本号：    git --version
查看配置:       git config --list
                    |--- git config --list --global
                    |--- git config --list --system
                    |--- git config --list --local
查看单一信息:   git config user.email
```

---

##### 2.操作相关

```
初始化:     git init
添加文件：  git add <file>
提交记录：  git commit -m <备注>
记录溯回：  git reset --hard HEAD~<step>
记录溯回：  git reset --hard <SHA1>
删除文件：  git rm <file>
查看状态：  git status
打标签：    git tag v0.0.6
```

---

##### 3.查看相关

```
git log
git reflog
git reflog --all
git log --graph
git log --graph --pretty=oneline --abbrev-commit
```

---

##### 4.远端相关

```
克隆项目：      git clone git@github.com:toly1994328/Poem-GitTest.git
推送到远端：    git push -u origin <branch>
拉取远端资源：  git pull origin <branch>
与远端同步：    git merge origin <branch>
查看远端信息：  git remote -v
查看远端差异：  git diff origin <branch>
推送标签：      git push origin --tags
```

---

##### 5.分支相关

```
查看分支：              git branch
创建分支：              git branch <name>
切换分支：              git checkout <name>
创建+切换分支：         git checkout -b <name>
合并目标分支到当前分支:  git merge <目标分支>  
删除分支：              git branch -d <name>
```
