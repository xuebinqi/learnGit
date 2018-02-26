git学习中的相关命令及问题：
一：git的安装及配置：
    在 https://git-scm.com/ 网址中就可以下载git，有各种版本的，自行下载即可；
    安装完成后，找到Git Bash，打开Git Bash，安装完成后，还需要进行设置，在命令行输入：
        $ git config --global user.name "Your Name"
        $ git config --global user.email "email@example.com"
    在这里"Your Name"是你自己定义的用户名，"email@example.com"是你自己的邮箱号。
二：创建版本库
    1. 创建版本库：
        和Ubuntu下命令行一样，用mkdir创建一个目录，用 cd 进入创建的版本库。
        pwd 用来显示当前所在的版本库所在的目录。
        通过命令git init,就可以把这个目录变成Git可以管理的仓库；
    2：向版本库中添加文件：
        首先自己新创建一个文件，比如readMe.txt, 放到我们创建的目录下，
        第一步，用命令git add告诉Git，把文件添加到仓库：
            $ git add readMe.txt
        执行该命令后，没有任何提示，表示添加成功，
        第二步，用命令git commit告诉Git，把文件提交到仓库：
            $ git commit -m "wrote a readMe file"
            -m表示后面输入的是本次提交的说明：
三：常用的命令：
    1：$ git status
        git status命令可以让我们时刻掌握仓库当前的状态，
    2：$ git diff readMe.txt 
        git diff用来查看我们修改前后的文件有那些不同；
        如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
    3：$ git log
        git log命令显示从最近到最远的提交日志;如果嫌输出信息太多，
        看得眼花缭乱的，可以试试加上--pretty=oneline参数：
    4：$ git log --pretty=oneline
        在Git中，用HEAD表示当前版本，也就是最新的提交
    5：$ git reset --hard HEAD^
        表示回退到上一个版本。
    总之，就是让这个文件回到最近一次git commit或git add时的状态。    
    6：$ git reflog
        git reflog查看命令历史，以便确定要回到未来的哪个版本。
    7：$ git checkout -- readme.txt
        命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的
        修改全部撤销，这里有两种情况：
        一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
        一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
    8：$ git reset HEAD file    
        git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区：
    9：$ rm file:
        表示删除文件：
        如果确定要删除file文件，则用git rm file这个命令，并且用git commit命令
        如果删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
        用 git checkout -- file来恢复。
四: 几个概念的区分：
    1：工作区（Working Directory）：
        就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：
    2：版本库（Repository）：
        工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
        工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
         Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，
        还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
    3：我们把文件往Git版本库里添加的时候，是分两步执行的：
        第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
        第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
        因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，
        所以，现在，git commit就是往master分支上提交更改。
        可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
五：添加远程仓库（GitHub）：
    1：在连接GitHub之前，需要以下操作：
        第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，
        如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
        命令：$ ssh-keygen -t rsa -C "youremail@example.com"，然后一路回车即可：
        如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，
        id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
        第2步：注册及登陆GitHub，点击账户头像，点击设置（settings），找到“SSH and GPG keys”选项，点击，
        到“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：
        点“Add Key”，你就应该看到已经添加的Key：
    2：现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，
        这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。
        登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：
        在Repository name填入learngit（这里名称自己随意选择），其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：
        现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：
六：本地仓库同步到GitHub：
    1：$ git remote add origin git@github.com:xuebinqi/learngit.git
        把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
    2：$ git push origin master
        由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
        还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
    3：注意：
        当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：
        只需要输入yes即可。
        如果输入$ git remote add origin git@github.com:djqiang（github帐号名）/gitdemo（项目名）.git 
        提示出错信息：fatal: remote origin already exists. 
        解决办法如下：
            1、先输入$ git remote rm origin 
            2、再输入$ git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了！
七：GitHub仓库克隆到本地仓库：
    $ git clone git@github.com:xuebinqi/gitskills.git
        表示将我的gith仓库中的gitskills文件夹克隆到Git本地仓库。
        git@github.com:xuebinqi/gitskills.git这段命令可以直接从文件夹中复制。
八：分支管理：
    $ git checkout -b dev
        表示我们创建dev分支，然后切换到dev分支：
        git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
            $ git branch dev
            $ git checkout dev
    然后，用git branch命令查看当前分支：
        $ git branch
    创建分支：git branch <name>
    切换分支：git checkout <name>
    创建+切换分支：git checkout -b <name>
    合并某分支到当前分支：git merge <name> （name表示要被合并的分支）
    删除分支：git branch -d <name>
    $ git checkout master
    表示从当前某一分支切换的master分支。









