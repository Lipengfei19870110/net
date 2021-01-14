Git is a version control system.
Git IS free software.
This txt is test code.
Lipengfei wanna to reasch python and Resnet.
首先在想建立本地库的位置,在git bush中使用cd d:/git到git文件夹下，mkdir net，建立本地库文件夹net
并git init执行初始化命令。
使用全局设置命令git config --global user.name=Lipengfei ；git config --global user.email=303365961@qq.com
存放在当前git工作区（即net文件夹下，只有文件建立在net文件夹下或其子目录下才可以提交git，在建立的net
文件夹内先执行git init生成.int文件）的文件，
由git add 命令提交到暂存区stage，然后由命令git commit -m “版本说明”提交到指定分支下
（默认为master分支）。多次提交会在该分支下形成一个时间线将各个版本按先后顺序串起来，
当你想退回某个版本是，使用命令git reset --hard HEAD~n（HEAD代表该分支下不同版本时间线上的指针，
数字1代表当前版本之前的第n个版本）即可回退。
git log 可显示所有从近到远所提交的所有版本信息，包括SHA1（安全哈希序列算法加密）生成的版本号。
利用该版本号使用命令git reset --hard 版本号  可直接回到该版本。git reflog 可显示所有使用过的命令，
方便查看每个版本的SHA1序列号。git status 可以查看工作区内所有文件的修改情况，提交过的发生修改显示
为Changes not staged for commit（文件未暂存）并给出提示命令,未提交的显示为Untracked files. 使用add命令后在git status
会发现Change to be commited 表明都在文件都添加到暂存区stage等待提交。
使用git diff HEAD -- readme.txt可查看该文件在工作区和版本库里的版本区别。
当你add后（版本1）对文件又修改后（形成版本2）没有继续add而是commit了，那么暂存区提交的是版本1而不是
后形成的版本2.
版本1
版本2
使用git chectout -- readme.txt命令（注意--两边的空格）可以撤销工作区内的文档修改。在没有add到暂存区内
如果已经add到暂存区了，但是还没有commit提交到远程仓库，可以先git reset HEAD~1撤先回到工作区，在使
用checkout命令撤销更改。
建立远程仓库与本地仓库的链接，先注册github账号，然后在本地git bash中切换到当前git目录（NET文件夹内）
并确认以执行git init命令，然后使用命令shh-keygen -t rsa -C "303365961@qq.com"。一路回车生成SHA1加密的
密匙，包括私用密匙id——rsa和公用密匙id_rsa.pub，均存放于C:/users/Lipengfei/.shh文件夹内。
然后登陆github，打开右上角Account settings，找到左边的SSH Keys，打开页面点Add SHH Keys,tittle随便写，
Key文本框里粘贴id_rsa.pub文件里的内容，点击add key就可以了。
提前在github里建立了net远程仓库
然后在git bash里使用命令git remote add netorigin git@github.com:Lipengfei19870110/net.git将本地仓库
关联到net远程仓库。命令中netorigin表示远程仓库名（这是自己设定的，系统通常默认的名字为origin）
Lipengfei19870110为本人github账户名
分支master的关联
下一步就可以使用git push -u netorigin marster推送本地库内容到远程库。第一次推送master分支时加上 
-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的
master分支关联起来，在以后的推送或者拉取时就可以简化命令。第一次push或clone链接远程库会受到警告，
一路yes就行了，主要是确认Key信息是否一致及添加到github信任列表里。
克隆远程库
使用git clone git@github.com:Lipengfei19870110/net.git将远程库克隆到本地库。提前在本地建好文件夹
创建新的分支，git switch -c dev，会自动切换到dev分支去。git branch可以查看所有的分支，带*的是目前
所在的分支，然后就可以将新的修改提交到dev分支了。以后所有的新更改都在dev分支里，master就没有了。
但是可以将两者合并，切换到master分支后git merge dev，会将dev分支的内容合并到master去。 然后可以
使用git branch -d dev删除dev分支。
在master分支使用--no-ff参数合并分支为普通模式，合并后历史有分支能看出来曾经做过合并，而直接
git merge命令则采用fast forward模式合并，合并后看不出来曾经做过合并。
git merge --no-ff -m "此处使用-m添加commit提交说明只是为了将来使用git log --graph --prettyoneline
 --abbrev-commit 命令时能查看到分支历史" bb
 bb为新建的分支。上面两行的意思是采用普通模式将bb分支合并到master分支，保留合并历史信息。
 通常都在新建分支上进行推送，下拉。master分支一般不开发代码，只在发布新版本时推送。下面进行分布式
 开发时以新建分支（比如bb）为主，围绕他进行合并，下拉及推送。
 
 ########bug修复时的git应用模式
 1.假设我们目前在bb分支干活，首先保存当前分支内的工作内容（特别是没有完成时无法提交时），使用命令
 git stash将当前工作现场“储藏”起来，这样工作区就干净了，可以放心的创建分支去修复bug
 2.确定要在哪个分支上修复bug，切换到该分支创建新的bug分支，以master分支为例
 git switch master 切换到master分支
 git switch -c bugfix001 建立该分支的bug修复分支，对文件进行修改，然后切换到master分支进行合并，然后
 删除bug修复分支 Git branch -d bugfix001
 3.切换到bb分支接着干活，需要先把“储藏”起来的工作内容恢复过来，使用git stash list可查看所有储藏的工作
 内容，使用git stash apply stash@{0} 恢复指定的stash，这里的{0}是当前最近的一个stash。这个命令不会删除
 stash,也可以用git stash pop 命令，在恢复工作内容的同时将stash删除了，不推荐使用这个方法，建立保留每次
 的stash。
 4.我们修复了master分支的bug，那么基于master分支建立的bb分支肯定也存在这个bug。我们只需要将修复bug的那
 个commit提交的修改复制到bb分支就行（只是复制提交的修改不是复制整个master分支）。
 使用cherry-pick （commit版本号） 将复制一个特定的提交到当前分支。并自动在当前分支再提交一次，会从新获得
 一个新的commit编号，与复制之前的编号不一样
 修复了吗？
