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
   Ext.application，接受一个参数 方法初始化的。这个方法的参数是一个 Ext.app.Application 对象，这个方法会加载 Ext.app.Application 类，并在页面加载完成后开始应用给定的配置 Ext.app.Application 这个类代表我们的整个应用
   
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




下列代码来创建一个类的实例
Ext.create(Class,Options); 

这个函数在页面加载完成后调用：
Ext.onReady(function(){     
    new Ext.Component({       
        renderTo: document.body,       
        html: 'DOM ready!'  
    });  
}) ; 

Ext.define('Ext.panel.Panel', {  
    extend: 'Ext.container.Container',  
    alias: 'widget.panel'//这里是定义的别名，  
});  

Ext.Base
这是所有 Ext 类的基础。所有的 Ext 类都继承自 Ext.Base。该类所有的原型和静态成员都会传递给继承它的类

如果你需要引入一个指定命名空间下所有的 组件/类 时，使用通配符，如以下代码所示
Ext.require(['widget.*', 'layout.*', 'Ext.data.*')

用以下语法排除掉不需要的类
Ext.exclude('Ext.data.*').require('*');

requires 属性加载需要的类时，当前类初始化之前被加载。
uses 属性加载需要的类时，当前类初始化之后被加载。
singleton:true 属性当前类初始化时,该实例是一个单例对象。


Adding listeners(添加事件监听)

当你创建对象或者创建以后都可以为这个对象添加监听器。下列示例代码为这个对象添加了一个 单击事件 的监听

Ext.create('Ext.Button', {     
    renderTo: Ext.getBody(),     
    listeners: {       
        click: function() {  
            Ext.Msg.alert('Button clicked!');  
        }  
    }  
}) ;  

你也可以在对象创建之后，使用 on 方法为对象添加事件监听
var button = Ext.create('Ext.Button');  
button.on('click', function() {  
   //Do something  
}) ; 

Removing listeners (删除事件监听)
button.un('click', HandleClick);  

访问 DOM

Ext.get   ------get 方法是根据这个 DOM 元素的 ID 检索获取并封装为 Ext.dom.Element 对象
Ext.query ------种方式基于传入的 CSS 选择器 从给定的根节点开始查找。它返回一个匹配选择器的元素(HTMLElement[]/Ext.dom.Element[])数组。如果没有匹配的，返回一个空值的数组对象
Ext.select -----Ext.select 方法返回一个 CompositeElement 类型的对象，代表一个元素的集合。这个 CompositeElement 对象可以进行过滤，迭代，和对整个集合执行整体操作等

Ext.select('div.row, span.title'); //匹配所有的 class 用 .row 的 div 元素，和匹配所有 class 用 .title 的

链式选择器下列的查询方式会匹配 class 为 row 并且 title 属性值为 bar 的 div ，这个 div 属于其父元素的首个子元素
Ext.select('div.row[title=bar]:first'

Ext.ComponentQuery
Ext.ComponentQuery.query('button');  将返回所有的 xtype 为 button 的组件



1新建文件夹
打开cmd
运行sencha -sdk   ext目录  generate app --classic Sgai 项目得目录

打开app删除文件夹
copy原来为牛按得webapp文件下得除了aplication.js


打开app.js   配置mainView出口文件
    app.json   配置requires引入“ext-ux”"charts"和js文件配置需要引入得框架
    
    
    打开classic下得src得classic得src替换文件
      



