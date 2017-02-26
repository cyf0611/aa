##**git常见命令**
- `pwd（print working directory）` 打印出当前路径
- `cd（change directory）`改变路径
- `ls(list files) `
    + ls  列出当前目录文件
    + `ls 目录路径`列出指定路径文件
    + `ls -a` 列出文件并显示隐藏文件或目录
-`cp(copy)`
    + cp  在复制目录的时候，不会复制里面的子文件或子目录
    + -r 递归复制
- `mv(move)`移动文件或者目录，还可以重命名文件或目录
- `mkdir（make directory）` 创建目录
- `rm（remove）` 删除文件或目录
   + `-rf`递归删除：直接将整个目录包括里面的内容都删掉
- `rmdir` 目录名称
   + **只能删除空的目录**
- `clear` 清屏
- `touch` 根据文件名创建新的文件
- `cat` 查看指定的文本文件

----
##**安装和配置 Git 环境**##
**Git管理的4种状态**
	- 未追踪（untracked）
	- 已提交（committed）
	- 已修改（modified）
	- 已暂存（staged）

---

##**安装和配置 Git 环境**##
####1. **确认是否有 git 环境：**
```
$ git --veson
```
如果看到能输出一个版本号 `git version 2.10.1.windows.1（版本不一定一致）`，说明没有问题。
br
####2. **初始设置：**
```
$ git config --global user.name "yourname"
$ git config --global user.email "your_email@example.com"
br
```
####3. **基本操作：**
- `git init`
   + 通过该命令创建一个本地仓库
   + 执行过后，会在目录下生成一个 `.git` 隐藏目录，最好不要手动修改
- `git status`
	+ 查看当前工作树状态
	+ 例如有新增的文件、修改的、删除的、等操作没有被添加到暂存区或者没有被提交
	+ 都可以通过 git status 命令看到
- `git add 文件名`
	 + 将制定的文件添加到暂存区（待提交列表）
- `git commit -m "提交日志"`
	+ 将暂存区（待提交列表）中的文件提交到本地仓库，形成一个历史快照
- `git log`
	+ 查看提交日志
- `git log --oneline` 与`git log`区别是不显示提交人信息，将提交记录显示出来
####4. **更改提交的操作：**
指定文件回滚：
- `git checkout [file]`恢复暂存区的指定文件到工作区
- `git checkout [commit] [file]`恢复某个commit的指定文件到暂存区和工作区
- `git checkout .` 恢复暂存区的所有文件到工作区

br
指定版本回滚：
- `git reset --hard`恢复暂存区和工作区到上一次最新的提交
- `git reset --hard 提交哈希值`根据提交哈希值（版本号）回溯到历史版本
- `git reflog`将操作记录和对应的编码显示出来

---
####5. **推送至远程仓库：**
如果已经有了一个本地仓库，就可以通过下面的形式和线上的空仓库产生关联：
- `git remote add origin `远程仓库地址(git 会自动将远程仓库地址起个别名 origin)

----
####6. **gitignore忽略文件：**
在项目根目录下创建一个.gitignore文件，可以将不希望提交的罗列在这个文件里，如项目的配置文件node_modules等

----
####7. **分支操作：**
- `git branch` 查看分支
- `git branch“分支名称”` 创建一个新的分支
- `git checkout“分支名称”`切换分支
- `git merge“分支名称”`合并分支
- `git branch -d “分支名称”` 删除分支

----
####8. **使用vi/vim编辑器：**
- 打开/创建文件， vi 文件路径
	+ **底行模式** 
		* :w保存，:w filenme另存为
		* :q退出
		*  :wq保存并退出
		* :e! 撤销更改，返回到上一次保存的状态
		* :q! 不保存强制退出
		* :set nu 设置行号
	+ **命令模式**
		* esc 切换到底行模式
		* u辙销操作，可多次使用
		* i进入编辑模式，当前光标处插入
		* a进入编辑模式，当前光标后插入

----
####9. **SSH：**
- 常见有两种加密技术，分别是对称性加密和非对称性加密，SSH属于后者。
- ssh-keygen -t rsa会创建公钥和密钥（默认在用户目录/.ssh目录下）
- ssh-copy-id user@host添加到对应远程主机的用户目录/.ssh目录下
- 也可以登录远程主机，进入到用户目录/.ssh目录下手动创建authorized_keys文件，并将自已的公钥粘入该文件。
- 进入git-bash验证是否添加成功：ssh -T git@github.com
---
####10. **每次push的时候都需要输入账号密码的解决方法：**
进入%HOME%目录，一般是`C:\Users\Administrator`，新建一个名为"_netrc"的文件，文件中内容格式如下：
```
machine github.com
login your-usernmae
password your-password
```