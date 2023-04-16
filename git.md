# 1.简介

免费开源的代码管理工具

功能：

- 在不同版本之间切换
- 对代码维护
- 被多人修改时处理代码冲突
- 远程仓库
- 创建代码分支，独立的代码记录，不会对其他分支产生影响

# 2.配置git

设置名字：`git config --global user.name "  "`

设置邮箱：`git config --global user.email " "`

查看目录状态：`git status`

初始化：`git init`

查看日志：`git log`

`git add *`表示将所有未跟踪的文件暂存

## 1.文件状态

- 未跟踪：git没有管理     
- 已跟踪：git管理             
  - 暂存：已经保存，但没有提交到git
  - 未修改：磁盘中的文件与git仓库中文件相同
  - 已修改：磁盘中的文件与git仓库中文件不同

1. 创建文件`1.txt`
2. `git status`返回`untractked files`（未跟踪）
3. 将文件暂存`git add <file name>`
4. `git status`返回`changes to be committed`（暂存）
5. 将暂存文件提交到git仓库`git commit `

****

`git commit -m " "`字符串中用来描述提交文件的信息

****

6. `git status`返回`nothing to commit`（未修改）
7. 修改文件`1.txt`
8. `git status`返回`modified`（已修改）

****

如果要将修改过的文件提交到git仓库中，需要再次`git add <file name>`

`git commit`                        

****

## 2.常用命令

暂存所有文件`git add *` 

暂存以js为后缀的所有文件`git add *.js`

### 1.重置文件

```
git restore <file name>                重置文件
git restore --staged <file name>       将文件从暂存状态取消
```

### 2.删除文件

```
`git rm <file name>    删除文件（当文件是已修改状态不可以删除）
git rm <file name> -f  强制删除
```

### 3.重命名

```
git mv <file name> <file name>
```

# 3.分支

查看提交日志`git log`

## 1.merge

每次提交都会创建一个节点，git会创建一个树状结构。通常只会有一个分支`master`，可以创建多个分支，分支与分支之间相互独立。

```
git branch                    查看分支
git branch <branch name>	  创建分支
git branch -d <branch name>   删除分支
git switch <branch name>      切换分支
git switch -c <branch name>   创建并切换分支
```

开发过程中，在自己的分支中修改bug，将修改bug的分支与主分支合并

```
git switch master          切换到主分支
git merge <branch name>	   将分支合并到主分支
git branch -d <branch name>将被合并的分支删除
```

## 2.变基（rebase）

使用merge合并的时候，当项目周期较长，合并记录太多，不方便查看

1. 先找到两条分支最近的公共祖先
2. 对比当前分支对于祖先的历史提交，并提取出来存储到一个临时文件中
3. 将当前部分指向目标的基底
4. 以当前基底开始执行

```
git switch 待改变的基
git rebase 主分支
```

当提交到远程仓库，最好用merge

# 4.远程仓库

## 1.上传

将本地库上传到github

```
git init//初始化代码仓库

git remote add <remote name> <url>//关联到远程仓库
git branch -M main//修改为main

git add <file name>//将文件暂存
git commit -m "提交信息"//将文件提交，提交信息必须要写

git push -u <remote name> main //将文件提交到仓库
```

`<remote name>`表示远程库的名字

## 2.下载

打开code，复制网站

在文件夹中输入命令行`git clone <url>`

## 3.操作

```
git remote     显示当前关联的远程库
git remote add <remote name> <url>  关联远程仓库  用名字指向网页链接
git remote remove <remote name>   将关联的远程库删除
git push -u <remote name> <branch name>  向远程仓库推送代码，并于分支关联
git push -u <remote name> <branch name>:<branch child name>  将远程仓库中的子分支推送代码
当修改完该文件的时候，由于已经关联，只需要git push即可
```



`git clone <url> <file name>`指定克隆到某个文件夹内



如果本地库的版本低于远程库的版本，push不上去

- fetch   向关联的库下载所有代码，但不会将代码和当前的分支自动合并

  所以还要手动合并代码 git merge origin/master  将当前分支与远程库master合并

- pull     从服务器上拉取代码，自动合并

## 4.gitignore

默认情况下，git会监视项目中的所有内容，但有些内容比如node_modules，不希望被监视。可以在项目中添加`.gitignore`文件

```
在.gitignore文件中写
node_module         忽略node_module文件夹中所有内容
yarn.lock           忽略yarn.lock文件
*.log               忽略所有以log为后缀的文件
```

****

使用GitHub的域名部署$\textcolor{red}{静态网页}$，分支名必须为$\textcolor{red}{gh-pages}$

在setting中，左侧pages中查看路径。仓库的名字修改为

`用户名.github.io`

****

# 3.标签

切换节点      `git switch <id> --detach`      id只需要写前几个字母就行

****

id通过`git log`查看

****

头指针：指向当前页面显示的代码对应的节点的指针

当头指针没有指向某个分支的节点的时候，这种状态称为分离头指针。分离头指针的情况下也可以操作代码，但这些修改不会出现再任何分支上

假如要修改的话，必须要先创建分支`git swtich -c <branch name> <id>`

给每个提交记录设置一个标签，设置标签后，可以通过标签快速切换不同的节点

设置标签：

```
git tag <tag name>//当前节点的标签设置为<tag name>
git tag <tag name> <id>//给指定节点设置<tag name>
```

切换节点就可以写成`git switch <tag name>`

```
git push <remote name> <tag name>将指定节点推送到仓库
git push <remote name> --tags   推送所有标签
git tag -d <tag name>   删除本地指定标签
git remote <remote name> --delete <tag name> 删除仓库指定标签
```

