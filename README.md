探索 Sencha Cmd 命令
现在让我们学习 Sencha Cmd 的一些非常有用的命令。
Sencha 命令格式
Sencha 命令采取以下格式：

sencha [类别] [命令] [选项…] [参数…]

在 Sencha Cmd 中许多命令和可选项。我们看一下都有哪些比较重要的命令。
sencha help  获取一个 categories(类别)列表，一个顶层的 commands(命令)列表，一个可用的 options(选项)列表。
sencha help app  获取一个特定类别的帮助信息，类别名称紧随在 help 后面，例如获取一个类别 app 的帮助信息。
sencha help app clean 想进一步获取 app 命令下的子命令的帮助信息，你只需要在最后添加子命令例如 clean。
sencha upgrade --check 检查是否有 Sencha Cmd 可用的更新。
sencha upgrade 要升级 Sencha Cmd，只需要移除 –check 选项。
sencha app upgrade 后面跟上 sdk 路径   升级一个现有的 ExtJS 应用到最新版本，需要先进入到你的 ExtJS 工程目录，使用一下命令。不加路径的话，就会自动从官网下载最新版本的 ExtJS 框架
sencha app build 运行下列命令将进行构建 HTML，JS，SASS 等等。
sencha app build modern  使用 Sencha Cmd 6 构建 Ext JS 6 应用，你还可以运行下列命令选择构建 moern 或 classic 风格的应用
sencha app build classic 使用 Sencha Cmd 6 构建 Ext JS 6 应用，你还可以运行下列命令选择构建 moern 或 classic 风格的应用
modern 和 classic 的构建配置在 app.json。 默认 Sencha Cmd 运行两个构建配置： classic 和 modern 。如果需要你也可以在 app.json 中添加额外的构建配置
sencha app watch  watch 命令用于重新构建并启动应用。这不仅会启动应用程序,还监视任何代码更改，一旦代码改变，浏览器刷新将包括最新的代码

用Sencha Cmd，你可以生成 Ext JS 代码，例如 view，controller，model
sencha generate view myApp.MyView    
sencha generate model MyModel id:int,fname,lname     
sencha generate controller MyController  

sencha app upgrade [ path-to-new-framework ]Sencha Cmd 升级 SDK 的版本是很容易的。使用这个升级命令将你的程序升级到新框架

