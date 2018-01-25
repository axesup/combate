# CodeCombat Windows 安装笔记

安装环境：Windows7 (x64)

## 安装依赖软件

下载安装软件，都用x64版本：
1. MongoDb (3.6)
2. Node.js (6.12.3) _如果用其他版本可能会出错_
3. Ruby (2.5.0)
4. Python (2.7) _不能用3.0_
5. Git (2.16.1.windows.1)
6. Microsoft Visual Studio 2013

以上软件涉及的可执行命令，包括node, npm, gem, ruby, python, git都需要加入系统的Path
变量环境。在cmd窗口中测试一下是否可以直接输入找到即可。


## 安装游戏环境

使用Windows7自带的PowerShell作为命令窗口，用cmd会出错。在“开始按钮”-“运行”处输入
“PowerShell”即可找到，系统自带。

1. 下载游戏代码安装包

  `git clone https://github.com/codecombat/codecombat`

  完成后会生成一个`codecombat`目录。然后输入`cd codecombat`进入此目录

2. 安装游戏安装工具的依赖模块

  `npm install -g bower brunch nodemon sendwithus webpack`

  其中 -g 参数表示“全局”安装，而不仅仅是装到codecombat中使用。

  `bower i`

  这一步是安装bower这个工具，之后构建游戏文件需要。

  以下两步是替换Ruby的更新网站为淘宝的镜像，避免国外原站被墙

  `gem source -r https://rubygems.org/`

  `gem source -a https://rub.taobao.org`

  以下这部为安装构建游戏具体文件所需的SASS工具

  `gem install ffi -f` 这行主要是因为sass需要的ffi模块不支持ruby 2.0以上的版本

  `gem i sass`

3. 修改可能出错的esper.js配置。打开codecombat目录下的packags.json文件，查找字符串
“esper.js”，可能看到这样一行：
  `"esper.js": "codecombat/esper.js"`
  这里的"codecombat/esper.js"描述的是从本地的esper包进行安装，但clone下来的文件并没有这个包，
  所以修改成`"esper.js": "*"`，用来从网上下载最新的版本。根据错误提示好像原作者用到是0.3.0-dev这个版本。

4. 构建编译器sass

  `npm install node-sass`

  `npm rebuild node-sass`

  由于sass模块需要利用本地的C++编译器编译（这就是要预先安装Visual Studio的原因），所以这里需要先安装，然后重新编译一下，用以生成sass目录下的一个vendo文件。

5. 构建安装codecombat游戏资源文件

  `npm install`

  注意这一步需要在codecombat目录下运行。这是最多错误发生的步骤，我发生过的问题有：
   - 报告有一个包含"/??/D:\Git\git"的出错信息。更换成PowerShell后解决
   - 报告一个"esper.js preinstall"的出错信息。修改Packages.json解决，见步骤3
   - 报告bower命令不存在的问题，安装npm install bower解决，见步骤2
   - 报告webpack命令不存在的问题，安装npm install webpack解决，见步骤2
   - 报告大量sass的vendo文件找不到的问题，通过npm rebuild node-sass解决，见步骤4

## 安装游戏数据库

1. 下载最新的游戏关卡数据库导出文件：`http://analytics.codecombat.com:8080/dump.tar.gz`
2. 解压这个文件，可以使用7-Zip软件，会得到一个dump目录
3. 运行MongoDB。需要你先建立一个数据库目录，如“d:\db”，然后运行命令`mongod --dbpath d:\db`。如果报告mongod找不到，就在命令中加上这个文件的路径前缀，这个文件在一般在你安装的MongoDB目录下的“Server\3.6\bin\”下。注意这里的“3.6”是我安装的MongoDB版本，可能会是其他版本号数字。
4. 向MongoDB导入下载回来的数据：`mongorestore --drop --noIndexRestore path/to/dump --db coco`，注意命令中的“path/to/dump”是你解压出来的dump目录的路径。

## 运行游戏

1. 启动数据库：`mongod --dbpath \path\to\dbdir`，这里的\path\to\dbpath是你自己的数据库内容目录
2. 启动游戏服务器：先进入codecombat目录，然后运行命令`npm start`
3. 用浏览器访问 http://localhost:3000/ 就可以玩游戏了
