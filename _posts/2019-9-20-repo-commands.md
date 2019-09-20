 

# repo 常用命令

### repo简介

***

**repo是用来管理N个git仓库的工具** 

它需要一个*manifest.xml*脚本来记录都有哪些*git*仓库需要一起下载下来,组成一个完整的项目。不指定*manifest.xml*则使用默认的*default.xml*。

一个*manifest.xml* 文件中可以有多个“remote”，每个 remote 有各自的名字（name 属性），通过各自的 fetch 属性给出了相应的 *project git remote URL* 的计算方法。

其中有一个 remote 和 revision 默认值设置 <default remote="XXX" revision="YYY"/>。

每个 project 都可以指定 remote（如果没有指定就采用前面的 default remote）和 revision（如果没有指定则采用 default revision）(revision 一般是一个分支的名字，但也可以是某个 git commit 的 hash，尤其是在 manifest 快照中)。

每个project指定了name属性或者patch属性，如果只指定了一个，则另一个取相同的值。

其中 path 属性决定代码同步下来之后，该 project 在文件系统中的路径。

name 属性与该 project 的 remote 属性（及 xml 中该 remote 的 fetch 属性）相结合，确定出该项目的远程服务器 URL。

***

#### repo sync
同步最新本地工作文件，更新成功，这本地文件和 server 的代码是一样的。可以指定需要更新的project ，如果不指定任何参数，会同步整个所有的项目。
如果是第一次运行 repo sync ，则这个命令相当于 git clone，会把server所有内容都拷贝到本地。
根据manifests中的xml文件中git的commit进行同步，这个再repo init的时候指定使用哪个xml；
如果不是第一次运行 repo sync ，则相当于 git remote update ;  git rebase origin/branch .将server上的code与本地合并；repo sync 会更新 .repo 下面的文件。如果在merge 的过程中出现冲突，这需要手动运行：git  rebase --continue

***

#### repo branch
repo分支：这里通过repo init -b <branch>，中的-b所指定的分支，是manifests的分支，不同分支，其中的文件清单内容有所不同。 
xml分支：通过清单文件manifest.xml中的default实体的revision属性，指定版本库默认的分支为revision属性值，该属性值做为repo sync之后工作目录中所有git项目的公共起点分支，也就是说，该manifest对应所有的git项目都有一个以revision属性值为名的分支，repo sync之后，在任意一个repo工作目录下的git库中，使用git branch或者repo start创建的分支，都是基于该git库中revision属性值为名的分支来创建。我们可以将这个分支设置为和repo分支类似的名字。

***

#### repo start
使用repo start -all创建分支，基于xml文件的commit和branch进行创建，使用repo checkout 之后将会变成以repo init 初始化指定的xml文件的所有时期软件的commit，相当于恢复到之前的一个软件版本；

***

### 代码提交

```
git add -A
git add filename
git commit -m "note"
git push origin master
 1. 查看远程分支：git branch -a
 2. 创建本地分支：git checkout -t  (必须与远程分支路径一致)
 3. 查看要上传的代码:  git status
 4. 添加代码: git add (代码路径)
 5. git commit -m "评审标识"   
 6. git push remote HEAD:refs/for/branch || git push project  HEAD:refs/for/master   上传到服务器分支
 git push [远程仓库名] [本地分支名：refs/for/远程分支名]
```

***

### **撤销commit**

**情境1：**有的时候你只需要撤销commit，但并不想将commit下的代码也撤销，那么可以先找到你的最新的commit号

```
git log
```

撤销上一次的commit

```
git reset HEAD~
或者
git reset HEAD~1
如果你提交了多个commit，那么可以通过修改HEAD~之后的数字，如撤销前3次的commit
git reset HEAD~3
```



**情境2：**如果你使用了多次*git commit*命令，但是发现刚刚*commit*的内容不需要提交了，需要恢复到上一次的*commit*时，使用如下命令：

```
git reset --hard HEAD^1
```

注：使用了之后，你最新的*commit*命令下修改的内容将完全被撤销。

***

### 切SDK

*written by: zhouming*

> #### **切之前准备：**

> > + *要切换sdk的小系统*
> >
> > + *整编通过的新的大系统*
> >
> > + *旧的大系统*
> >
> >   ***

