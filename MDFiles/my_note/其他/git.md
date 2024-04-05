# Git

GitHub

-   版本控制

    什么是版本控制——版本迭代 新老版本的管理

    协同开发

    追踪记载多个文件历史记录

    统计工作量

    并行开发 提高效率

    降低错误

    -   主要版本控制工具：
        -   git（当下最流行）
        -   CVS
        -   vss
        -   tfs
        -   visual studio online

    -   分类
        -   本地版本控制-每一次修改都存一份新文件 （个人使用）

        -   集中式版本控制![image-20230115163330377](D:\MDFiles\images\image-20230115163330377.png)

            所有版本都在服务器上，用户本地只有以前同步的版本，不联网用户就就看不到历史版本 SVN

        -    分布式版本控制  git

        -    ![image-20230323135109360](D:\MDFiles\images\image-20230323135109360.png)
        
            -   每个本地用户都有全部代码——会出现安全隐患 在本地就能看到历史记录 不会因为服务器损坏、网络问题出现不能工作的情况
            -   git 和SVN的区别：
                -   git 没有中央服务器
                -   git能看到代码的更新
                -   **git是目前最先进的分布式版本控制系统 免费 开源**

-   git历史

-   环境配置

    -   卸载：

        -   >   卸载： 直接反安装即可 删除环境变量 打开控制面板卸载即可

    -   git bash ： linux 和 Unix 风格的命令行 使用最多 推荐最多

    -   git cmd ： Windows 风格的命令行

    -   git GUI ：图形界面git 不建议初学者使用 尽量先熟悉常用命令

-   基本理论

    -   基本linux 命令：
        -   cd 改变目录 cd ..
        -   cd ..回退到上一个目录 直接cd进入默认目录
        -   pwd 显示当前所在目录的路径 pwd
        -   ls(ll) 列出当前目录所有文件 只不过加两个ll更详细
        -   touch ：新建文件夹
        -   rm 删除一个文件 rm -rf /（切勿在linux系统中尝试）
        -   mkdir 新建一个目录
        -   rm -r 删除一个文件夹
        -   mv 移动文件
        -   reset 重新初始化终端/清屏
        -   clear 清屏（linux）  cls（windows）
        -   help 帮助
        -   exit 退出
        -   #表示注释
        -   git config -l 配置列表
        -   git config --system  系统配置
        -   git config --global  --list  本地配置
        -   所有的配置文件都保存在本地 git安装目录\gitconfig  Git\etc\gitconfig

-   git 基本理论

    -   三个工作区域 —— 工作目录 暂存区 资源库

        ![image-20230323143030660](D:\MDFiles\images\image-20230323143030660.png)

    -   工作区 workspace —— 平时存放代码的地方

    -   暂存区 index/stage —— 临时存放文件的改动  事实上他只是一个文件 保存即将提交的文件列表的信息

    -   仓库区 repository —— 安全存放数据的文职 有提交的版本的数据 其中head指向最新放入仓库的版本 

        ![image-20230323143605801](D:\MDFiles\images\image-20230323143605801.png)

    -   git工作流程

        -   在工作目录中 添加、修改文件
        -   将需要进行版本管理的文件放入暂存区 
        -   将从、暂存区的文件提交到git仓库
        -   git管理的文件有三种状态 已修改（modified） 已暂存（staged）和已提交（committed）

-   项目搭建

    -   配置 git config --global user.name "JinYu-2023"
    -   配置  git config --global user.email "2086689759@qq.com"
    -   环境变量 —— 为了全局使用 配置或者不配置其实无所谓
    -   本地搭建仓库 鼠标右键 git bash here
        -   git init 初始化项目

    -   克隆一个远程仓库到本地
        -   git clone 网址

-   文件操作

    -   untracked 未跟踪 在文件夹中 并没有加入git库中 通过 git add 状态变为staged

    -   unmodify 已入库 没有修改 使用git rm 移出版本库

    -   modified 文件已修改 通过git add 把文件加入到暂存区

    -   staged 暂存状态

    -   git commit -m 提交暂存区的东西 到本地仓库 -m 提交信息

    -   忽略文件

        -   有时候我们不想把一些文件纳入版本控制系统中 比如数据库文件 临时文件 设计文件等 比如前端项目 npm_modules不能打包进去 idea目录下的东西也不能放进去.gitignore

        -   忽略文件中的空行或井号（#）开始的行会被忽略

        -   可以使用linux 通配符 如星号（*）代表任意多个字符 问号（？）代表一个字符 方括号代表可选自付范围 大括号{string1, string2，...}代表可迭代的字符串等

        -   如果名称前面有一个感叹号（！）代表例外规则 不能被忽略

        -   如果名称的最前面是一个路径分隔符 / 表示要忽略的文件在此目录下 而子目录中的文件不忽略

        -   如果名称最后面是一个路径分隔符 / 表示要忽略的是此目录下的=该名称的子目录 而非稳健（默认文件或目录都忽略）

            ```python
            # 是注释
            *.txt      # 忽略所有.txt结尾的文件
            ！lib.txt  # 但是lib.txt除外
            /temp      # 仅忽略项目根目录下的TODO文件 不包括其他目录temp
            build/     # 忽略build/目录下的所有文件
            doc/*.txt  # 会忽略doc/notes.txt 但不包括doc/server/arch.txt
            ```

            

-   使用码云

    >   github 国外是有墙的
    >
    >   可以搭建自己的gitlib服务器

    -   注册登录码云 完善个人信息

    -   设置本级绑定SSH公钥 实现免密码登录（重要 码云是远程仓库 工作在本地仓库）

        ```python
        # 进入 C:\users\20866\.shh目录
        #生成公钥
        ssh-keygen
        ssh-keygen -t rsa 使用rsa的加密方式
        ```

    -   将公钥信息public key 添加到码云账户中即可 id_rsa.pub里面的代码

    -   使用码云创建一个自己的仓库

    -   许可证 —— 开源是否可以转载 是否商业适用

-   IDEA中集成git

-   git分支

![image-20230323160058188](D:\MDFiles\images\image-20230323160058188.png)

git branch 查看本地分支

git branch -r 查看远程分支

git branch dev 新建dev分支

多个分支如果并行执行 那么就会导致代码不冲突 也就是同时存在多个版本

git branch -b dev 新建一个dev分支并进入该分支

git branch -d branch-name 删除分支

git branch branch-name 合并分支