=======
 修复bug

>>>>>>> bb
=======
为了试验推送分支bb到远程仓库
为了试验rebase,先提交一次。
在修改一次，再提交一次。
git rebse -i 可将本地多次提交版本合并为1个，简化提交历史，避免合并到主分支时可能发生多次的解决冲突
>>>>>>> bb

########标签使用
使用命令git tag -a 标签名字 -m "标签解释"可以快速建立标签，要注意的是标签是和commit挂钩的，如果想指
定给某一个commit打标签，可以先用git log --graph --pretty=oneline --abbrev-commit找到该历史commit，然
后使用git tag -a 标签名字 -m "标签解释" commit历史版本号 ，可以打上标签。
使用git tag 可以列出所有标签，git show <tagname>可以显示该标签详细信息。
如果标签打错了可以使用git tag -d v0.1这种方法删除标签，通常标签是存储在本地，不会自动推送到远程。
推送标签到远程库git push netorigin <tagname>；一次性推送多个本地标签，使用git push netorigin --tags
删除远程标签git push netorigin :refs/tags/v0.1。注意命令中netorigin是自己的远程库名，另注意空格。
########使用github
 查看别人的库，认为比较好，直接点fork，就相当于克隆到自己的远程库里，然后再pull或者克隆
下来到自己的当地库（推荐克隆），就完成了对别人代码的下载，并具有了推送权限。
########国内github托管
----gitee,使用与github类似。1个本地库可以同时关联github和gitee，但是注意2个不同平台上
的远程库不要一样。比如在github上叫netorigin，在gitee上可以叫gnetorigin。
关联命令 git remote add gitte@gitee.com:Lipengfei19870110（gitee账户名）/gnetorigin.git；
git remote -v 查看关联；git remote rm 远程库名，可以删除该关联；git push gitee master 推送到gitee上
########自定义git(配置别名) 
git config --global alias.st status。该命令表示，将git status（查询状态）命令自定义为git st(别名).
那么以后可以直接使用git st 代替git status，简化了命令。
git config --global alias.lg log --color--graph --pretty=oneline --abbrev-commit  --date=relative --author=Lipengfei"后，
git lg就等于这一串命令，也可以参考网上别人配置好的更复杂的命令。
git config --global alias.lg "log --color --graph --pretty=format:'%C(yellow)%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
git config --global alias.br branch;git config --global alias.ck checkout;git config --global alias.rt remote
git config --global alias.last 'log -1';git config --global alias.unstage 'reset HEAD';
同时需要明确，--global指配置对当前用户生效，--system指配置对所有用户生效。
每个仓库的配置文件都放在该本地库的.git/config文件中[alias]字段下面。可直接添加。
如果你传递参数选项’–-system’ 给 git config，它将明确的读和写这个文件。且对所有用户生效。
未指定--system或--global则只对当前仓库生效。
git config --system user.name "lipengfei"  
git config --system user.email "303365961@qq.com" 
指定 --global 的时候，会对当前用户生效。
每个用户的配置文件在C盘:用户/Lipengfei/.gitconfig文件中[alias]字段下，可以直接添加；

#*#*#*#*#*#*#*#*#*#----全局用户配置内容
[user]
	name = LiPengFei
	email = 303365961@qq.com
[alias]
	st = status
    lg = "log --color --graph --pretty=format:'%C(yellow)%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
    br = branch
    cm = commit
    cl = clone
    ck = checkout
    cp = cherry-pick
    cfg = config
    df = diff
    fh = fetch
	sh = stash
	mg = merge
	pl = pull
	ps = push
	rt = remote
	rs = reset
	sw = show
#*#*#*#*#*#*#*#*#*#