> + 首先将小系统下***platform/on-project/src/***的文件全部拷贝到***platform/public-project/src***下
>   然后再用 ***repo merge -i(小系统根目录路径) --public*** 将***platform/public-project/src***下的代码
>   合入到旧的大系统中(命令在旧大系统根目录执行)
>
>   ***
>
> + 修改小系统下的 ***.repo/manifests/default.xml*** 文件，把 release 切换到最新。然后在小系统根目录执行 ***repo sync*** 同步仓库到最新
>
>   ***
>
> + #### **SDK中同步**
>
>   + 将小系统中已经切换到新大系统的 release 仓库中release-manifest.xml 文件复制到 NEW_SDK 大系统 ***.repo/manifests*** 目录下；
>
>   + 在 NEW_SDK 大系统根目录执行 ***repo init -m release-manifest.xml*** ， 将 manifest.xml 文件链接指向 release-manifest.xml；
>
>   + 然后执行 ***repo start develop --all*** 创建 develop  (创建并切换分支) 分支并同步源码到到新的大系统中
>
>     ***
>
> + #### **合并代码**
>
>   + 比较代码差异
>     (1) 分别在新大系统和旧大系统中用***git diff*** 命令比较代码差异，如果文件文件没差异则不用管
>     (2) 如果文件有差异则合并差异
>   + 合并差异
>     (1).打开一个旧的大系统并用***git diff***命令比较文件差异
>     (2).用***git checout***文件回退到新大系统的文件(有差异的那个文件)	
>     (3).在新的大系统中用***vimdiff*** 同时打开新大系统和旧大系统的代码
>     (4).再打开一个新的大系统并用 ***git log -p*** 打开文件
>   + 在vimdiff中，通过第2步的1和4判断不同文件是否合入
>
>   ***
>
> + 在大系统中用 ***git status*** 查看大系统修改的文件并进入到对应目录下编译修改的文件
>   把小系统中***platform/on-project/pub/system/***的对应目录下的文件删除，然后第五步生成的文件拷贝到对应的目录下
>
> +  将***platform/public-project/pub/image***下的文件拷贝到 ***platform/on-project/pub/image*** 下
>
> + 将***platform/on-project/src/***的文件全部删除，在新大系统根目录执行 ***repo diff -o(小系统根目录路径)*** 将大系统修改的代码拷贝到小系统对应的目录
>
>   ***
>
> + 在小系统执行***git status*** 查看修改的代码并删除下面 ***git add*** 的红色代码(如果有)
>
> + 在大系统中用***git diff***比较第九步小系统中删除的代码，删除的是没有差异的 
>   编译小系统就行自测，没问题将修改的代码提交gerrit 评审
>
> + ***pubilc-project*** 公共仓库增加的只有我这个项目针对公共仓库的变更 针对公共仓库的差异合到 项目仓库 ***repo diffext*** 把公共仓库所有的修改拷贝到 ***on-project*** 项目仓库下面 

***

### **定制代码合并工具**

1. ***repo merge*** 将小系统代码合并到大系统

   如果项目报了问题，在修改问题时，首先要把小系统的定制代码同步到大系统上，如果项目小系统固定了发布点，还需要同时将大系统代码回退到固定点上。我们使用repo merge命令来完成这个操作：

   ```
   repo merge [<project>...] [-b <new-branch>] [--copy-only] -i <small-system-rootdir>
   # 参数介绍：
   #     project，表示要对指定仓库进行代码回退、合并，比如frameworks/base。如果不带此参数，表示要对整个大系统进行代码回退、合并；
   #     -b <new-branch>，此参数的含义是新建一个分支，并指向固定点；
   #     -i <small-system-rootdir> 表示小系统路径（小系统根目录）；
   #     --copy-only  表示只是将项目定制代码拷贝到大系统，不会checkout到历史节。
   ```

   ***

2. ***repo diff*** 将修改完成的代码再合并到小系统

   项目问题修改完成后，如果项目固定了发布点，就必须把修改的代码传到小系统上。其他情况，要根据本规范第二节的规定，决定代码是否需要上传到系统。使用repo diff命令把修改完的代码合并到小系统：


     ~~~
   repo diff [<project>...]  -o <small-system-rootdir>
   # 参数介绍：
   #	project 同repo merge；
   #	-o <small-system-rootdir> 小系统根目录的路径；
     ~~~

   ***

3. ***repo merge 和 repo diff*** 使用介绍

   repo merge和repo diff两个命令依赖于大系统仓库根目录下的.repo/repo里面的代码。如果这个仓库代码不是最新的，则很可能无法执行这两个命令，需要pull一下代码。

   使用前需要确保小系统是项目最新状态。方法有两个：

   - 如果没有项目小系统，使用repo下载，则代码必然是最新的；

   - 如果项目小系统已经有了，则首先到小系统根目录下的 ***.repo/manifests*** 目录下，确保分支正确，并使用 git pull 命令更新一下这个目录。然后到项目小系统目录下，执行 repo sync 命令（执行 repo sync 命令是要注意是否有报错）。

     ***

4. 去掉已经 merge 的项目代码

   当merge的项目定制代码不再需要时，可以使用如下命令回退掉

   ~~~
   repo init -m default.xml
   repo forall -c 'pwd && git clean -df && git checkout -- . && git checkout develop'
   ~~~

   


### **如何确定项目是否固定了发布点**

到项目小系统根目录下的.repo/manifests目录，首先使用git branch命令确定当前分支是否是项目分支，并确保当前目录是否是最新状态（可以使用git pull命令更新一下）。然后打开default.xml。找到**platform/release **和 **platform/release_user** 两行（有的项目可能只有一个）。

- 如果revision的值是master，则表示没有固定发布点。

- 下面这种情况，则表示固定了发布点：

  ```
  <project path="platform/release" name="hisilicon/hisi-3798M-spc060-kk-release" remote="platform" revision="740d4933a5162043fa947c72a8a7ed98d0949c06" />
  <project path="platform/release_user" name="hisilicon/hisi-3798M-spc060-kk-release-user" remote="platform" revision="dc938c1e104f6ba21ba5879674a6947809fb4dca" />
  ```

### ReleaseNotes

大系统（如Android SDK和Linux SDK等）修改代码需要书写ReleaseNotes，ReleaseNotes有如下用途：

- 发布基线版本时，需要同步提供ReleaseNotes给项目部同事；
- 大系统一般都是多个git仓库组成（有的多大几十个），通过ReleaseNotes能够快速查询大系统的所有修改，而不需要挨个仓库去查找；

ReleaseNotes书写方法：

1. 修改代码并提交；

2. 在大系统的任意目录执行"

   repo note

   "命令，然后按照命令中的模板进行填写：

   ```
   132. 问题概述:
       责任人: 
       修改时间: 2018-01-31 11:33:18
       详细描述:
       修改文件及其仓库commit ID:
       更新的库或可执行文件:
       项目名称:
       影响范围:
       测试建议:
   ```

3. 提交***ReleaseNotes***，执行"***repo note push***"命令即可：


```
# -r 参数表示远程仓库名称，如果没有该参数，则默认为sunniwell
# -b 参数表示分支名称，如果没有该参数，则默认为develop
repo note push [-r remote] [-b branch]
```
