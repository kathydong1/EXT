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






核心概念：
   Ext.application 方法初始化的。这个方法的参数是一个 Ext.app.Application 对象，这个方法会加载 Ext.app.Application 类，并在页面加载完成后开始应用给定的配置 Ext.app.Application 这个类代表我们的整个应用
   
   Ext.define(name,data, callback) 你可以用这个方法定义或者重写一个类。 这个方法有三个参数，如以下代码所示。 在这里 name 参数是你要定义的类名，data 参数是应用于这个类的属性，callback 是可选参数，这个函数将会在这个类被创建后调用
   
   创建一个名为 Car 的类
   Ext.define('Car', {     
    name: null,  
    constructor: function(name) {       
        if (name) {         
            this.name = name;       
        }  
    },  
    start: function() {       
        alert('Car started');  
    }  
}) ;

使用 define 继承扩展一个类
xt.define('ElectricCar', {     
    extend: 'Car',     
    start: function() {  
        alert("Electric car started");  
    }  
}) ; 

想替换一个父类方法的实现，你可以使用 Ext.define 来重写这个方法
Ext.define('My.ux.field.Text', { 
     //继承我们使用 extend 而重写使用 override
    override: 'Ext.form.field.Text',     
    setValue: function(val) {       
        this.callParent(['In override']);       
        return this;  
    }  
}); 

