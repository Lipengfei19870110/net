Git is a version control system.
Git IS free software.
This txt is test code.
Lipengfei wanna to reasch python and Resnet.
存放在当前git工作区（即net文件夹下，只有文件建立在net文件夹下或其子目录下才可以提交git）的文件，
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