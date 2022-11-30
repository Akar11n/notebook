了解开源相关的概念
 1.什么是开源
    open source code 开放源代码
    代码是公开的
    任何人都可以去查看 修改和使用开源代码

   闭源 
    软件的代码是封闭的
    只有作者可以看到闭源软件的代码
    只有作者能对源代码进行修改

   开源指的是不仅提供程序 还提供程序的源代码
   闭源指的是只提供程序 不提供源代码

  2.什么是开源许可协议
    为了限制使用者的适用范围和保护作者的权利，每个开源的项目都应该遵守开原许可协议(Open source License)

  3.常见的五种开源许可协议
    BSD 
    Apache Licence 2.0
    *GPL(GNU General Public License)
         具有传染性的一种开源协议 对商业性很不友好 不允许修改后和衍生的代码作为闭源的商业软件发布和销售
         Linux
    LGPL(GNU lesser General Public License)      
    *MIT(Massachusetts Institute of Technology,MIT)
        必须包含原作者的许可信息
        jquery node.js

   4.为什么要拥抱开源
     1.开源给使用者更多的控制权
     2.让学习变得更容易
     3.真正的安全

   5.开源项目托管平台
    免费存放开源项目源代码的网站 叫做开源项目托管平台
     Github (最NB的)
     Gitlab(对企业用户比较多)
     Gitee(国产 纯中文界面 使用友好)       

   6.什么是Github
     是全球最大的开源项目托管平台 因为只支持Git作为唯一的版本控制工具 所以叫Github  但Github != Git
     issues 提要求 fork赋值一份作为自己的项目进行修改

Github -远程仓库的使用
  1.新建空白远程仓库
  2.远程仓库的两种访问形式
     HTTPS和SSH
     HTTPS:零配置 每次访问仓库时，需要重复输入Github的账号密码才能访问成功
     SSH:需要进行额外的配置，当你配置成功之后，每次访问仓库不需要重复输入Github的账号和密码(推荐)
  3.基于HTTPS将本地仓库上传到远程仓库

  用git做
      1.本地没有现成的Git仓库
      #使用终端命令创建README.md文档 并写入初试内容为 # notebook
        echo "# notebook" >> README.md
      #初始化本地Git仓库，并将文件的修改提交到本地的Git仓库中  
        git init
        git add README.md
        git commit -m "first commit"
        git branch -M main
      #将本地仓库和远程仓库进行关联 并把远程仓库改为origin   
        git remote add origin https://github.com/Akar11n/notebook.git
      #吧本地仓库中的内容推送到远程的origin的仓库中 
        git push -u origin main   


       2.本地有现成的Git仓库
      #将本地仓库和远程仓库进行关联 并把远程仓库改为origin   
                git remote add origin https://github.com/Akar11n/notebook.git
      #吧本地仓库中的内容推送到远程的origin的仓库中 
                git branch -M main
                git push -u origin main    **之后就不用这个了 只要第一次就行 后面只运用git push就行

    4.SSH key
      作用:实现免登录和加密数据传输
      好处：免登录 加密
      两部分组成
      id_rsa(私钥文件，存放鱼客户端的电脑中即可)
      id_rsa(公钥文件，需要配置到Github中)

    5.生成SSH key  
        1.打开Git Bash
        2.粘贴如下命令，并将your_email@example.com -->替换成注册Github账号时填写的邮箱
          ssh-keygen -t rsa -b 4096 -C "makabaka402@163.com"
        3.连续敲击三次回车 即可在C盘的目录中生成 id_rsa 和 id_rsa.pub 两个文件
    
    6.配置SSH key 
      1.使用记事本打开本地的id_rsa.pub文件，复制里面的内容
      2.浏览器中登录 点击头像 --Setting是--SSH and GPG Keys --> New SSH key
      3.内容粘贴到key对应的文本框中
      4.在Title填写一个名称 来表示Key从何而来

    7.检测 SSH key是否配置成功
       输入 ssh -T git@github.com  

    8.基于SSH将本地仓库上传到Github
    需要执行ssn-keygen -t rsa -b 4096 -C "makabaka402@163.com"
      其实同理 就是把第二个那个每个赋值一份 就像HTTP的那种

    9.将远程仓库克隆到本地
    打开Git bash 输入下面命令回车执行
      git clone 远程仓库的地址 有个clone or download 里面有地址      

Git分支-本地分支操作
  1.分支的概念
      就是平行宇宙
  
  2.作用
     防止相互干扰 提高协同开发的体验
  
  3.master主分支
    master分支就是主分支 是Git默认创建的
    作用是用来保存和记录整个项目已完成的功能代码
  
  4.功能分支
    专门用来开发新功能分支 分叉出来的分支 测试完毕后合并到master主分支上 如图所示
  
  5.查看分支列表
    git branch  查看当前仓库的分支
     *代表当前所处的分支 master/main
  
  6.创建新分支
     基于当前分支来创建新分支
     git branch 新分支的名字 不会切换分支 执行完创建分支的命令之后 用户当前还所处的是master分支
  
  7.切换分支 切换到指定的分支上进行开发
    git checkout  分支名字
  
  8.分支的快速创建和切换
 #-b代表创建一个新分支
 # checkout 表示切换到刚才新建的分值上
    git checkout -b 分支名称

  9.合并分支 必须要先切换
     #1.切换到master分支
      git checkout master
     #2.在master分支上运行 git merge 命令 将login分支代码河滨到master分支
      git merge login   

  10.删除分支
    git branch -d 分支名称

  11.遇到冲突时的分支合并
    两个不同的分支中 对同一个文件进行了不同的修改 Git就没办法干净的合并他们 此时我们需要打开这些包含冲突的文件然后手动解决冲突

    #假设 再把reg分支合并到master分支期间 代码发生了冲突
    git checkout master
    git merge reg

    #打开包含冲突的文件 手动解决冲突后再实行如下命令
    git add .
    git commit -m "解决了分支合并冲突的问题"  vscode可能会出现两个文件 merge failed 失败啦

  12.将本地分支推送到远程仓库
    第一次的话执行如下命令

     # -u 表示吧本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u参数
      git push -u 远程仓库的别名 本地分支名称:远程分支名称  

    #实例
     git push -u origin payment:pay

     #如果希望远程分支的名称和本地分支名称保持一直 可以对命令进行简化
      git push -u origin payment

   2.查看远程仓库中所有的分支列表
    git remote show 远程仓库名称

   3.跟踪分支

    从远程仓库中，把远程分支下载到本地仓库中 需要运行的命令如下
   #远程仓库中 吧对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同

     git checkout 远程分支的名称
   实例
     git checkout pay

#从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
     git checkout -b 本地分支名称  远程仓库名称/远程仓库分支

   示例
     git checkout -b payment origin/pay       
   
   4.拉取远程分支的最新代码
     #从远程仓库，拉取当前分支的最新代码，保持当前分支的代码和远程分值代码一致
      git pull

   5.删除远程分支
      #删除远程仓库中，指定名称的远程分支
       git push 远程仓库名称 --delete 远程分支名称

      #示例
    git push origin --delete pay    

    git branch -D 分支名称 (强制删除)

总结
  掌握Git中基本命令的使用
    git init 
    git add .
    git commit -m "提交信息"
    git status 和git status -s
   能够使用Github创建和维护远程仓库
     能够配置Github和SSH访问
     能够将本地仓库上传到Github中
   能够掌握Git分支的基本使用
    git checkout -b 新分支名称
    git push -u origin 新分支名称
    git checkout 分支名称
    git branch        