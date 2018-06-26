# git

## 本地仓库关联远程仓库

```
git remote add origin repository
git push -u origin master
```

> 如果更新时提示,`fatal: refusing to merge unrelated histories`,则执行`git pull origin master --allow-unrelated-histories`


## 忽略本地已经追踪了的文件

```
git update-index –assume-unchanged filename //忽略文件
git update-index –no-assume-unchanged filename //恢复记录忽略的文件
```

## 移除已经追踪了的文件

```
1. git rm –cached filename //不再追踪
2. filename commit -m “filename文件以后都不会被记录到git中” //提交修改到本地git,filename此时变成 untracked,可以被添加到.gitignore文件中被忽略
3. 将需要忽略的文件添加到.gitignore文件中
```
> 这些文件需要重新 git add filename 才能被再次追踪

###克隆一个新项目
```
git clone https://github.com/singi2016cn/webpack-start.git
```

### 查看所有分支
```
git branch -a
```

### 从远端新建本地分支并切换过去
```
git checkout -b branch origin/branch
```

### 添加文件或目录到暂存区
```
git add <file>
```
### 取消已添加到暂存区的文件或目录
```
git checkout -- <file>
```

### 提交添加的文件到本地仓库
```
git commit -m <message>
```

### 取消commit到本地仓库
```
git rm <file>
```

### 提交本地仓库的文件到远端仓库
```
git push
```
### 更新远端仓库到本地
```
git pull
```
