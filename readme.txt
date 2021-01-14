Git is a version control system.
Git IS free software.
This txt is test code.
Lipengfei wanna to reasch python and Resnet.
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