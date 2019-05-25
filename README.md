### 1.命令部分
#### 一、git clone <url版本库>   表示克隆库上代码的所有部分,且默认创建一个origin库和		master主分支
#### 二、git remote add <xxx名字>  <url自己库>    表示给库关联一个名字
#### 三、git pull <origin库>  <master主分支> 
#### 四、git pull <origin库>  <master分支>：<本地分支hbs>   表示取回origin主机的master		分支，与本地的hbs分支合并
#### 五、git pull <origin库>  <master分支>   表示取回origin主机的master分支，与本地		的当前分支合并
#### 六、git push 同理
#### 七、git checkout <文件名或者一个点>   表示撤销当前文件或者所有文件的修改

### 2.提交代码部分
#### 一、NO1
##### (1):修改代码后、git stash  把修改的内容放入缓存区
##### (2):git pull <origin库>  <xxx当前分支>  --rebase   拉取库上最新的代码与本地		##### 合并
##### (3):如果有冲突，解决冲突。完成过后，git add . 然后 git rebase --continue
##### (4):git stash pop 取出缓存区修改的内容
##### (5):git commit -m “描述信息”
##### (6):git push <hbs库>  <xxx当前分支>
#### 二、NO2
##### (1):把本地修改完成的代码备份出来
##### (2):git fetch <origin库>    拉取库上最新的代码
##### (3):git checkout -b xxx --track remotes/origin/master 拉取库上master分支最新的代码到 xxx分支
##### (4):把备份的代码修改进当前分支
##### (5):git add 然后 git commit 再 git push 

### 3.其他部分
#### 一、合并两个连续的commit
##### (1):git log查看需要合并的两个commit是否是最新的两个commit，是则往下
##### (2):git rebase -i HEAD~2  2表示两个，当然也可以是很多个，但必须是连续的。或者此处可以使用git rebase -i <commit号>。
##### (3):进去操作界面。按 i 键编辑,保留一个pick,其他的修改为s。然后按 Esc键，再输入 :wq 保存退出。
##### (4)git push <hbs库> <当前分支> -f 强推一下
#### 二、合并两个不连续的commit
##### (1):git log 查看需要合并的两个commit号
##### (2):git fetch <origin库>
##### (3):git checkout -b <xxx> --track remotes/origin/master 
##### (4):git cherry-pick <最开始提交的commit号>
##### (5):git status查看，如果有红色内容、表示有冲突，需要修改冲突，然后git add . 。按照提示，git cherry-pick --continue
##### (6):git cherry-pick <最后提交的commit号> 再走一遍流程
##### (7)走完后，git log 查看两个commit是否出现再最新的位置。
##### (8):然后再进行合并两个连续的commit的操作
#### 三、修改commit信息
##### (1):查看需要修改的commit是否是最新的，不是则需要reset
##### (2):git commit --amend
##### (3):修改完后git push.

