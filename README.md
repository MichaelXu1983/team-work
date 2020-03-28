# 团队协作开发指南

## 目录简介

1. [环境搭建](#环境搭建)  
    * [安装编辑器](#安装编辑器)
    * [安装Git](#安装Git)
    * [安装Node](#安装Node)
    * [安装JDK](#安装JDK)
    * [安装Python](#安装Python)
    * [安装VUE其他工具](#安装VUE其他工具)
    * [安装RN其他工具](#安装RN其他工具)
2. [开发步骤](#开发步骤)
    * [领取开发任务](#领取开发任务)
    * [查看开发文档](#查看开发文档)
    * [克隆源码开发](#克隆源码开发)
    * [报告开发任务](#报告开发任务)
3. [相关知识](#相关知识) 
    * [敏捷开发指南](#敏捷开发指南)
    * [开发规约](#开发规约)
    * [常用git命令](#常用git命令)
    * [分支约定](#分支约定)
    * [文档约定](#文档约定)  
    * [Git提交规范](#Git提交规范)  

## <a name='环境搭建'>环境搭建</a>
1. <a name='安装编辑器'>安装编辑器</a>  
点击下载 [Eclipse](https://www.eclipse.org/) 和 [Visual Studio Code](https://code.visualstudio.com/)。  

2. <a name='安装JDK'>安装JDK</a>  
从 [官网](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html) 下载jdk并安装，注意选择操作系统版本。完成安装后，在系统环境变量中新增 `JAVA_HOME` 变量。
    ```shell
    # 开发环境需要安装Java Development Kit [JDK] 1.8。

    # 将jdk的bin目录路径`%JAVA_HOME%\bin`和`%JAVA_HOME%\jre\bin`加入到系统环境变量Path中。

    # 可以在命令行输入`java -version`来检查jdk安装版本。
    ```  

3. <a name='安装Python'>安装Python（Mac 自带）</a>   
从 [官网](https://www.python.org/downloads/release/python-2711/) 下载并安装python 2.7.x（3.x版本不行）。完成安装后，在用户环境变量中新增 `PYTHON_HOME` 变量。
    ```shell
    # 系统环境变量Path中添加：`%PYTHON_HOME%`和`%PYTHON_HOME%\Scripts`。

    # 安装和配置完成后需要重启电脑。

    PYTHON  // 输入命令`PYTHON`查看是否安装成功
    ```  
4. <a name='安装Node'>安装Node</a>  
从官网下载 [Node.js](https://nodejs.org/en/) 并安装后，建议设置 `Npm` 国内源以加速包下载速度。
    ```bash
    node -v                                                               // 查看node是否安装成功
    npm install -g nrm                                                    // 安装 npm 源管理工具
    nrm add npm http://registry.npmjs.org/                                // 添加国外源
    nrm add taobao https://registry.npm.taobao.org/                       // 添加国内源
    nrm add npm-all http://npm.lsswp.com/repository/npm-all/              // 添加私有源
    nrm use taobao                                                        // 使用淘宝源
    npm config list                                                       // 查看当前使用源，是否淘宝源
    ```  

5.  <a name='安装Git'>安装Git</a>  
下载 [Git](https://git-scm.com/downloads) 客户端并安装，在安装过程中记得勾选安装 `Git Bash` 和 `Git GUI` 两项，并注意要选择 `Use Git from Git Bash only` 选项。  

6. <a name='安装VUE其他工具'>安装VUE其他工具</a>  
[传送门](http://git.lsswp.com/classroom/vue/vue-webpack-start)  

7. <a name='安装RN其他工具'>安装RN其他工具</a>  
[传送门](http://git.lsswp.com/classroom/react/helloworld)     

## <a name='开发步骤'>开发步骤</a>
1. <a name='领取开发任务'>领取开发任务</a>  
注册[项目管理平台](http://work.lsswp.com/redmine/)，并告知项目管理员你的用户名，等待其分配开发任务，并在[项目概述](http://work.lsswp.com/redmine/projects/workplatform)中查看所有项目相关资料（包括：测试环境地址、用户名、密码，发布、部署等）。

2. <a name='查看API文档'>查看API文档</a>  
注册[API管理平台](http://rap2.taobao.org/)，并告知管理员用户名，待加入到组内，查看全部API。

3. <a name='克隆源码开发'>克隆源码开发</a>  
注册[源码管理平台](http://git.lsswp.com/)，并告知项目管理员你的用户名，待其分配开发权限给你后，执行以下操作：
    ```powershell
    # git 本地全局设置（打开Git Bash，任意目录执行即可）
    git config --global user.name "michael" // michael 换成自己注册gitlab的账号，执行后无消息即代表成功了（遵循Linux哲学“没有消息就是好消息”）
    git config --global user.email "michael.xu1983@qq.com" // michael.xu1983@qq.com 换成自己注册gitlab的email
    
    # 从头克隆新的项目仓库到本地进行开发（下面只演示前端工程，后端工程更换对应地址即可）
    git clone http://git.lsswp.com:10001/yunshang/project-cloud-plat.git // 下载项目前端代码和它的整个历史
    （如果需要使用SSH管理远程代码，参考这篇配置[如何配置github中的SSH key值](https://jingyan.baidu.com/article/dca1fa6f756777f1a44052e3.html)）
    cd project-cloud-plat // 进入工程目录
    git checkout -b feat/功能代号 // 新建并切换到本地功能分支，文件新增/修改都在该分支上进行，功能代号用有意义的英文表示你所开发的模块
   
    # 要求：每个方法、变量、引用、表字段的命名都要有意义，并且写注释

    # 开发完成后，打包（前台：/dist/index.html  后台：/target/workplatform.war）
    
    # 本地合并到"develop"分支并提交，请求测试
    git add . // 开发完成后，添加所有新增/更改文件到暂存区
    git commit -m "feat(影响的范围):此处填写本次修改日志便于日后查阅" // 提交暂存到本地仓库，feat代表新增文件或功能
    git checkout develop // 切换到"develop"分支
    git pull // 此处一定先取回远程仓库的变化，并解决代码冲突
    git merge --no-ff -m "merge:此处填写本次合并日志便于日后查阅" feat/功能代号 // 合并"feat/功能代号"分支中暂存区文件到"develop"分支
    git push //上传本地"develop"分支到远程仓库
    git branch -d feat/功能代号 // 删除本地功能分支
    
    # 按照提示输入自己注册的账号和密码（SSH方式不用输入）
    
    # 提交成功后，打包文件会自动部署到测试地址（视文件大小一般30-60秒）
    
    # 如果正式环境有BUG需要紧急修复
    git stash // 如果有已经修改但还未提交的代码，就暂存起来
    git checkout master // 切换到master分支
    git pull // 取回远程仓库master分支的变化，并解决代码冲突
    git checkout -b fix/修复代号 // 修复代号用有意义的英文表示
    git push origin fix/修复代号 // 推送fix/修复代号分支，请求测试合并
    git branch -d fix/修复代号 // 删除本地fix/修复代号分支
    git stash pop // 恢复之前已经修改但还未提交的代码，继续之前开发

    # 当一个里程碑完成就必须打标签
    git tag -a v1.0.0 -m "本次里程碑标志性介绍"    // 打标签
    git push origin --tags                         // 提交当前所有标签
    git tag -d v1.0.0                              // 删除v1.0.0标签
    git push origin :refs/tags/v1.0.0              // 提交删除v1.0.0标签
    ```  
    > 发布周期  
    > 修订版本号：每周末会进行日常 bugfix 更新（如果有紧急的 bugfix，则任何时候都可发布）  
    > 次版本号：每月发布一个带有新特性的向下兼容的版本  
    > 主版本号：含有破坏性更新和新特性，不在发布周期内  

4. <a name='报告开发任务'>报告开发任务</a>  
登录[项目管理平台](http://work.lsswp.com/redmine/)，更新相应任务`[状态]`、`[%完成]`进度、`[耗时]`、`[活动]`、`[注释]`、`[说明]`内写清楚测试地址（前台）或接口地址（后台）  

## <a name='相关知识'>相关知识</a>  

### <a name='敏捷开发指南'>敏捷开发指南</a>  
[传送门](http://git.lsswp.com/classroom/guide/team-work/blob/master/%E6%95%8F%E6%8D%B7%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97.pptx)  

### <a name='开发规约'>开发规约</a>  
[传送门](http://git.lsswp.com/classroom/guide/team-work/blob/master/%E5%BC%80%E5%8F%91%E8%A7%84%E7%BA%A6.docx)  

### <a name='常用Git命令'>常用Git命令</a>
[阮一峰的网络日志-常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)  

一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。  
![](http://git.lsswp.com/classroom/guide/team-work/raw/develop/assets/bg2015120901.png)  

### <a name='分支约定'>分支约定</a>  
**git 项目会分成 master、release、develop、feature、hotfix 以下几种分支类型：**   
* mater 为主分支，主要用于部署生产环境
* release 为预上线分支，当有一组 feature 开发完成，首先会合并到 develop 分支，进入提测时，会合并到 release 分支
* develop 为开发分支，当开发人员完成某个 feature 之后，手动解决冲突合并到 develop 分支
* feature 为功能分支，从 develop 上拉取代码，本地新建功能分支（命名：feature/功能代号），开发完成后本地合并到 develop 分支并提交
* hotfix 为紧急线上修复分支，需要从 master 上拉取分支进行 bug 修复，修复完成后本地合并到 develop 分支并提交

### <a name='文档约定'>文档约定</a>  
* 专有名词保持大写：HTML, HAML, SASS, REST... 等等；
* 英文和数字与中文之间要留空格，中文标点符号和中文之间不需要留空格；
* 使用中文的标点符号，句号是 `。` 不是 `.`，破折号是 `——` 不是 `-`；
* 重点词句需 `**强调**`；
* 代码缩进使用两个空格，禁止使用 Tab；

### <a name='Git提交规范'>Git提交规范</a>  
**type:**   
* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动

**scope:**   
scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同  

**subject:**   
subject 是 commit 目的的简短描述，不超过50个字符  
* 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
* 第一个字母小写
* 结尾不加句号（.）

```shell
# 简易提交
git commit -m type(scope): subject

# 详细提交
git commit

feat: 初始化全局样式

初始化全局样式，保持不同浏览器默认样式一致

- 安装 Sass 预处理器
- 创建自定义全局样式文件
- 保持不同浏览器默认样式一致

Issue #1, #2
Close #1
```  

