# Mac下JDK、Maven、Tomcat、Git开发安装及环境变量配置
原文出处：https://www.cnblogs.com/jing99/p/9070177.html 作者 kosamino

本文主要内容： 
- 1.Mac OS 安装Java 设置环境变量 
- 2.Mac OS 安装Maven设置环境变量 
- 3.Mac OS 安装Tomcat设置环境变量 
- 4.Mac OS 安装HomeBrew服务器 
- 5.Mac OS 安装Git 服务器

## 1.Mac OS 安装Java 设置环境变量
### 1.获取Java 安装包： [ Java 安装包获取地址]。
在下载Java 安装包的时候一定要下载 Java JDK ，别下载 Java JRE，因为Java JDK 里面包含有Java JRE ，而Java JRE 并不不包含 Java JDK 。 我下载的是 Java JDK 1.8,Mac OS 版本 。
### 2.安装Java JDK 
一直默认安装就好，直到完成。
### 3.接下来是本教程的核心内容，就是设置环境变量　
3.1 打开终端，输入echo Shell，查看系统使用shell脚本类型，如果输出的是bash，说明是Bourneshell，是默认的UnixShell命令。注意，echoShell，查看系统使用shell脚本类型，如果输出的是bash，说明是Bourneshell，是默认的UnixShell命令。注意，echoShell 的S一定是大写，否则会报错.  

3.2 输入java－version查看java 版本信息，如果安装成功就会输出如下信息：
  
    192:~ houjing$ java -version
    java version "10.0.1" 2018-04-17
    Java(TM) SE Runtime Environment 18.3 (build 10.0.1+10)
    Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10.0.1+10, mixed mode. 
如果不是的话，说明没有安装成功，需要检查原因，重新安装后再执行此操作。    

3.3 使用工具命令“/usr/libexec/java_home”来定位JAVA_HOME:  

    192:~ houjing$ /usr/libexec/java_home -V 
    Matching Java Virtual Machines (1):
        10.0.1, x86_64:    "Java SE 10.0.1"    
    /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
    /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
如果出现 /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home，这就是Java 的安装路径，就是Windows 系统所说的Path。  

3.4 配置JAVA_HOME：输入vim .bash_profile ，进入vim编辑器view视图.   

3.5 键盘输入i，进入插入模式，在文件尾部添加java安装路径：
    /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
    
    JAVA_HOME=/Library/java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
    PATH=$JAVA_HOME/bin:$PATH
    CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar
    export JAVA_HOME
    export PATH
    export CLASSPATH

3.6 添加完毕之后，按esc退出插入模式，并键入wq!保存退出文件

3.7 如果保存时出现：vi E212:Can’t open file for writing 说明你没有修改权限，如果没有说明已经构建成功，不用执行8-10操作

3.8 退出vim编辑器，在终端输入 sudo su命令，输入开机密码

3.9 输入vim .bash_profile 命令，进入vim编辑器view视图

3.10 键盘输入i，进入插入模式，在文件尾部添加java安装路径：

    JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home"
    CLASS_PATH="$JAVA_HOME/lib"
    PATH=".;$PATH:$JAVA_HOME/bin"
    export JAVA_HOME

3.11 输入echo $JAVA_HOME查看路径是否正确，如果正确则继续下面的操作，如果不正确则需要修改。

3.12 输入source .bash_profile 使得修改的文件生效。

3.13 输入java 命令，到此设置完毕。

    192:~ houjing$ java
    用法: java [options] <主类> [args...]
               (执行类)
       或  java [options] -jar <jar 文件> [args...]
               (执行 jar 文件)
       或  java [options] -m <模块>[/<主类>] [args...]
           java [options] --module <模块>[/<主类>] [args...]
               (执行模块中的主类)
 有关详细信息, 请参阅 http://www.oracle.com/technetwork/java/javase/documentation/index.html。  
 还可以：打开终端，输入touch .bash_profile，输入open .bash_profile打开记事本进行编辑。  
 更新配置的环境变量source .bash_profile,使得环境变量生效，可以输入 Java 进行验证。
 
 ## 2.Mac OS 安装Maven设置环境变量. 
 
