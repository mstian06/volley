# README

## Git使用_远程
[Git远程操作详解_阮一峰！](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)</p>
> git clone</p>
> git remote git remote命令列出所有远程主机。
> 使用-v选项，可以参看远程主机的网址。</p>
> git fetch 默认情况下，git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。</p>
> git pull git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。</p>
> git push git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。</p>

[github的多人协作](https://gist.github.com/suziewong/4378619)</p>
git branch -vv（两个v），就能够看到本地分支跟踪的远程分支。 </p>
你是想知道跟踪分支的对应关系吧？使用git config --list查看branch的设置就知道了。</p>
[git是如何知道本地分支与远程分支的跟踪关联关系的?](http://herry2013git.blog.163.com/blog/static/219568011201341192418644/)

### 理解
比如.git/config如下:

	[core]
		repositoryformatversion = 0
		filemode = false
		bare = false
		logallrefupdates = true
		symlinks = false
		ignorecase = true
		hideDotFiles = dotGitOnly
	[remote "origin"]
		url = https://github.com/mstian06/volley
		fetch = +refs/heads/*:refs/remotes/origin/*
		puttykeyfile = 
	[branch "master"]
		remote = origin
		merge = refs/heads/master
	[remote "official"]
		url = https://android.googlesource.com/platform/frameworks/volley
		fetch = +refs/heads/*:refs/remotes/official/*
	[branch "master_official"]
		remote = official
		merge = refs/heads/master
	[branch "dev_mstian"]
		remote = origin
		merge = refs/heads/dev_mstian


说明：

	remote：表示远程主机地址
	branch：表示本地分支跟踪远程分支的地址。
	因为volley不是从github中fork下来的，导致config中没有official的远程主机标示（是自己拉取到本地建立的）。
	使用git remote add official https://android.googlesource.com/platform/frameworks/volley 添加远程主机（从github库fork默认会有对原库的一条remote）
	使用git fetch official 拉取远程主机的远程分支
	使用git branch master_official official/master建立跟踪（或者git branch --set-upstream master_official official/master）
	
	**official volley更新了，如何合并最新的代码？**
	方法1：
	在本地master分支，git fetch official；
	git checkout -b newBrach official/master
	git merge origin/master或者git rebase origin/master
	方法2：
	git pull <远程主机名> <远程分支名>:<本地分支名>//将远程分支合并到本地分支
	git pull official master:master
	**最后**在push到github上的库中。

## volley