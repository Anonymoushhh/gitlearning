##Git教程（参考廖雪峰的官方网站）

+ ### 安装Git

   ​	最早Git是在Linux上开发的，很长一段时间内，Git也只能在Linux和Unix系统上跑。不过，慢慢地有人把它移植到了Windows上。现在，Git可以在Linux、Unix、Mac和Windows这几大平台上正常运行了。 

   #### Linux

   ```
   sudo apt-get install git
   ```

   ​	在Linux系统中，只需要简单的一条命令便可以安装完成Git。

   #### Windows

   ​	可直接去官网下载[安装程序](https://git-scm.com/downloads)，然后按照默认选项安装即可。

   ​	安装完成后，在桌面右键找到Git Bash，即可开始使用！

   #### Mac OS

   ​	如果你正在使用Mac做开发，有两种安装Git的方法。

   ​	一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：					  <http://brew.sh/>。

   ​	第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

   ​	安装完成后，需要在Git Bash中设置git账户：

   ```
   $ git config --global user.name "Your Name"
   $ git config --global user.email "email@example.com"
   ```

+ ### 创建版本库

  ​	什么是版本库呢？版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。 

  ​	创建一个版本库非常简单，只需要在你喜欢的地方创建一个空目录：

  ```
  $ mkdir D:/learngit
  $ cd learngit
  ```

  ​	这样我们就在D盘目录下创建了一个目录，然后切换到这个目录下，执行：

  ```
  $ git init
  ```

  ​	你就会发现，**该目录下多了一个.git目录**（如果你看不到请查看隐藏文件），这个目录是Git来跟踪管理版本库的，手动修改这个目录里面的文件会损坏Git仓库。

  ​	当然，如果你想要在一个已经在开发的项目目录下创建Git仓库也是可以的，只需要到对应路径下创建即可。

  #### 添加文件到版本库

  ​	首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。 

  ​	不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

  ​	因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

  ​	下面我们开始讲一个文件添加到版本库：

  1. 用命令git add告诉Git，把文件添加到仓库：

     ```
     $ git add README.txt
     ```

     如果想把目录下**所有更改**都添加到仓库，可以执行：

     ```
     $ git add .
     ```

  2. 用命令git commit告诉Git，把文件提交到仓库:

     ```
     $ git commit -m 'first commit'
     ```

     ​	简单解释一下git commit命令，-m后面输入的是本次提交的说明。commit之后可以把之前add的文件一次性提交到本地仓库。

+ ### 版本管理

  #### 版本回退

  ​	当我们commit了多次之后，项目就会有多个版本，有时当前版本出现了问题，因此需要回退到之前的版本。

  ​	要查看之前提交的版本，需要命令：

  ```
  $ git log
  ```

  ​	git log命令显示从最近到最远的提交日志，我们可以看到3次提交。

  ​	好了，现在我们启动时光穿梭机，准备把README.txt回退到上一个版本，怎么做呢？

  ​	首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

  ```
  $git reset --hard HEAD^
  ```

  ​	此时我们观察下README.txt就已经回到了之前的一个版本。

  ​	那么我如果后悔了，想回到最新版本怎么办？

  ​	此时需要查到最新版本的commit id，之前在输入git log时可以看到每一次提交的id：

  ```
  $ git log
  commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:06:15 2018 +0800
  
      append GPL
  
  commit e475afc93c209a690c39c13a46716e8fa000c366
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:03:36 2018 +0800
  
      add distributed
  
  commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 20:59:18 2018 +0800
  
      wrote a readme file
  ```

  ​	可以看到最新版本的id就是1094a...，于是我们可以输入：

  ```
  $ git reset --hard 1094a
  ```

  ​	不需要输入完全，git会自动去查找，但也要尽量多的输入，避免重复。

  ​	那么假设你把之前的命令窗口关掉了，此时的版本不是最新的，那么你输入git log就看不到最新版本了，此时怎么办呢？

  ​	问题的关键是我们需要找到最新版本的id，只要找到了id，就可以去往任意版本。Git提供了一个命令git reflog用来记录你的每一次命令： 

  ```
  $ git reflog
  ```

  ​	这样你就可以看到之前的操作，从而找到commit id：

  ```
  e475afc HEAD@{1}: reset: moving to HEAD^
  1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
  e475afc HEAD@{3}: commit: add distributed
  eaadf4e HEAD@{4}: commit (initial): wrote a readme file
  ```

  #### 工作区和暂存区

  ​	工作区就是你在电脑里能看到的目录，比如我的learninggit文件夹就是一个工作区 。

  ​	工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

  ​	Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

  ​	前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

  ​	第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

  ​	第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

  ​	因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

  ​	**你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。**

  ​	**所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。 **

  ​	一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的,git status可以查看当前工作区的状态： 

  ```
  $ git status
  On branch master
  nothing to commit, working tree clean
  ```

+ ### 远程仓库

  #### 将本地仓库与远程仓库关联

  ​	现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

  ​	首先，登陆GitHub，然后，找到“Create a new repo”按钮，创建一个新的仓库。

  ​	创建成功之后，可以把这个远程仓库和我们的本地仓库关联，然后再本地仓库修改项目后推送到远程仓库。

  ![1](D:\git\git教程\1.png)

  ​	github告诉我们，首先自己创建一个本地仓库或切换一个本地仓库目录下，然后执行

  ```
  $ git remote add origin git@github.com:Anonymoushhh/gitlearning.git
  ```

  ​	最后面的是你的github上的ssh或https地址（**一般使用ssh协议，因为https等其他协议会有诸多不便**）。添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。这样本地的仓库就和远程仓库关联上了，之后我们在本地仓库commit了修改后可以同步到远程仓库：

  ```
  $ git push -u origin master
  ```

  ​	由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。 

  ​	之后再同步时只需通过命令：

  ```
  $ git push origin master
  ```

  #### 从远程仓库克隆项目到本地

  ​	假设我们现在在github上托管了一个项目，需要把它克隆到本地进行开发，那么我们需要首先找到这个项目的ssh：

  ![2](D:\git\git教程\2.png)

  ​	首先切换到你想要保存该项目的目录：

  ```
  cd D:/git
  ```

  ​	然后在git bush里执行：

  ```
  $ git clone git@github.com:Anonymoushhh/BP_neural_network.git
  ```

  ​	后面为该项目的ssh。

+ ### 分支管理

  ####创建与合并分支

  ​	在版本回退里，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

  ​	一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点：  

  ![0](D:\git\git教程\0.png)

  ​	每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长： 

  ![0 (1)](D:\git\git教程\0 (1).png)

  ​	你看，Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！

  ​	不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：

  ![0 (2)](D:\git\git教程\0 (2).png)

  ​	所以Git合并分支也很快！就改改指针，工作区内容也不变！

  ​	合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：

  ![0 (3)](D:\git\git教程\0 (3).png)

  下面开始实战。

  ​	首先，我们创建dev分支，然后切换到dev分支：

  ```
  $ git checkout -b dev
  ```

  ​	git checkout命令加上-b参数表示创建并切换，相当于以下两条命令： 

  ```
  $ git branch dev
  $ git checkout dev
  ```

  ​	然后，用git branch命令查看当前分支： 

  ```
  $ git branch
  * dev
    master
  ```

  ​	git branch命令会列出所有分支，当前分支前面会标一个*号。

  ​	然后，我们就可以在dev分支上正常提交,比如对README.txt做个修改 ，之后提交：

  ```
  $ git add README.txt 
  $ git commit -m "branch test"
  ```

  ​	现在，dev分支的工作完成，我们就可以切换回master分支： 

  ```
  $ git checkout master
  ```

  ​	切换回master分支后，再查看一个README.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：

   ![0 (4)](D:\git\git教程\0 (4).png)

  ​	现在，我们把dev分支的工作成果合并到master分支上： 

  ```
  $ git merge dev
  ```

  ​	git merge命令用于合并指定分支到当前分支。合并后，再查看README.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。**这次合并是“快进模式”(Fast forward)，也就是直接把master指向dev的当前提交，所以合并速度非常快。 **

  ​	合并完成后，就可以放心地删除dev分支了： 

  ```
  $ git branch -d dev
  ```

  ​	**因为创建、合并和删除分支都是修改指针的引用，所以非常快。因此Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。 **

  #### 解决冲突

  ​	新建一个分支dev1：

  ```
  $ git checkout -b dev1
  ```

  ​	这样就新建了dev1分支并切换到该分支，然后在该分支上修改README.txt文件为1234，之后在dev1分支上提交：

  ```
  $ git add README.txt
  $ git commit -m '1234'
  ```

  ​	然后切换到master分支：

  ```
  $ git checkout master
  ```

  ​	更改master分支上的README.txt为234，之后提交：

  ```
  $ git add README.txt
  $ git commit -m '234'
  ```

  ​	此时master和dev1上都有新的提交，Git无法快速合并：

  ```
  $ git merge dev1
  Auto-merging README.txt
  CONFLICT (content): Merge conflict in README.txt
  Automatic merge failed; fix conflicts and then commit the result
  ```

  ​	此时我们查看README.txt的内容会发现：

  ```
  <<<<<<< HEAD
  1234
  =======
  234
  >>>>>>> dev1
  ```

  ​	可以看到git帮我们标出了不同分支的内容，我们修改合并后的内容为12345，再提交：

  ```
  $ git add README.txt
  $ git commit -m '12345'
  ```

  ​	此时便合并成功，可以删除dev1分支了：

  ```
  $ git branch -D dev1
  ```

  #### 分支管理策略

  ​	通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。 

  ​	如果要强制禁用Fast forward模式要使用--no-ff参数，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息：

  ```
  $ git merge --no-ff -m "merge with no-ff" dev
  ```

  ​	因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。 

  ​	合并后我们使用git log查看分支历史，可以发现，merge后就像这样：

  ![0 (5)](D:\git\git教程\0 (5).png)

  #### 多人协作

  ​	当我们从远程仓库克隆项目分支到本地时，实际上就是把远程的分支和本地的分支连接了起来，远程仓库默认名称是origin。

  ​	如果要查看远程仓库信息，用git remote：

  ```
  $ git remote
  ```

  ​	当我们推送分支时，就是把本地分支的所有提交推送到远程库。推送时，需要指定本地分支和远程分支：

  ```
  $ git push origin local-branch:remote-branch
  ```

  ​	现在假设我们有多个小伙伴同时在开发项目，小伙伴A切换到自己电脑的某个目录，然后执行:

  ```
  $ git clone 某个项目的ssh
  ```

  ​	小伙伴A想在远程仓库和本地创建dev分支，然后将远程的dev和本地的dev绑定（或者远程仓库有dev分支，在本地中创建一个dev分支与远程的绑定）：

  ```
  $ git checkout -b dev origin/dev
  ```

  ​	origin代表远程仓库，这样就将本地的dev分支和远程的dev分支绑定了。小伙伴A开心的在本地分支dev上修改，然后时不时的推送到远程：

  ```
  $ git add .
  $ git commit -m 'v1.0'
  $ git push origin dev
  ```

  ​	此时你看到小伙伴A开发的这么6，你也跃跃欲试，于是你也按照他的做法敲了一遍代码，在本地的dev分支上修改了一个文件，但不幸的是，你的小伙伴A实在是太6了！在你还没来得及push之前，他又修改了一次并成功push到远程仓库，那么此时你本地的版本就不是最新的了，你再试图push就会出现错误：

  ```
  $ git add .
  
  $ git commit -m "v1.1"
  [dev 7bd91f1] add new env
   1 file changed, 1 insertion(+)
   create mode 100644 env.txt
  
  $ git push origin dev
  To github.com:Anonymoushhh/learngit.git
   ! [rejected]        dev -> dev (non-fast-forward)
  error: failed to push some refs to 'git@github.com:Anonymoushhh/learngit.git'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ```

  ​	可以看到推送失败，因为小伙伴A的最新提交和你试图的提交有冲突。那么如何就解决呢？办法其实很简单，只要我们获取到最新分支的内容，然后与我们的本地分支进行合并，再推送：

  ```
  $ git branch --set-upstream-to=origin/dev dev
  $ git pull
  ```

  ​	首先指定本地dev分支与远程的dev关联，然后执行pull命令拉取到本地。之后合并后再次推送即可。（若不清楚如何合并或合并有冲突请参考前面）

+ ### 自定义Git

  #### 忽略特殊文件

  ​	有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等 。好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

  ​	不需要从头写 .gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：<https://github.com/github/gitignore>

  ​	忽略文件的原则是：

  1. 忽略操作系统自动生成的文件，比如缩略图等；
  2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
  3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。