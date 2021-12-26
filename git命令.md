## 基本命令

git init   //将目录变成Git可以管理的仓库

Git add   xxx.xxx      //将xxx文件添加到仓库

git commit -m "this is test"     //将文件提交到仓库  -m""是添加说明

Git添加文件可以一次性添加很多

例如

```
git add file.txt
git add file2.txt file3.txt
git commit -m "add 3 file"
//不要被add 3 file迷惑，只是说明，提交仓库只有一个命令那就是git commit
```

git status   //查看仓库状态

git diff 文件名    //查看文件修改了什么



版本回顾

查看历史记录 git log

嫌弃数据太多可以加--pretty=oneline参数

git log --pretty=oneline

```
9d0915ed5923a16cc0bf9fbad7ac1cf63ea37738 (HEAD -> master) this is a test
433c93595a4e05d8ee07c27ec0adeb187739f99e this is test
d188b87161f4508396e3697f692fbf0a68845242 this is test
```

注：此处是commit的版本号，并不是递增的1,2,3,4而是SHA1计算出的数字，16进制

回溯要知道回到哪里

首先，git要知道自己什么什么版本，当前版本用head表示，上一个是head^，上上一个是head^^

或者head~n

git reset    时光回溯

例子

```
git reset --hard head^            //回到上一个版本
```

**hard参数****：**

再使用git log查看历史版本

发现无上一个版本了，当然如果穿梭返回了 也是可以返回的，但是需要几下历史记录的commit版本号，也就是一长短sha值，只需要输入前几位，会自动找

git reset --hard d188b

介绍一下原理：

```ascii
┌────┐
│HEAD│
└────┘
   │
   └──> ○ append GPL
        │
        ○ add distributed
        │
        ○ wrote a readme file
```

git 是指针指向版本，回退版本时：

```ascii
┌────┐
│HEAD│
└────┘
   │
   │    ○ append GPL
   │    │
   └──> ○ add distributed
        │
        ○ wrote a readme file
```

git提供了记录命令的命令 git reflog



## 工作区

就是在电脑里能看到的目录

之前说过 git init可以创建版本库

普通目录都是工作区

工作区隐藏的目录.git 不算工作区，而是git的版本库



Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。



![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)





- **工作区：**就是你在电脑里能看到的目录。
- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。
- 

***git diff：当工作区有改动，暂存区为空（即***已经add 并 commit*)，diff对比的是“工作区与最后一次commit提交的仓库的共同文件”；当工作区有改动，暂存区不为空（即*已经add但还未commit** *)，diff对比的是“工作区与暂存区的共同文件”。***



：