1.获取Maven 安装包： [Maven 安装包获取地址](https://www.cnblogs.com/gumuzi/p/5711495.html)。  
注意，下载Maven 的时候一定是下载：apache-maven-3.3.9-src.tar.gz，复制到你需要放置的位置，解压（可以用tar命令或者就在）。我的文件名：

2.打开终端，输入touch .bash_profile，再次输入open .bash_profile打开记事本：
    
    export MAVEN_HOME=/Volumes/work/apache-maven-3.5.3
    export PATH=$MAVEN_HOME/bin:$PATH
    
3.在终端输入source ~/.bash_profile，再输入：mvn -v。
   
    192:~ houjing$ mvn -v
    Apache Maven 3.5.3 (3383c37e1f9e9b3bc3df5050c29c8aff9f295297; 2018-02-25T03:49:05+08:00)
    Maven home: /Volumes/work/apache-maven-3.5.3
    Java version: 10.0.1, vendor: Oracle Corporation
    Java home: /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
    Default locale: zh_CN_#Hans, platform encoding: UTF-8
    OS name: "mac os x", version: "10.13.4", arch: "x86_64", family: "mac"

## 3.Mac OS 安装Tomcat设置环境变量
1.获取Tomcat安装包： [Tomcat安装包获取地址](http://tomcat.apache.org/download-90.cgi)  
注意，下载Maven 的时候一定是下载：Tomcat.tar.gz，然后在桌面新建一个文件夹，名称自定义，但是一定要为英文，不可为中文。我的文件名：ApplicationsTools，就是之前放Maven的文件夹，放在一起方便查找和管理。

2.配置环境变量  
打开终端，输入touch .bash_profile，再次输入open .bash_profile打开记事本：

    export CATALINA_HOME=/Volumes/work/apache-tomcat-9.0.8
    export PATH=$CATALINA_HOME/bin:$PATH

3.更新环境变量配置  
环境变量source .bash_profile验证是否成功，终端中输入$CATALINA_HOME:

    192:~ houjing$ $CATALINA_HOME
    -bash: /Volumes/work/apache-tomcat-9.0.8: is a directory
　　
终端中输入$PATH显示如下：

    192:~ houjing$ $PATH
    -bash: /Volumes/work/apache-tomcat-9.0.8/bin:/Volumes/work/apache-maven-3.5.3/bin:/Library/java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home/bin:
    /Volumes/work/apache-tomcat-9.0.8/bin:/Volumes/work/apache-maven-3.5.3/bin:/Library/java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home/bin:
    /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin: No such file or directory

4.启动tomcat.  
终端中输入startup.sh，startup.sh后出现类似 “Permission denied” ，这个时候需要对目录进行权限设置：输入 sudo chmod 755 Library/Tomcat8/bin/*.sh 回车，设置文件的读写执行权限；
终端中输入startup.sh，startup.sh后出现类似 “Permission denied” ，这个时候需要对目录进行权限设置：输入 sudo chmod 755 Library/Tomcat8/bin/*.sh 回车，设置文件的读写执行权限；

    192:~ houjing$ cd $CATALINA_HOME/bin
    192:bin houjing$ pwd
    /Volumes/work/apache-tomcat-9.0.8/bin
    192:bin houjing$ sh startup.sh 
    Using CATALINA_BASE:   /Volumes/work/apache-tomcat-9.0.8
    Using CATALINA_HOME:   /Volumes/work/apache-tomcat-9.0.8
    Using CATALINA_TMPDIR: /Volumes/work/apache-tomcat-9.0.8/temp
    Using JRE_HOME:        /Library/java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
    Using CLASSPATH:       /Volumes/work/apache-tomcat-9.0.8/bin/bootstrap.jar:/Volumes/work/apache-tomcat-9.0.8/bin/tomcat-juli.jar
    Tomcat started.

5.关闭需要使用shutdown.sh即可。

## 4.Mac OS 安装HomeBrew 管理器
### 1.获取HomeBrew安装包： [HomeBrew 管理器官网](http://brew.sh/index_zh-cn.html)  
macOS 不可或缺的套件管理器。

### 2.安装HomeBrew
2.1 打开终端，输入：ruby -e “$(curl –insecure -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)” 后回车： 

    192:~ houjing$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ==> This script will install:
    /usr/local/bin/brew
    /usr/local/share/doc/homebrew
    /usr/local/share/man/man1/brew.1
    /usr/local/share/zsh/site-functions/_brew
    /usr/local/etc/bash_completion.d/brew
    /usr/local/Homebrew
    ==> The following new directories will be created:
    /usr/local/Cellar
    /usr/local/Homebrew
    /usr/local/Frameworks
    /usr/local/bin
    /usr/local/etc
    /usr/local/include
    /usr/local/lib
    /usr/local/opt
    /usr/local/sbin
    /usr/local/share
    /usr/local/share/zsh
    /usr/local/share/zsh/site-functions
    /usr/local/var
    ==> The Xcode Command Line Tools will be installed.

2.2 继续回车： 

    Press RETURN to continue or any other key to abort
    ==> /usr/bin/sudo /bin/mkdir -p /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include 
    /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
    Password:

2.3 输入开机密码，继续回车，你是看不见的密码的（此处还会自动帮你下载Xcode）： 

    Password:
    ==> /usr/bin/sudo /bin/chmod g+rwx /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include 
    /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
    ==> /usr/bin/sudo /bin/chmod 755 /usr/local/share/zsh /usr/local/share/zsh/site-functions
    ==> /usr/bin/sudo /usr/sbin/chown houjing /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc 
    /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions 
    /usr/local/var
    ==> /usr/bin/sudo /usr/bin/chgrp admin /usr/local/Cellar /usr/local/Homebrew /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include 
    /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/share/zsh /usr/local/share/zsh/site-functions /usr/local/var
    ==> /usr/bin/sudo /bin/mkdir -p /Users/houjing/Library/Caches/Homebrew
    ==> /usr/bin/sudo /bin/chmod g+rwx /Users/houjing/Library/Caches/Homebrew
    ==> /usr/bin/sudo /usr/sbin/chown houjing /Users/houjing/Library/Caches/Homebrew
    ==> /usr/bin/sudo /bin/mkdir -p /Library/Caches/Homebrew
    ==> /usr/bin/sudo /bin/chmod g+rwx /Library/Caches/Homebrew
    ==> /usr/bin/sudo /usr/sbin/chown houjing /Library/Caches/Homebrew
    ==> Searching online for the Command Line Tools
    ==> /usr/bin/sudo /usr/bin/touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
    ==> Installing Command Line Tools (macOS High Sierra version 10.13) for Xcode-9.3
    ==> /usr/bin/sudo /usr/sbin/softwareupdate -i Command\ Line\ Tools\ (macOS\ High\ Sierra\ version\ 10.13)\ for\ Xcode-9.3
    Software Update Tool

    Downloading Command Line Tools (macOS High Sierra version 10.13) for Xcode
    Downloaded Command Line Tools (macOS High Sierra version 10.13) for Xcode
    Installing Command Line Tools (macOS High Sierra version 10.13) for Xcode
    Done with Command Line Tools (macOS High Sierra version 10.13) for Xcode
    Done.
    ==> /usr/bin/sudo /bin/rm -f /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
    ==> /usr/bin/sudo /usr/bin/xcode-select --switch /Library/Developer/CommandLineTools
    ==> Downloading and installing Homebrew...
    remote: Counting objects: 101182, done.
    remote: Compressing objects: 100% (34/34), done.
    remote: Total 101182 (delta 23), reused 27 (delta 13), pack-reused 101135
    Receiving objects: 100% (101182/101182), 23.11 MiB | 46.00 KiB/s, done.
    Resolving deltas: 100% (73636/73636), done.
    From https://github.com/Homebrew/brew
     * [new branch]          master     -> origin/master
     * [new tag]             0.1        -> 0.1
     * [new tag]             0.2        -> 0.2
     * [new tag]             0.3        -> 0.3
     * [new tag]             0.4        -> 0.4
     * [new tag]             0.5        -> 0.5
     * [new tag]             0.6        -> 0.6
     * [new tag]             0.7        -> 0.7
     * [new tag]             0.7.1      -> 0.7.1
     * [new tag]             0.8        -> 0.8
     * [new tag]             0.8.1      -> 0.8.1
     * [new tag]             0.9        -> 0.9
     * [new tag]             0.9.1      -> 0.9.1
     * [new tag]             0.9.2      -> 0.9.2
     * [new tag]             0.9.3      -> 0.9.3
     * [new tag]             0.9.4      -> 0.9.4
     * [new tag]             0.9.5      -> 0.9.5
     * [new tag]             0.9.8      -> 0.9.8
     * [new tag]             0.9.9      -> 0.9.9
     * [new tag]             1.0.0      -> 1.0.0
     * [new tag]             1.0.1      -> 1.0.1
     * [new tag]             1.0.2      -> 1.0.2
     * [new tag]             1.0.3      -> 1.0.3
     * [new tag]             1.0.4      -> 1.0.4
     * [new tag]             1.0.5      -> 1.0.5
     * [new tag]             1.0.6      -> 1.0.6
     * [new tag]             1.0.7      -> 1.0.7
     * [new tag]             1.0.8      -> 1.0.8
     * [new tag]             1.0.9      -> 1.0.9
     * [new tag]             1.1.0      -> 1.1.0
     * [new tag]             1.1.1      -> 1.1.1
     * [new tag]             1.1.10     -> 1.1.10
     * [new tag]             1.1.11     -> 1.1.11
     * [new tag]             1.1.12     -> 1.1.12
     * [new tag]             1.1.13     -> 1.1.13
     * [new tag]             1.1.2      -> 1.1.2
     * [new tag]             1.1.3      -> 1.1.3
     * [new tag]             1.1.4      -> 1.1.4
     * [new tag]             1.1.5      -> 1.1.5
     * [new tag]             1.1.6      -> 1.1.6
     * [new tag]             1.1.7      -> 1.1.7
     * [new tag]             1.1.8      -> 1.1.8
     * [new tag]             1.1.9      -> 1.1.9
     * [new tag]             1.2.0      -> 1.2.0
     * [new tag]             1.2.1      -> 1.2.1
     * [new tag]             1.2.2      -> 1.2.2
     * [new tag]             1.2.3      -> 1.2.3
     * [new tag]             1.2.4      -> 1.2.4
     * [new tag]             1.2.5      -> 1.2.5
     * [new tag]             1.2.6      -> 1.2.6
     * [new tag]             1.3.0      -> 1.3.0
     * [new tag]             1.3.1      -> 1.3.1
     * [new tag]             1.3.2      -> 1.3.2
     * [new tag]             1.3.3      -> 1.3.3
     * [new tag]             1.3.4      -> 1.3.4
     * [new tag]             1.3.5      -> 1.3.5
     * [new tag]             1.3.6      -> 1.3.6
     * [new tag]             1.3.7      -> 1.3.7
     * [new tag]             1.3.8      -> 1.3.8
     * [new tag]             1.3.9      -> 1.3.9
     * [new tag]             1.4.0      -> 1.4.0
     * [new tag]             1.4.1      -> 1.4.1
     * [new tag]             1.4.2      -> 1.4.2
     * [new tag]             1.4.3      -> 1.4.3
     * [new tag]             1.5.0      -> 1.5.0
     * [new tag]             1.5.1      -> 1.5.1
     * [new tag]             1.5.10     -> 1.5.10
     * [new tag]             1.5.11     -> 1.5.11
     * [new tag]             1.5.12     -> 1.5.12
     * [new tag]             1.5.13     -> 1.5.13
     * [new tag]             1.5.14     -> 1.5.14
     * [new tag]             1.5.2      -> 1.5.2
     * [new tag]             1.5.3      -> 1.5.3
     * [new tag]             1.5.4      -> 1.5.4
     * [new tag]             1.5.5      -> 1.5.5
     * [new tag]             1.5.6      -> 1.5.6
     * [new tag]             1.5.7      -> 1.5.7
     * [new tag]             1.5.8      -> 1.5.8
     * [new tag]             1.5.9      -> 1.5.9
     * [new tag]             1.6.0      -> 1.6.0
     * [new tag]             1.6.1      -> 1.6.1
     * [new tag]             1.6.2      -> 1.6.2
     * [new tag]             1.6.3      -> 1.6.3
     * [new tag]             1.6.4      -> 1.6.4
    HEAD is now at 18d450122 Merge pull request #4200 from GauthamGoli/newformula-audit-condition-fix

2.4 继续回车 ：

    ==> Tapping homebrew/core
    Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
    remote: Counting objects: 4760, done.
    remote: Compressing objects: 100% (4555/4555), done.
    remote: Total 4760 (delta 54), reused 591 (delta 17), pack-reused 0
    Receiving objects: 100% (4760/4760), 3.85 MiB | 363.00 KiB/s, done.
    Resolving deltas: 100% (54/54), done.
    Tapped 4548 formulae (4,801 files, 12MB)
    ==> Cleaning up /Library/Caches/Homebrew...
    ==> Migrating /Library/Caches/Homebrew to /Users/houjing/Library/Caches/Homebrew...
    ==> Deleting /Library/Caches/Homebrew...
    Already up-to-date.
    ==> Installation successful!

    ==> Homebrew has enabled anonymous aggregate user behaviour analytics.
    Read the analytics documentation (and how to opt-out) here:
      https://docs.brew.sh/Analytics.html

    ==> Next steps:
    - Run `brew help` to get started
    - Further documentation: 
        https://docs.brew.sh

到这，HomeBrew 管理器就安装完成了！

## 6.Mac OS 安装Git

打开终端，输入 brew install git;

    192:bin houjing$ brew install git
    ==> Downloading https://homebrew.bintray.com/bottles/git-2.17.0.high_sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring git-2.17.0.high_sierra.bottle.tar.gz
    ==> Caveats
    Bash completion has been installed to:
      /usr/local/etc/bash_completion.d

    zsh completions and functions have been installed to:
      /usr/local/share/zsh/site-functions

    Emacs Lisp files have been installed to:
      /usr/local/share/emacs/site-lisp/git
    ==> Summary
    🍺  /usr/local/Cellar/git/2.17.0: 1,497 files, 35.6MB

输入brew install gcc：

    192:bin houjing$ brew install gcc
    ==> Installing dependencies for gcc: gmp, isl, mpfr, libmpc
    ==> Installing gcc dependency: gmp
    ==> Downloading https://homebrew.bintray.com/bottles/gmp-6.1.2_2.high_sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring gmp-6.1.2_2.high_sierra.bottle.tar.gz
    🍺  /usr/local/Cellar/gmp/6.1.2_2: 18 files, 3.1MB
    ==> Installing gcc dependency: isl
    ==> Downloading https://homebrew.bintray.com/bottles/isl-0.19.high_sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring isl-0.19.high_sierra.bottle.tar.gz
    🍺  /usr/local/Cellar/isl/0.19: 66 files, 3.8MB
    ==> Installing gcc dependency: mpfr
    ==> Downloading https://homebrew.bintray.com/bottles/mpfr-4.0.1.high_sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring mpfr-4.0.1.high_sierra.bottle.tar.gz
    🍺  /usr/local/Cellar/mpfr/4.0.1: 28 files, 4.6MB
    ==> Installing gcc dependency: libmpc
    ==> Downloading https://homebrew.bintray.com/bottles/libmpc-1.1.0.high_sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring libmpc-1.1.0.high_sierra.bottle.tar.gz
    🍺  /usr/local/Cellar/libmpc/1.1.0: 12 files, 353.8KB
    ==> Installing gcc
    ==> Downloading https://homebrew.bintray.com/bottles/gcc-8.1.0.high_sierra.bottle.1.tar.gz
    ######################################################################## 100.0%
    ==> Pouring gcc-8.1.0.high_sierra.bottle.1.tar.gz
    🍺  /usr/local/Cellar/gcc/8.1.0: 1,495 files, 336.1MB
　　
都完成后，输入 git -version 和 which git 验证是否成功，失败重新来过！

    192:bin houjing$ git --version
    git version 2.17.0
    192:bin houjing$ which git
    /usr/local/bin/git
    192:bin houjing$ git --help
    usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
               [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
               [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
               [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
               <command> [<args>]

    These are common Git commands used in various situations:

    start a working area (see also: git help tutorial)
       clone      Clone a repository into a new directory
       init       Create an empty Git repository or reinitialize an existing one

    work on the current change (see also: git help everyday)
       add        Add file contents to the index
       mv         Move or rename a file, a directory, or a symlink
       reset      Reset current HEAD to the specified state
       rm         Remove files from the working tree and from the index

    examine the history and state (see also: git help revisions)
       bisect     Use binary search to find the commit that introduced a bug
       grep       Print lines matching a pattern
       log        Show commit logs
       show       Show various types of objects
       status     Show the working tree status

    grow, mark and tweak your common history
       branch     List, create, or delete branches
       checkout   Switch branches or restore working tree files
       commit     Record changes to the repository
       diff       Show changes between commits, commit and working tree, etc
       merge      Join two or more development histories together
       rebase     Reapply commits on top of another base tip
       tag        Create, list, delete or verify a tag object signed with GPG

    collaborate (see also: git help workflows)
       fetch      Download objects and refs from another repository
       pull       Fetch from and integrate with another repository or a local branch
       push       Update remote refs along with associated objects

    'git help -a' and 'git help -g' list available subcommands and some
    concept guides. See 'git help <command>' or 'git help <concept>'
    to read about a specific subcommand or concept.

很多时候失败了不是没努力也不是运气差，而是努力不够，没有推自己一把！ 
