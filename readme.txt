git 所有：
1 repository 又叫仓库，在这个目录里面的所有文件都可以被Git管理起来，每个文件
的修改，删除，git都可以跟踪，以便任何时刻都可以追踪历史。
2 pwd git中pwd命令用于显示当前目录。
3 git init 在一个目录下运行git init可以把这个目录变成git可以管理的仓库。
4 git add  命令git add告诉git,把文件添加到仓库。
5 git commit 命令git commit告诉git，把文件提交到仓库。-m后面输入的是本次提交的说明，
	可以输入任意内容，当然是最好是有意义的，这样你就能从历史记录里方便的找到改动记录。
6 git commit可以一次提交很多文件，所以可以多次git add不同的文件。
7 git status git status命令可以让我们时刻掌握仓库当前的状态
8 git diff 顾名思义就是查看difference,显示的格式正是unix通用的diff格式。
9 git log 版本控制系统可以通过git log命令查看历史记录。git log命令显示从最近到最远的
	提交日志。
10 如果嫌输出的信息太多，可以试试加上--pretty=oneline参数。
11 在git中，用HEAD表示当前版本，也就是最新的提交。上一个版本是HEAD^,上上个版本就是HEAD^^,
	如果向上太多可以写成HEAD~100等。
12 git reset 如果要回退到上一个版本的内容，就可以使用git reset命令。
13 git reflog 这个命令用来记录你用过的每一次命令。
14 git和SVN一个不同之处就是有暂存区的概念。
15 在电脑中能看到的目录，比如learngit文件夹就是一个工作区。
16 工作区有一个隐藏目录.git,这个不算工作区，而是git的版本库。
	git的版本库里存了很多东西，其中最重要的就是称为stage的暂存区，还有git为我们自动创建第一个
	分支master,以及指向master的一个指针叫HEAD.
17 git add把文件添加到版本库，就是放在暂存区，git commit把暂存区的所有内容提交到当前分支。
18 git checkout -- filename 把文件在工作区的修改全部取消。
	1 修改后还没有放到暂存区，撤销修改就回到和版本库一模一样的状态
	2 已经添加到暂存区后，又做了修改，撤销修改就回到暂存区后的状态。
19 rm 一般情况下，通常直接在文件管理器中把没用的文件删了。用rm删除文件的时候，
	git status命令会立刻告诉你。
20 git rm 确实要从版本库中删除该文件，就用git rm,然后再用git commit.
	另一情况，就是删错了，因为版本库里还有，所以很轻松将文件恢复。
21 远程仓库 git是分布式版本控制系统，同一个git仓库，可以分布到不同的机器上。
22 git与github仓库之间的传输是通过SSH加密的。
	1 创建SSH key。输入 ssh-keygen -t rsa -C 'youemail@example.com',生成的在主目录里面
	查找一个.ssh目录，里面有id_rsa和id_rsa.pub文件，其中id_rsa是私钥，不能泄露，id_rsa.pub是公钥，
	可以放心的告诉任何人。
	2 登录github，setting->sshkeys-->add ssdkey.
	因为github需要识别出你推送的提交是你推送的，而不是别人冒充的，而git支持SSH协议，所以github只要
	知道了你的公钥，就可以确认只有你寄才能推送。
	github允许你添加多个key，假如你有若干电脑，公司的家里的，只要把每台电脑的sshkey添加到github,就可以使用git
	就可以在每台电脑上往github推送了。
	3 github是免费的托管git仓库，任何人都可以看到，但只有你自己才能改。

23 登录github,在右上角看到create a new repo按钮，创建一个新的仓库。
   在repository name中填入仓库名。其他保持默认设置,点击create repository按钮。在此就创建了一个新的仓库。
   新建的repository一般都是空的，我们可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后
   把本地仓库的内容推送到github仓库。

24 然后在本地仓库，在git bash中输入命令，进行本地与github远程的关联：
	git remote add origin git@github.com:youAccountName/xx.git
	origin后面的就是在github中新仓库产生的url.
	
25 添加后，远程仓库的名字就是origin，这是git的默认叫法，也可以改成别的。
26 把本地内容推送到远程，用git push 命令，
	由于远程是空的，我们第一次推送master分支时，加上了-u参数，git不但会把本地的master分支内容
	推送到远程的master分支，还会把本地的master分支与远程的master分支关联起来，在以后的推送或者
	拉取时就可以简化命令。
	然后如果再进行提交的时候就只需要输入git push origin master就可以了，不用再加-u 了。

