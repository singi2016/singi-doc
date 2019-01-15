# git

## 如果git时输错密码，导致clone不下来

`WINDOWS`：打开`凭证管理器`找到对应账号密码修改再试即可

## 查看某几次提交的文件变动

> `HEAD`表示当前提交  
> `HEAD~1`表示倒数第1次提交  
> `HEAD~3`表示倒数第3次提交
>
> 列出倒数第1次提交到最新1次提交的文件变动

```
git diff --name-status $(git rev-parse HEAD) $(git rev-parse HEAD~1)
```

## 打包某两次提交的代码

> 打包倒数第1次提交到最新1次提交的代码

```
git archive -o ./latest-$(git rev-parse --short HEAD)-$(git rev-parse --short HEAD~1).zip $(git rev-parse HEAD) $(git diff --name-only $(git rev-parse HEAD) $(git rev-parse HEAD~1) --diff-filter=d)
```

### 方法1

```
git diff --name-only oldcommitID lastcommitID| xargs tar -jcvf filename.tar.zip
```

### 方法2

```
git archive -o ./latest-$(git rev-parse --short HEAD~3)-$(git rev-parse --short HEAD).zip $(git rev-parse HEAD~3) $(git diff --name-only $(git rev-parse HEAD~3) $(git rev-parse HEAD) --diff-filter=d )
```

## 本地仓库关联远程仓库

```
git remote add origin repository
git push -u origin master
```

> 如果更新时提示,`fatal: refusing to merge unrelated histories`,则执行`git pull origin master --allow-unrelated-histories`

## 忽略本地已经追踪了的文件

```
git update-index --assume-unchanged filename //忽略文件
git update-index --no-assume-unchanged filename //恢复记录忽略的文件
```

## 移除已经追踪了的文件

    1. git rm -rf --cached filename //不再追踪
    2. filename commit -m "rm" //提交修改到本地,filename此时变成`untracked`
    3. 将需要忽略的文件添加到.gitignore文件中

> 这些文件需要重新 git add filename 才能被再次追踪

### 克隆一个新项目

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



