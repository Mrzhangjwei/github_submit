## Github系列之【向Github提交代码

### 本文引用于http://stormzhang.com/github/2016/06/04/learn-github-from-zero4/

### 1.SSH
 你拥有了一个 GitHub 账号之后，就可以自由的 clone 或者下载其他项目，也可以创建自己的项目，但是你没法提交代码。仔细想想也知道，肯定不可能随意就能提交代码的，如果随意可以提交代码，那么 GitHub 上的项目岂不乱了套了，所以提交代码之前一定是需要某种授权的，而 GitHub 上一般都是基于 SSH 授权的。

那么什么是 SSH 呢？ 简单点说，SSH是一种网络协议，用于计算机之间的加密登录。目前是每一台 Linux 电脑的标准配置。而大多数 Git 服务器都会选择使用 SSH 公钥来进行授权，所以想要在 GitHub 提交代码的第一步就是要先添加 SSH key 配置。

### 2.生成SSH key
 
Linux 与 Mac 都是默认安装了 SSH ，而 Windows 系统安装了 Git Bash 应该也是带了 SSH 的。大家可以在终端（win下在 Git Bash 里）输入 ssh 如果出现以下提示证明你本机已经安装 SSH， 否则请搜索自行安装下。

 ![linux下存在SSH的截图](http://img.blog.csdn.net/20161029161513353)
 
 紧接着输入 ssh-keygen -t rsa ，什么意思呢？就是指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id_rsa 和 id_rsa.pub ，而 id_rsa 是密钥，id_rsa.pub 就是公钥。这两文件默认分别在如下目录里生成：
 
 ![产生id_rsa密钥,id_rsa.pub公钥文件](http://img.blog.csdn.net/20161029161816643)

Linux/Mac 系统 在 ~/.ssh 下，win系统在 /c/Documents and Settings/username/.ssh 下，都是隐藏文件，相信你们有办法查看的。

接下来要做的是把 id_rsa.pub 的内容添加到 GitHub 上，这样你本地的 id_rsa 密钥跟 GitHub 上的 id_rsa.pub 公钥进行配对，授权成功才可以提交代码。

### 3.GitHub 上添加 SSH key
 第一步先在 GitHub 上的设置页面，点击最左侧 SSH and GPG keys ：
 
 ![设置SSH](http://img.blog.csdn.net/20161029162256613)
 
 然后点击右上角的 New SSH key 按钮：
 
  ![添加key](http://img.blog.csdn.net/20161029162442505)
 
 需要做的只是在 Key 那栏把 id_rsa.pub 公钥文件里的内容复制粘贴进去就可以了（上述示例为了安全粘贴的公钥是无效的），Title 那栏不需要填写，点击 Add SSH key 按钮就ok了。

这里提醒下，怎么查看 id_rsa.pub 文件的内容？

Linux/Mac 用户执行以下命令：

 ![linux下执行命令查找SSH keys的值](http://img.blog.csdn.net/20161029162731115)

 Windows用户，设置显示隐藏文件，可以使用 EditPlus 或者 Sublime 打开复制就行了。

SSH key 添加成功之后，输入 ssh -T git@github.com 进行测试，如果出现以下提示证明添加成功了。

 ![SSH key添加成功的界面](http://img.blog.csdn.net/20161029162949772)

### 4.Push & Pull

 在提交代码之前我们先要了解两个命令，也是上次的文章没有介绍的，因为这两个命令需要跟远程仓库配合。

Push ：直译过来就是「推」的意思，什么意思呢？如果你本地代码有更新了，那么就需要把本地代码推到远程仓库，这样本地仓库跟远程仓库就可以保持同步了。

代码示例：``` git push origin master```

意思就是把本地代码推到远程 master 分支。

Pull：直译过来就是「拉」的意思，如果别人提交代码到远程仓库，这个时候你需要把远程仓库的最新代码拉下来，然后保证两端代码的同步。

代码示例：``` git pull origin master```

意思就是把远程最新的代码更新到本地。一般我们在 push 之前都会先 pull ，这样不容易冲突。

### 5.提交代码

 详情请点击文章刚开始的链接，主要的代码如下：

 Clone自己的项目 进入到项目中 复制你的地址，执行如下命令：
     
  ```  git clone 复制的地址  ```


  ```  git push origin master  ```


  ```  git remote add origin 要上传的路径  ```

 查看我们当前项目有哪些远程仓库可以执行如下命令：
  ```  git remove -v  ```

 接下来，我们本地的仓库就可以向远程仓库进行代码提交了：
	  ```  git push origin master  ```

 

