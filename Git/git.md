#### 撤销commit

取消commit:  git reset --soft HEAD^

撤销add:  git reset HEAD

 1、误add单个文件 git reset HEAD 将file退回到unstage区 2、误add多个文件，只撤销部分文件 git reset HEAD 将file退回到unstage区

git rm 与 git reset的区别 git rm：用于从工作区和索引中删除文件 git reset：用于将当前HEAD复位到指定状态。一般用于撤消之前的一些操作(如：git add,git commit等)。

git rm file_path 删除暂存区和分支上的文件，同时工作区也不需要 git rm --cached file_path 删除暂存区或分支上的文件, 但工作区需要使用, 只是不希望被版本控制（适用于已经被git add,但是又想撤销的情况） git reset HEAD 回退暂存区里的文件

#### 暂存栈

git add .   (把所有改动暂存)

git stash   (把暂存的文件提交到git的暂存栈)

git checkout 本该提交代码的分支 

git stash pop (将暂存栈中的代码放出来)

#### 取消文件跟踪

git rm -r --cached {dirname} // 不删除本地文件

git rm -r --f {dirname} // 删除本地文件

#### 查看地址

```
git remote -v
```

​    video_review_1： 2

### pull远程分支

```
git fetch origin 分支名称
```

```
切换至个人分支
git pull --rebase origin master
解决冲突后
git rebase --continue
再
git pull --rebase origin master
然后合并到 master
```

### 合并commit

```git
git rebase -i {commit_id}  # 最早的commit
// 进入编辑界面，将需要保留的commit 设置 p，不需要保留的设置为s
git rebase --continue  # 完成合并
```