27 当你第一次使用git的clone或者push命令连接github的时候。

28 从远程克隆，假设我们从零开发，那么最好的方式是先创建远程仓库，然后，从远程克隆。
	1 登录github,创建一个新的仓库，例如名字叫gitkills
	勾选Initialize this repository with a README,这样github会自动创建一个README.md文件。
	2 创建好远程仓库，下一步是用命令git clone克隆远程仓库，到一个本地库。
	  然后cd到本地仓库目录中，ls可以查看目录中的文件，当前已经有了README.md文件了。
	3 可以看到github给出的地址有https,ssh,svn三种。https除了速度慢，最大的麻烦是每次推送都
	必须要输入口令。

29 分支 在版本回退里，每次提交git都把他们串成一条时间线，这条时间线就是一个分支。截止到目前，在git里只有一个
   分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master,master才是指向提交的，所以HEAD指向的就是
   当前分支。
   刚开始的时候master分支是一条线，git用master指向最新的提交，再用HEAD指向master,就能确定当前分支，以及当前分支的提交点。
   每次提交，master分支都会向前移动一步，这样随着你的不断提交，master分支的线也越来越长。
  
30 当我们创建新的分支，例如dev时，git创建了一个指针叫dev,指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上。
	git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件没有任何变化。
	不过，从现在开始，对工作区的修改和提交就是针对dev分支了，master目前不会发生变化。
	加入我们在dev上的工作完成了，就可以把dev合并到master上。git 怎么合并呢，就是直接把master指向dev的当前提交。就完成了合并。
	合并完成后，甚至可以删除dev分支，删除dev分支就是把dev指针给删掉，
	
31 创建新分支，git checkout 命令加上 -b 表示创建并切换分支。
	git branch xxx 会创建新的分支
	git checkout xxx 切换到分支

32 git branch 命令会列出当前所有分支，当前分支前会加一个*号。

33 git merge命令用于合并指定分支到当前分支
	合并后显示的Fast-forward信息，git告诉我们，这次合并是快进模式，就是直接把master指向当前的提交，所以
	合并速度非常快。

34 合并完成后，删除分支 git branch -d dev.

35 如果在合并的时候出现冲突时，我们可以通过git status来查看冲突。也可以直接查看readme.txt的内容。

36 用git log --graph命令可以查看分支合并图。

37 在试驾开发中，我们应该按照几个基本原则进行分支管理。
	首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活。干活都在dev分支上，也就是说，
	dev分支是不稳定的，到某个时候，再把dev分支合并到master上，在master分支发布版本。
	每个人都有自己的分支，时不时的往dev分支上合并就可以了。
	合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就
	看不出来曾经做过合并。
	
38 git status查看工作区，git stash可以把当前工作线程储藏起来，等以后恢复现场后继续工作。

39 git stash list 用来查看刚才储藏起来的工作区。

40 用来恢复工作区，git stash apply恢复，恢复后，stash内容不删除，你要用git stash drop来删除。
	另一种方式是git stash pop,恢复同时把stash内容也删了。
	
41 git stash apply stash@[0] 用来恢复指定的stash。

42 软件开发中添加新功能时，肯定不希望代码把主分支搞乱了。所以，没添加一个新功能，最好新建一个
	feature分支，在上面开发，完成后，合并，最后删除该feature分支。
	
43 git branch -D xxx命令用来强行删除分支。
	
44 git remote 要查看远程仓库的信息。

45 git remote -v 可以查看远程仓库更详细的信息。显示了可以抓取和推送的origin的地址。如果没有推送权限的话，就看不到push的地址。

46 关于本地分支：
	master分支是主分支，因此要时刻与远程同步；
	dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
	bug分支只用于在本地修复bug,就没必要推到远程了
	feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

47 多人协作：首先，可以试图使用git push origin branch-name 推送自己的修改。
	如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
	如果合并有冲突，则解决冲突，并在本地提交
	没有冲突或者解决掉冲突后，再用git push prigin branch-name 推送就成功
	
48 创建标签，先切换到需要打标签的分支上，然后通过命令git tag tagName来创建标签。
	并且可以通过git tag命令来查看所有标签。
	通过git show tagName可以查看标签信息。
	
49 配置简写 用 git config --global alias.xx xxxx用xx代表xxxx.
	
50 --global 参数是全局参数，也就是这些命令在这台电脑的所有git仓库下可以使用。


	
	
