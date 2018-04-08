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
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    layout
1.面板
    (1)类结构
        Ext.Base
        Ext.AbstractComponent
            Ext.Component
                Ext.container.AbstractContainer
                    Ext.container.Container
                        Ext.panel.AbstractPanel
                            Ext.panel.Panel
    (2)常见子类
        Ext.window.Window
        Ext.form.panel  ---form的panel
        Ext.panel.Table ---grid的panel
        Ext.tab.Panel   ---标签页的panel
        Ext.menu.Menu
        Ext.tip.Tip
        Ext.container.ButtonGroup
    (3)组成面板的部件
           底部工具栏,顶部工具栏,面板头部,面板底部,面板体
           
2.布局
    (1) Auto自动布局(Ext.layout.container.Auto)
        默认为自动布局，采用布局布局的模式与HTML流式排版类似
    (2) Fit自适应布局(Ext.layout.container.Fit)
        面板里有且只有一个其它面板资源元素，并且填满整个body
    (3) Accordion折叠(即手风琴)布局(Ext.layout.container.Accordion)
        同时会初始化多个面板，当一个面板处于打开状态时，其它面板会处于收起状态
    (4) Card卡片布局(Ext.layout.container.Card)
        它和手风琴布局类似，也有多个面板；不同之处在于他用按钮来切换（常用于导航）
    (5) Anchor描点布局[Ext.layout.container.Anchor]
        根据容器的大小，自适应来为容器的子元素进行布局和定位
            A.百分比
            B.偏移量
            C.参考离边的距离定位
    (6)    多选框布局[Ext.layout.container.CheckboxGroup]
    (7) Column列布局[Ext.layout.container.Column]
        列风格的布局，每一列的宽度可以根据百分比或固定数据来控制
    (8) Table表格布局[Ext.layout.container.Table]
        和传统的HTML的Table布局方式一样，同样具有跨列，跨行的属性。
    (9) Absolute绝对布局[Ext.layout.container.Absolute]
        格局容器X、Y轴的方式绝对定位
    (10) Border边界布局[Ext.layout.container.Border]
         可以控制上、下、左、右、中 (通常用于页面框架的规划)
    (11) 盒子布局
         Ext.layout.container.Box
            Ext.layout.container.HBox 竖排
            Ext.layout.container.VBox 横排
         重要参数
            Box
                flex 具有配置flex的子项，会根据占有剩余总量的比值，来决定自己的大小
                pack 控制子元素展示的位置(start左面--这时候flex生效，center中间，end后面)
                padding 边距
            HBox
                align[top,middle,stretch,stretchmax]
            VBox
                align[left,center,stretch,stretchmax]
                
3.面板常用的配置属性
    Ext.panel.Panel
        (1) closable:true //启用关闭功能
        (2) closeAction:'destroy' //设置关闭窗口后的对象处理[destroy销毁面板|hide隐藏面板]
        (3) hideCollapsible:true  //启用面板隐藏面板体功能
        (4) collapsible:true      //是否展开面板体
        (5) 
4.Ext.tab.Panel标签页，一种特殊的布局方式
    常用方法
        setActiveTab( Ext.Component card) 设置当前显示的标签页

posted @ 2013-04-27 18:15 赵雪丹 阅读(15) 评论(0) 编辑
chart
1.关于图表
    图表的轴(axes)
        (1) 数值轴 Ext.chart.axis.Numeric
        (2) 时间轴 Ext.chart.axis.Time
        (3) 分类轴 Ext.chart.axis.Category
        (4) 仪表轴 Ext.chart.axis.Gauge
    图表的类型
        (1) 折线图 Ext.chart.series.Line
        (2) 柱形图 Ext.chart.series.Column
        (3) 饼状图 Ext.chart.series.Pie
        (4) 条形图 Ext.chart.series.Bar
        (5) 面积图 Ext.chart.series.Area
        (6) 雷达图 Ext.chart.series.Radar
        (7) 散点图 Ext.chart.series.Scatter
        (8) 仪表图 Ext.chart.series.Gauge
    常用属性
        highlight高亮，label标题，tips提示，renderer格式化

posted @ 2013-04-27 18:15 赵雪丹 阅读(32) 评论(0) 编辑
Form组件
1.根类
      Ext.form.Basic
      提供了表单组件,字段管理,表单提交,数据加载的功能
2.表单的容器
      Ext.form.panel
      容器自动关联 Ext.form.Basic的实例对象,更方便的进行字段的配置
      重要属性
          defautType : "" （设置默认子项的xtype）
3.数据交互和加载
      Ext.form.action.Action（两种表单自身的提交方式）
          Ext.from.action.Submit Ajax方式提交
              Ext.form.action.StandardSubmit 原始鼻癌单提交方法
          Ext.form,action.DirectLoad
              Ext.form.action.DirectSubmit 类似于dwr的方式提交
4.字段的类型
      Ext.form.field.Base 根类
          混入了的类[Ext.form.field.Field]得到表单的处理功能
          混入了的类[Ext.form.Labelable]得到表单标签错误信息提示功能
          Ext.form.field.Text 文本框方式的如下：
              Ext.form.field.TextArea 富文本域
              Ext.form.field.Trigger 触发器
                  Ext.form.field.Picker 触发器子类（选择器）
                      Ext.form.field.Time
                      Ext.form.field.Date
                      Ext.form.field.Number
                      Ext.form.field.file 文件上传
                      Ext.form.field.ComboBox 选择框
              Ext.form.field.Checkbox 选择框方式的
                  Ext.form.field.Radio 单选框
              Ext.form.field.Hidden 特殊的--隐藏字段（数据页面不显示，但后台需要）
      Ext.form.field.HtmlEditor 特殊的--文本编辑框
5.其中夹杂布局的类
      Ext.form.FieldContainer
          Ext.form.CheckboxGroup
              Ext.form.RadioGroup
      Ext.form.Label
          Ext.form.Labelable
      Ext.form.FieldSet
      Ext.form.fieldContainer (里面可以放多个表单项，进行统一布局)
6.常用的组件配置
      Ext.form.Panel
          重要的配置项
              title:'',
              bodyStyle:'',
              frame:true,
              height:122,
              width:233,
              renderTo:'',
              defaultType:'',
              defaults:{
                  allowBanlk:true,
                  msgTarget:'side',
                  pageSize:4  //配置这个参数即可在下拉框内一分页的形式操作数据 
              },
              由于混入了Ext.form.labelable所以可进行如下配置；
                  labelSeparator 字段的名称与值直之间的分隔符
                  labelWidth 标签宽度          
      Ext.form.field.Text 文本框(xtype:textfield)
          重要配置项
              width:156,
              allowBlank:false,//不能为空
              labelAlign:'left',
              msgTarget:'side' //在字段的幼斌展示提示信息
              grow:false,//是否在这个表单字段规定长度内，自动根据文字的内容进行伸缩
              selectOnFocus：true, //当字段的内容得到焦点的时候，选择所有文本
              regex : /\d+/g,
              regexText : '请输入数字',
              inputType:'password',//其它类型：email、url等。默认text
              //vType:'IPAddress'用于数据校验,Ext.form.field.VTypes
              //如果校验不是你想要的，可以自定义，如下：
              //custom Vtype for vtype:'IPAddress'
                Ext.apply(Ext.form.field.VTypes, {
                    IPAddress:  function(v) {
                        return /^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$/.test(v);
                    },
                    IPAddressText: 'Must be a numeric IP address',
                    IPAddressMask: /[\d\.]/i //不符合正则的，键盘整么输入，都不起作用
                });
      Ext.form.field.Number
          重要的配置项
              allowDecimals：false,//不能输入小数
              hideTrigger:true,//隐藏框帮边的调节按钮    
              decimalPrecision : 3,//自动四舍五入,保留小数位为3位。
              emptyText：'请输入小数'//默认框内灰色提醒
              //指定范围
              minValue:10,
              maxValue:100,    
              baseChars:'01',//表示框内只能输入0和1        
              step:'0.8',//指定步长
              
      Ext.form.field.ComboBox
          Ext.view.BoundList 约束列表
          重要属性
              listConfig：{
                //规划下拉框到底是什么样的样式
                //这里面的值是根据BoundList里面的属性进行初始化的
                getInnerTpl:function()
                {
                    return "<div style='color:red'>${name}</div>";//动态改变下拉框内容样式
                }
              } 
              queryMode:'remot', //local(本地数据)|remot(远程数据)
              valueFiled:'id',//后台需要
              displayField:'name'//页面显示的
              forceSelection:true, //必须选中数据集合中有的数据
              minChars:2,//表示输入2个字符的的时候，就到后台请求数据
              queryDelay:400,
              queryParam:'name',//指定往后台传入的参数名称,对应的参数值是你输入的参数
              multiSelect:true, //允许多选
              typeAhead:true,   //自动补全
      Ext.form.field.Date
          重要属性
              disableDays:[0,6] //周日与周六不能选为灰色
7.常用事件
      当字段类型为xtype:'triggerfield',它具有onTriggerClick事件，
      经常用于从其它弹出表格中选择某个值。              
                  
8.常用操作    
      获取表单中某项的值
          var fieldValue = Ext.getCmp('表单id').getForm().findField('字段名称').getValue();     
          
      自动填充表单的各项值
        loadRecord( Ext.data.Model record) : Ext.form.Basic
        Loads an Ext.data.Model into this form by calling setValues with the record data. See also trackResetOnLoad.

posted @ 2013-04-27 18:14 赵雪丹 阅读(24) 评论(0) 编辑
Tree
1. 类结构
    Ext.panel.Panel
        Ext.panel.Table
            Ext.tree.Panel --- 他是和grid完全一样的

2. 主要配置项
        title 标题
        width 宽
        height 高
        renderTo 渲染到什么地方
        root 控制根节点(Ext.data.Model/Ext.data.NodeInterface)
        animate : Boolean 控制收起和展开是发有动画效果
        store: store 数据集合
        rootVisible : false,//控制显隐的属性
    重要事件
        itemclick:function(tree,record,item,index,e,options)
    重要方法
        expandAll
        collapseAll
        getChecked
        appendChild    
        
3. Ext.data.TreeStore
    重要属性
        defaultRoodId  //指定根节点

4. 树形的拖拽（插件）
    Ext.tree.ViewDDPlugin
        alias ：'plugin.treeviewdragdrop'
    需要在tree的panel下面加
        viewConfig:{
            plugins:{
                ptype :'treeviewdragdrop',
                appendOnly:true //加上这个叶子节点之间拖拽时，会弹出图形警告。
            }
        }    
    事件
        listeners:{
            drop: function(HtmlElement node, Object data, Ext.data.Model overModel, String dropPosition)
            beforedrop: function(HtmlElement node, Object data, Ext.data.Model overModel, String dropPosition, Function dropFunction)
        }

5. 关于节点的拷贝与粘贴
         重要方法
              updateInfo（把更新的节点属性值，更新显示的界面）

6. 关于删除节点操作
        重要方法
             remove（节点的方法）
        
7. 多列树的配置
         主要配置项
              columns（与表格一样）

8. 级联选中，以及级联不选中

9. 关于Store的Proxy里的api应用

Ext.define("AM.store.deptStore",{
 extend:'Ext.data.TreeStore',
 defaultRoodId:'root',
 proxy:{
  //Proxy里面的api属性，可以存放crud的后台url，通过前台就可以取到
  api:{
   update:"/extjs/extjs!updateDept.action",
   remove:"/extjs/extjs!delDept.action"
  }
  type:'ajax',
  url:'/extjs/extjs!getDept.action',
  reader:'json',
  autoLoad:true
 }
});

 

Ext.define("AM.view.deptView",{
 extend:'Ext.tree.Panel',
 alias: 'widget.deptTree',
 title : '部门树形',
 width : 250,
 height: 300,
 padding : '5 3 3 10',
 rootVisible : false,//控制显隐的属性
 config：{
  copyNodes:'' //充当剪切板的作用,临时存放树节点
 }
 //里面得配置与表格类似
 columns:[
  {
   xtype:'treecolumn',
   text:'text',
   width:150,
   dataIndex:'text'
  },{
   text:'info',
   dataIndex:'info'
  }
 ],
 viewConfig:{
  plugins:{
   ptype :'treeviewdragdrop',
   appendOnly:true //加上这个叶子节点之间拖拽时，会弹出图形警告。
  }
  listeners:{
   drop:function(node,data,voerModel,dropPosition,options){
    alert("把："+data.records[0].get('text')+"移动到："+overModel.get('text'));
   }
   beforedrop:function(node,data,overModel,dropPosition,dropFunction){
    if(overModel.get("leaf")) //如果把一个节点拖到一个叶子节点下面时，这时我可以把叶子节点修改为费叶子节点，就可以放了。
    {
     overModel.set('leaf',true);
    }
   }
  }
 } 
 dockedItems:[{
  xtype:'toolbar',
  dock:'left',
  //ui:'footer',
  items:[
   {xtype:'button',text:'add',id:'add'},
   {xtype:'button',text:'copy',id:'copy'},
   {xtype:'button',text:'delete',id:'delete'}
   {xtype:'button',text:'delete',id:'paste'}
  ]
 },{
  xtype:'toolbar',
  items:[{
   xtype:'button',
   id:'allopen',
   text:'展开全部'
  },{
   xtype:'button',
   id:'allclose',
   text:'收起全部'
  }]
 }],
 store:'deptStore'
});

 

Ext.define('AM.controller.deptController', {
    extend: 'Ext.app.Controller',
 init:function(){
  this.control({
   "deptTree":{
    checkchange:function(node,checked,options){
     if(node.data.leaf == false)
     {
      if(checked){
       //先展开节点
       node.expand();
       //遍历子节点，如果遇到非叶子节点，将递归遍历
       node.eachChild(function(n){
        n.data.checked = true;
        n.updateInfo({checked:true});
       })
      }else
      {
       //先展开节点
       node.expand();
       //遍历子节点，如果遇到非叶子节点，将递归遍历
       node.eachChild(function(n){
        n.data.checked = false;
        n.updateInfo({checked:false});
       })
      }else
      {
       //只要有一个叶子节点没有选中,父节点都不应该选中
       if(!checked){
        node.parentNode.data.checked = false;
        node.parentNode.updateInfo({checked:false});
       }
      }
     }
     var tree = b.ownerCt.ownerCt;
     //得到选中数据集合
     var nodes = tree.getChaecked();
     for(i=0;i<nodes.length;i++)
     {
      nodes[i].remove(true); //删除该节点
     }
   },
      "deptTree button[id=delete]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     //得到选中数据集合
     var nodes = tree.getChaecked();
     for(i=0;i<nodes.length;i++)
     {
      nodes[i].remove(true); //删除该节点
      //通过ajax向后台提交删除数据
      
      //通过这种方式也是可以自动提交到后台的，不过数据可能不是你所需要的。
         //tree.getStore().getProxy().update(new Ext.data.Operation(
       //{action:'remove'} //你写什，它就会提交那个url，eg：{action:'update'}
      //));
      
      //自己组装参数Ajax的提交（常用）
      Ext.Ajax.request({
       //通过这种方式就可以直接获取到store里面配置的url
       //避免url到处乱写
       //其实就是利用了store的proxy里面已经有的api属性来存放url集合
       url: tree.getStore().getProxy().api['remove'],
       params: {
        id: nodes[i].data.id
       },
       success: function(response){
        var text = response.responseText;
        // process server response here
       }
      });
     }
   },
   "deptTree button[id=copy]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     //得到数据集合
     var nodes = tree.getChaecked();
     if(nodes.length>0){
      //把数据放到剪切板中
      tree.setCopyNodes(Ext.clone(nodes));
      for(i=0;i<nodes.length;i++)
      {
       nodes[i].data.checked = false; //这个只是更新节点的属性值，并没有更新显示到页面
       nodes[i].updateInfo();//更新显示到页面
      }
     }
    }   
   },
   "deptTree button[id=paste]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     //获得被追加孩子的节点集合
     var checkNodes = tree.getChecked();
     //去剪切板中取数据
     var nodes = tree.getCopyNodes();
     if(checkNodes.length == 1 && nodes.lenght > 0){
      // 被追加孩子的节点
      var node  = checkNodes[0];
   
      for(i=0;i<nodes.length;i++){
       var el = nodes[i].data;
       //在这里可以进行组装数据传入后台
       node.appendChild(el);
      }

     }else{
      alert("剪切板中没有数据或没有选中节点");
     }
    }   
   },
  
   "deptTree button[id=allopen]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     tree.expandAll();
    }   
   },   
   "deptTree button[id=allclose]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     tree.collapseAll();
    }   
   },
   "deptTree button[id=add]":{
    click:function(b,e){
     var tree = b.ownerCt.ownerCt;
     var nodes = tree.getChecked();
     if(nodes.length == 1){
      var node = nodes[0];
      node.appendChild({
       checked:true,
       text:'技术架构组',
       id : '0103',
       leaf:true  
      });
     }else{
      alert("请您选择一个节点");
     }
    }
   },
   "deptTree":{
    itemclick:function(tree,record,item,index,e,options){
     alert(record.get('id'));
    }
   }
  });
 },
 views:[
  'deptView'
 ],
 stores :[
  'deptStore'
 ],
 models :[
 ] 
});

posted @ 2013-04-27 18:13 赵雪丹 阅读(24) 评论(0) 编辑
Grid组件
1. 表格面板类Ext.grid.Panel基本属性。（两个别名xtype:gridpanel, grid）

 

    重要的配置参数：
       （1）columns : Array 列模式(Ext.grid.column.Columnxtype: gridcolumn)
        列里面的常用配置参数：
                text : String 列的标题 默认是""
                dataIndex : String 和Model的列一一对应的
                field: {} //配合插件使用，告诉插件在那一列起作用
                xtype:默认为gridcolumn
                renderer : function(value) //可以列里面值显示之前，做一些改变。

                                                   //参数value就是列的值，我可以在函数处理后，返回其改变后的值。
       （2）title : String 表格的标题，如果不写默认表格是没有头标题那一栏。
       （3）renderTo : Mixed 把表格渲染到什么地方，即展示到那个元素里面。
       （4）width : Number 宽 
       （5）height: Number 高            
       （6）frame : Boolean 是否填充渲染这个Panel（渲染的比较好看）
       （7）forceFit : true 设定表格列的长度是否自动填充
       （8）store : store 数据集合
       （9）tbar: [] 头部工具栏，里面可以放置各种按钮
       （10）bbar：[] 底部操作栏，一般放分页面板 
       （11）dockedItems : Object/Array 更具有位置的灵活性,当你用这个属性时,

                                                     可以指定工具条停靠在表格中上下左右位置；可以用来替换tbar与bbar。 
        
       （12）selType : 'checkboxmodel'/'rowmodel'/'cellmodel',

                             选择模式即选中记录方式：选择框/鼠标单击或双击行选择/鼠标单击或双击单元格选择

                            （用多选框模式时,forceFit属性最好不启用，或则样式不好看）
       （13）multiSelect :true,//允许多选 与上面属性联合属性
       （14）plugins :[] 插件的形式，为表格添加一些特殊的功能（eg：单元格编辑、行编辑以及行拖拽等）

 

         例子可以参考上面MVC里面view层里面的grid定义。

 

2. 常用表格的列都有哪些类型。

 

    （1）Ext.grid.column.Column xtype: gridcolumn 普通列
    
    （2）Ext.grid.column.Action xtype: actioncolumn
        在表格中渲染一组图标按钮,并且为他赋予某种功能，类似于链接
          altText : String 设置应用image元素上的alt
          handler : function(view,rowindex,collndex,item,e);
          icon     : 图标资源地址
          iconCls : 图标样式
          items   : 多个图标的数组   //在使用MVC的时候建议不要用  如果大家有好得放大请与uspcat联系 
                function(o,item,rowIndex,colIndex ,e)
          stopSelection : 设置是否单击选中不选中
            
   （3）Ext.grid.column.Boolean xtype: booleancolumn
          falseText,

          trueText
        
   （4）Ext.grid.column.Date xtype: datecolumn
          format:'Y年m月的日'
        
   （5）Ext.grid.column.Number xtype: numbercolumn
          format:'0,000'
        
   （6）Ext.grid.column.Template xtype: templatecolumn
          xtype:'templatecolumn',
          tpl :"${字段的名称}"  可以进行动态的组合字段的值，作为该字段的值。

   （7）Ext.grid.RowNumbererxtype: rownumberer    //显示行号

Ext.define("AM.view.List",{
 extend:'Ext.grid.Panel',
 title : 'Grid Demo',//标题
 alias: 'widget.userlist',
 frame : true,//面板渲染
 width : 1000,
 height: 280,
 columns : [ //列模式
    Ext.create("Ext.grid.RowNumberer",{}),
    {text:"Name",dataIndex:'name',width:100},
    {text:"age",dataIndex:'age',width:100},
    {text:"email",dataIndex:'email',width:200,
     field:{
      xtype:'textfield',
      allowBlank:false
     }
    },{
     text:'sex',
     dataIndex:'sex',
     width:50,
     DDName:'sy_sex',
     renderer:function(value){
      if(value){
       if(value == "女"){
        return "<font color='green'>"+value+"</font>"
       }else if(value == "男"){
        return "<font color='red'>"+value+"</font>"
       }
      }
     }
    },{
     text:'isIt',
     dataIndex:'isIt',
     xtype : "booleancolumn",
     width:50,
     trueText:'是',
     falseText:'不是'
    },{
     text:'birthday',
     dataIndex:'birthday',
     xtype : "datecolumn",
     width:150,
     format:'Y年m月d日'
    },{
     text:'deposit',
     dataIndex:'deposit',
     xtype:'numbercolumn',
     width:150,
     format:'0,000'
    },{
     text:'描述',xtype:'templatecolumn',
     tpl:'姓名是{name} 年龄是{age}',
     width:150
    },{
     text:'Action',xtype:'actioncolumn',
     id:'delete',
     icon:'app/view/image/table_delete.png',
     width:50//,
//     items :[
//      {},{}
//     ]
//     handler:function(grid,row,col){
//      alert(row+" "+col);
//     }
    }
 ],
 tbar :[
    {xtype:'button',text:'添加',iconCls:'table_add'},
    {xtype:'button',id:'delete',text:'删除',iconCls:'table_remove'},
    {xtype:'button',text:'修改',iconCls:'table_edit'},
    {xtype:'button',text:'查看',iconCls:'table_comm'}
 ], 
 dockedItems :[{
    xtype:'pagingtoolbar',
    store:'Users',
    dock:'bottom',
    displayInfo:true
 }],
 plugins:[
    Ext.create("Ext.grid.plugin.CellEditing",{
     clicksToEdit : 2 //单击几下
    })
 ],
 selType:'checkboxmodel',//设定选择模式
 multiSelect:true,//运行多选
 store : 'Users',
 initComponent:function(){
  this.callParent(arguments);
 }
});

3. 选择模型Ext.selection.Model的用法（嵌套在一些高级组件使用）以及表格的一些特性功能。

 

     选择模型Ext.selection.Model的用法

    （1）选择模式的根类Ext.selection.Model (通过选择模式里面提供的方法进行操作行的选择)
           重要方法：
                撤销选择 deselect( Ext.data.Model/Index records, Boolean suppressEvent ) : void
                得到选择的数据getSelection( ) : Array
                得到最后被选择数据getLastSelected( ) : void
                判断你指定的数据是否被选择上isSelected( Record/Number record ) : Boolean
                选择你指定的行selectRange( Ext.data.Model/Number startRow, Ext.data.Model/Number endRow, [Boolean keepExisting], Object dir ) : void
                keepExisting true保留已选则的项,false重新选择，不保留已选则的项
            
   （2） 隐藏了一个单元格的选择模式 selType: 'cellmodel'    (从这发现的Ext.grid.plugin.CellEditing)
           重要方法
                得到被选择的单元格getCurrentPosition() Object
                    Ext.JSON.encode()
                    itemclick( Ext.view.View this, Ext.data.Model record, HTMLElement item, Number index, Ext.EventObject e, Object options )


                selectByPosition({"row":5,"column":6}) 很实用，选中你要特殊处理的数据单元格
            
   （3） Ext.selection.CheckboxModel 多选框选择器
        重要方法
    
   （4）Ext.selection.RowModel      rowmodel 行选择器（通过鼠标单击表的行记录进行选择）
         重要属性
              multiSelect 允许多选
              simpleSelect 单选选择功能
              enableKeyNav 允许使用键盘上下键选择

 

    表格的一些特性功能 

   （1）Ext.grid.feature.RowBody  表格的行体（在行的下面来一个空白行，显示你所需要的信息）
          重要方法
                getAdditionalData( Object data, Number idx, Ext.data.Model record, Object orig ) : void
                如果你要展示这个面板那么必须复写这个方法
                features: [
                        Ext.create("Ext.grid.feature.RowBody",{
                            getAdditionalData:function(data,idx,record,orig){
                                ......
                            }
                        })
                ],    
                2.必须返回行体的对象
                var headerCt = this.view.headerCt,
                    colspan  = headerCt.getColumnCount();
                return {
                    rowBody: "",
                    rowBodyCls: this.rowBodyCls,
                    rowBodyColspan: colspan
                };
                
   （2）Ext.grid.feature.AbstractSummary negative 能够在表格数据的最后做一些统计功能。

                                                                   （eg：统计某一列的平局值等）
          Ext.grid.feature.Summary
               实用方法是在
                    第一步
                    features: [{
                        ftype: 'summary'
                    }],
                    第二步
                    columns中配置summaryType: 'count', (count,sum,min,max,average)
                    summaryRenderer: function(value, summaryData, dataIndex) {
                       return Ext.String.format(' : '+value); 
                    }    
    用于对某一列，进行求平均值等。            
                            
   （3）Ext.grid.feature.Grouping        
          在store中设置可以分组的属性
            groupField : ' '
          在view中增加代码
            Ext.create("Ext.grid.feature.Grouping",{
                    groupByText : "职业分组",
                    groupHeaderTpl : "职业{name}  一共{rows.length}人",
                    showGroupsText : "展示分组",
                    startCollapsed : true
                
            }   

        
  （4）其它功能:

            重要事件
                  groupclick
                  groupdblclick
                  groupcontextmenu
                  groupexpand
                  groupcollapse


  （5）Ext.grid.feature.GroupingSummary


  （6）Ext.grid.feature.Chunking

Ext.define("AM.view.List",{
 extend:'Ext.grid.Panel',
 title : 'Grid Demo',//标题
 alias: 'widget.userlist',
 frame : true,//面板渲染
 width : 1100,
 height: 450,
 features: [
  Ext.create("Ext.grid.feature.RowBody",{
      getAdditionalData: function(data, idx, record, orig) {
          var headerCt = this.view.headerCt,
              colspan  = headerCt.getColumnCount();
          return {
              rowBody: record.get('email'),
              rowBodyCls: this.rowBodyCls,
              rowBodyColspan: colspan
          };
      }
  }),{
   ftype: 'summary'
  },Ext.create("Ext.grid.feature.Grouping",{
     groupByText : "性别分组",
     groupHeaderTpl : "性别{name}  一共{rows.length}人",
     showGroupsText : "展示分组"
    
  })
 ], 
 columns : [ //列模式
    Ext.create("Ext.grid.RowNumberer",{}),
    {text:"Name",dataIndex:'name',width:100},
    {text:"age",dataIndex:'age',width:100,
     summaryType:'average',
     summaryRenderer: function(value, summaryData, dataIndex) {
              return Ext.util.Format.number(value,"00.0")
           } 
    },
    {text:"email",dataIndex:'email',width:200,
     field:{
      xtype:'textfield',
      allowBlank:false
     }
    },{
     text:'sex',
     dataIndex:'sex',
     width:50,
     DDName:'sy_sex',
     renderer:function(value){
      if(value){
       if(value == "女"){
        return "<font color='green'>"+value+"</font>"
       }else if(value == "男"){
        return "<font color='red'>"+value+"</font>"
       }
      }
     }
    },{
     text:'isIt',
     dataIndex:'isIt',
     xtype : "booleancolumn",
     width:50,
     trueText:'是',
     falseText:'不是'
    },{
     text:'birthday',
     dataIndex:'birthday',
     xtype : "datecolumn",
     width:150,
     format:'Y年m月d日'
    },{
     text:'deposit',
     dataIndex:'deposit',
     xtype:'numbercolumn',
     width:150,
     format:'0,000'
    },{
     text:'描述',xtype:'templatecolumn',
     tpl:'姓名是{name} 年龄是{age}',
     width:150
    },{
     text:'Action',xtype:'actioncolumn',
     id:'delete',
     icon:'app/view/image/table_delete.png',
     width:50//,
//     items :[
//      {},{}
//     ]
//     handler:function(grid,row,col){
//      alert(row+" "+col);
//     }
    }
 ],
 tbar :[
    {xtype:'button',text:'添加',iconCls:'table_add'},
    {xtype:'button',id:'del',text:'删除',iconCls:'table_remove'},
    {xtype:'button',text:'修改',iconCls:'table_edit'},
    {xtype:'button',text:'查看',iconCls:'table_comm'},
    {xtype:'button',id:'selection',text:'selection',iconCls:'table_comm'}
 ], 
 dockedItems :[{
    xtype:'pagingtoolbar',
    store:'Users',
    dock:'bottom',
    displayInfo:true
 }],
 plugins:[
    Ext.create("Ext.grid.plugin.CellEditing",{
     clicksToEdit : 2
    })
 ],
 //selType:'rowmodel',//设定选择模式
 selType:'cellmodel',
 //multiSelect:true,//运行多选
 //enableKeyNav :true,
 store : 'Users',
 initComponent:function(){
  this.callParent(arguments);
 }
});

 

 

Ext.define('AM.controller.Users', {
    extend: 'Ext.app.Controller',
 init:function(){
  this.control({
   'userlist':{
    itemclick:function(View,  record,  item,  index,  e,  options ){
     var sm = View.getSelectionModel();//.getSelection();        
        //alert(Ext.JSON.encode(sm.getCurrentPosition()));
     sm.selectByPosition({"row":1,"column":2});
    }
   },
   'userlist button[id=selection]':{
    click:function(o){
     var gird = o.ownerCt.ownerCt;
     var sm = gird.getSelectionModel();
     //sm.deselect(0);
     //alert(sm.getLastSelected().get('name'))
     //alert(sm.isSelected(0));
     //sm.selectRange(1,2,true);
     sm.selectByPosition({"row":2,"column":3});
    }
   },
   'userlist button[id=del]':{
    click:function(o){
     var gird = o.ownerCt.ownerCt;
      var data = gird.getSelectionModel().getSelection();
      if(data.length == 0){
       Ext.Msg.alert("提示","您最少要选择一条数据");
      }else{
       //1.先得到ID的数据(name)
       var st = gird.getStore();
       var ids = [];
       Ext.Array.each(data,function(record){
        ids.push(record.get('name'));
       })
       //2.后台操作(delet)
       Ext.Ajax.request({
        url:'/extjs/extjs!deleteData.action',
        params:{ids:ids.join(",")},
        method:'POST',
        timeout:2000,
        success:function(response,opts){
         Ext.Array.each(data,function(record){
          st.remove(record);
         })
        }
       })
       //3.前端操作DOM进行删除(ExtJs)
      }
    }
   },
   "userlist actioncolumn[id=delete]":{
    click : function(o,item,rowIndex,colIndex ,e){
     alert(rowIndex+" "+colIndex);
    }
   }
  });
 },
 views:[
  'List'
 ],
 stores :[
  "Users"
 ],
 models :[
  "User"
 ] 
});

4.插件使用以及其它的特性使用。

 

（1）可编辑插件的根 Ext.grid.plugin.Editing
        Ext.grid.plugin.Editing
             Ext.grid.plugin.CellEditing  这个不讲(之前课程讲过)
             保存修改的两种办法：
             a、设立保存按钮,用户单击的时候保存数据
            
                st.sync(); //数据与后台进行同步，一般不用，他会把整个记录传到后台
                           //如果不写这句，下面的语句是得不到数据的
                var records = st.getUpdatedRecords();
                Ext.Array.each(records,function(model){
                    model.commit(); //前台的小红点会消失
                });    

                我们可以selectModel来获得修改的数据，组装后在往后台传入。
                
            b.注册edit事件
                e.record.commit(); //前台的小红点会消失
        Ext.grid.plugin.RowEditing
             使用方法:(有Bug推荐4.0.1a版本还是不要用这个功能)
             Ext.create('Ext.grid.plugin.RowEditing', {
                    clicksToEdit: 1
             })                

（2）Ext.grid.plugin.DragDrop 表格拖拽
       主意:配置有变化
       viewConfig:{
          plugins:[
            Ext.create('Ext.grid.plugin.DragDrop', {
                ddGroup:'ddTree', //拖放组的名称
                dragGroup :'userlist', //拖拽组()名称
                dropGroup :'userlist'  //释放租名称
                enableDrag:true, //是否启用
                enableDrop:true
            })]
       }        
      处理事件
      listeners: {
        drop: function(node, data, dropRec, dropPosition) {
              var st = this.getStore();
              for(i=0;i<st.getCount();i++){
                  st.getAt(i).set('index',i+1);
              }
        }
      }        

（3）Ext.toolbar.Paging 分页组件

       //第一种常用分页
       dockedItems: [{
          xtype: 'pagingtoolbar',
          store: store,
          dock: 'bottom',
          displayInfo: true
      }],
    
      //第二种分页的形式(条状，拨动分页)
      Ext.Loader.setPath('Ext.ux', 'http://www.cnblogs.com/../extjs4/examples/ux');
      Ext.require([
          'Ext.ux.data.PagingMemoryProxy',
          'Ext.ux.SlidingPager'
      ]);    
      bbar: Ext.create('Ext.PagingToolbar', {
         pageSize: 10,
         store: store,
         displayInfo: true,
         plugins: Ext.create('Ext.ux.SlidingPager', {})  ---- 重点是这
      })    

（4）Ext.grid.property.Grid
      属性配置框面板
      当通过页面自动配置一些属性时候了可以考虑用
    
（5）列锁定
      {text:"age",dataIndex:'age',width:100,locked:true},类似于excel里的冻结功能

（6）复杂表头
       列里面又包含列(不能和字段过滤一起使用)
       columns：{
          text:'other',columns:[
            {text:"age",dataIndex:'age',width:100,locked: true},
            {text:"int",dataIndex:'index',width:100}]
        }

（7）字段过滤
    Ext.require([
        'Ext.ux.grid.FiltersFeature'
    ]);
    Ext.define("AM.class.filters",{
        alias: 'widget.filters',
        ftype: 'filters',
            encode: false, 
            local: true, 
            filters: [{
                    type: 'boolean',
                    dataIndex: 'visible'
                }
         ]
    })
    view层中
    features: [Ext.create("AM.class.filters")],
    列中添加配置{filterable: true,text:"age",dataIndex:'age',width:100,filter: {type: 'numeric'}}

Ext.define("AM.util.filters",{
 alias: 'widget.filters',
 ftype: 'filters',
        encode: false, 
        local: true, 
        filters: [{
                type: 'boolean',
                dataIndex: 'visible'
            }
     ]
})

 

Ext.define("AM.view.List",{
 extend:'Ext.grid.Panel',
 title : 'Grid Demo',//标题
 alias: 'widget.userlist',
 frame : true,//面板渲染
 width : 500,
 height: 380,
 columns : [ //列模式
    //{text:"Name",dataIndex:'name',width:100,locked:true},
    {text:"Name",dataIndex:'name',width:100},
    //{text:'others',columns:[
     {text:"age",dataIndex:'age',width:100,filterable: true,filter: {type: 'numeric'}},
     {text:"email",dataIndex:'email',width:250,
      field:{
       xtype:'textfield',
       allowBlank:false
      }
     },{
      text:'index',dataIndex:'index',width:100
     }     
    //]}
 ],
 features: [Ext.create("AM.util.filters")],
 tbar :[
    {xtype:'button',text:'添加',iconCls:'table_add'},
    {xtype:'button',id:'delete',text:'删除',iconCls:'table_remove'},
    {xtype:'button',text:'修改',iconCls:'table_edit'},
    {xtype:'button',text:'查看',iconCls:'table_comm'},
    {xtype:'button',text:'save',id:'save',iconCls:'table_comm'}
 ], 
 dockedItems :[{
    xtype:'pagingtoolbar',
    store:'Users',
    dock:'bottom',
    displayInfo:true,
    plugins: Ext.create('Ext.ux.SlidingPager', {}) 
 }],
 //plugins:[
//    Ext.create("Ext.grid.plugin.CellEditing",{
//     clicksToEdit : 2
//    })
//    Ext.create('Ext.grid.plugin.RowEditing', {
//              clicksToEdit: 1
//          })
 //],
 viewConfig:{
  plugins:[
         Ext.create('Ext.grid.plugin.DragDrop', {
          ddGroup:'ddTree', //拖放组的名称
             dragGroup :'userlist', //拖拽组名称
             dropGroup :'userlist',  //释放租名称
             enableDrag:true, //是否启用
             enableDrop:true
         })],
  listeners: {
         drop: function(node, data, dropRec, dropPosition) {
                var st = this.getStore();
                for(i=0;i<st.getCount();i++){
                    st.getAt(i).set('index',i+1);
              }
         }
     }          
 }, 
 //selType:'checkboxmodel',//设定选择模式
 //multiSelect:true,//运行多选
 store : 'Users',
 initComponent:function(){
  this.callParent(arguments);
 }
});

posted @ 2013-04-27 18:12 赵雪丹 阅读(40) 评论(0) 编辑
MVC学习
 



从这个图中我们可以很清楚的看到M 、V、C在ExtJS4.0里面所对应数据类型。

 靠右边是对应的代码结构。

 

 下描述一下这model、store、view、controller以及application这几者之间的关系。

 

（1）application：它是MVC的入口，用来告诉ExtJS到那里去找对应js文件以及启动加载controller与view连个模块的代码。

//打开动态加载js功能
 Ext.Loader.setConfig({
  enabled:true
 });
 Ext.application({
  name : 'AM',//应用的名字 (根) 利用MVC时这时定义的包路径需要与命名空间的层次关系一致
  appFolder : "app",//应用的目录
  launch:function(){//当前页面加载完成执行的函数
         Ext.create('Ext.container.Viewport', { //简单创建一个试图（填充整个浏览器）
          layout:'auto',//自动填充布局
             items: {
              xtype: 'userlist', //引用已经定义的别名进行初始化类
                 title: 'Users',
                 html : 'List of users will go here'
             }
         });
  },
  controllers:[
   'Users'
  ]
 });

（2）controller：这一层主要是用来处理业务逻辑，即View上一些动作所触发要执行的操作都在此实现。同时它也是关联view、store以及model的地方。

Ext.define('AM.controller.Users', {
    extend: 'Ext.app.Controller',
 init:function(){
  this.control({
   'userlist button[id=delete]':{
    click:function(o){
     var gird = o.ownerCt.ownerCt;
      var data = gird.getSelectionModel().getSelection();
      if(data.length == 0){
       Ext.Msg.alert("提示","您最少要选择一条数据");
      }else{
       //1.先得到ID的数据(name)
       var st = gird.getStore();
       var ids = [];
       Ext.Array.each(data,function(record){
        ids.push(record.get('name'));
       })
       //2.后台操作(delet)
       Ext.Ajax.request({
        url:'/extjs/extjs!deleteData.action',
        params:{ids:ids.join(",")},
        method:'POST',
        timeout:2000,
        success:function(response,opts){
         Ext.Array.each(data,function(record){
          st.remove(record);
         })
        }
       })
       //3.前端操作DOM进行删除(ExtJs)
      }
    }
   }
  });
 },
 views:[
  'List' //必须是文件名称
 ],
 stores :[
  "Users" //
 ],
 models :[
  "User" //这个就是store里面引用的model，所在js文件的名字，保持和定义model的类名一样。eg:AM.model.User
         //（这个主要是给store层用的，当store在当前缓存中找不到指定命名空间定义的model时，再去加载User.js文件，
         //再根据文件内容初始化定义model。如果缓存中已经有了model的定义，其实这个是可以不要的。）
      //同样views、store都可以通过各种各样的工厂生成，来去掉。
 ] 
});

（3）model、store：它们俩主要做为模型数据层。主要是给view层提供数据展示的。

//User数据集合
Ext.define('AM.store.Users', {
 extend: 'Ext.data.Store',
 model: 'AM.model.User',
 storeId: 's_user',
 proxy:{
     type:'ajax',
     url:'/extjs/extjs!getUserList.action',
     reader: {
         type: 'json',
         root: 'topics'
     },writer:{
   type:'json'
  }
 },
 autoLoad: true //很关键
});

（4）view：这一层主要负责页面展示，也是确确实实能看见的一层。

 

<SPAN style="COLOR: #008000">Ext.define("AM.view.List",{
 extend:'Ext.grid.Panel',
 title : 'Grid Demo',//标题
 alias: 'widget.userlist',//别名定义
 frame : true,//面板渲染
 width : 600,
 height: 280,
 columns : [ //列模式
    {text:"Name",dataIndex:'name',width:100},
    {text:"age",dataIndex:'age',width:100},
    {text:"email",dataIndex:'email',width:350,
     field:{
      xtype:'textfield',
      allowBlank:false
     }
    }
 ],
 tbar :[
    {xtype:'button',text:'添加',iconCls:'table_add'},
    {xtype:'button',id:'delete',text:'删除',iconCls:'table_remove'},
    {xtype:'button',text:'修改',iconCls:'table_edit'},
    {xtype:'button',text:'查看',iconCls:'table_comm'}
 ], 
 dockedItems :[{
    xtype:'pagingtoolbar',
    store:'Users',
    dock:'bottom',
    displayInfo:true
 }],
 plugins:[
    Ext.create("Ext.grid.plugin.CellEditing",{
     clicksToEdit : 2
    })
 ],
 selType:'checkboxmodel',//设定选择模式
 multiSelect:true,//运行多选
 store : 'Users',
 initComponent:function(){
  this.callParent(arguments);
 }
});


</SPAN>

posted @ 2013-04-27 18:11 赵雪丹 阅读(9) 评论(0) 编辑
Ext事件机制、AJax以及Ext常用类
1. Ext事件机制
 
 （1）事件的3中绑定方式
HTML/DHTML
DOM
EXTJS
 （2）Ext.util.Observable 事件的基类
 它为所有支持事件机制的extjs组建提供事件的支持。
 如果我们自己创建新的组建需要有时间的支持那么我们就继承它。
 事件的分类：
标准事件[键盘按钮按下,鼠标的单击双击,滑过滑动]。
业务事件[当面板收起的时候触发,当组建被销毁的时候触发,当每一个对象的属数值不为空的时候触发]。
 
 （3）addManagedListener 收管制的监听
 它是由调用的组建管理的,当组建执行了销毁命令的时候所有被组建管制的事件全部销毁。
 
 （4）relayEvents 事件的分发和传播(控制实现事件在不同空间或对象内的传播)
 比如说孩子喝完三鹿就去医院呀,老爸就要带着去医院
 
 （5）事件对象Ext.EventObject
 不是一个单例,不能被直接new出来,他会存活早事件处理的函数中
 
 （6）事件管理器Ext.EventManager
 它可以更方便的为页面元素绑定事件处理函数
 方法:addListener 为元素增减事件
 
2. Ext中的Ajax是 Ext.data.Connection的一个子类，提供了用简单的方式进行Ajax的功能实现
 
   （1）主要方法:
   abort : 终止一个没有完成Ajax请求
   isLoading : 判断指定的Ajax请求是不是正在运行
   paresStatus : 返回请求响应的代码
   request : 发送服务器请求
//json格式的数据
var jsondata = "{id:'01',name:'uspcat.com','age':26,email:'yunfengcheng2008@126.com'}";
//xml格式的数据
var xmldata = "<user><name>mlmlml</name><age>19</age></user>";
//构建Ext的Ajax请求
Ext.Ajax.request({
 url : 'person.jsp',
 method : 'POST',
 timeout :3000,
 
 //请求的参数值
 params:{id:'01'},

 //可以提交form表单，只需要写表单的ID
 form:"myform",
 
 //下面是两种不同格式的请求参数
 jsonData:jsondata,
 xmlData：xmldata,
 
 //一些操作的函数，第一个为响应的值，第二个参数是请求的参数值
 success :function(response , options){
  alert(eval(response.responseText)[0].name);
 },
 failure  :function(response , options){
  alert(response.responseText+" "+options)
 }
});

（2）Ext.ElementLoader:方便我们重新构建页面
   load方法
   startAutoRefresh 方法
//get通过dom元素的id方式获得的是元素的对象
//getCmp通过定义对象ID的方式获得的是定义的对象，而不是简简单单的元素了 
//getDom通过dom元素的id方式获得的是dom元素
var time = Ext.get("time").getLoader();

//ajax常用的局部改变元素的值
time.load({
 url:'/extjs/extjs!getTime.action',
 renderer:function(loader,response,request){
  var time = response.responseText;
  Ext.getDom("time").value = time;
 }
});
//给元素设置定时的axja请求方式
i.startAutoRefresh(1000,{
 url:'/extjs/extjs!getI.action',
 renderer:function(loader,response,request){
  var i = response.responseText;
  Ext.getDom("i").value = i;
 }   
});

3. Ext以及core包下面的Domhelper、Element类。
 
  （1）Ext.core.Element
  API解释
  他是组建和控件的基础
  他对一个DOM对象的封装(Document Object Model)
  a、如何得到Element
   Ext.core.Element.fly(String/HTMLElement el, [String named] ) : Element
   Ext.get(Mixed el) : Element
  b、Element 相关方法
   addClsOnClick( String className ) : Ext.core.Element。
   addClsOnOver( String className ) : Ext.core.Element。
   addKeyMap( Object config ) : Ext.util.KeyMap。
   addKeyListener( Number/Array/Object/String key, Function fn, [Object scope] ) : Ext.util.KeyMap。
   appendChild( String/HTMLElement/Array/Element/CompositeElement el ) : Ext.core.Element
   createChild( Object config, [HTMLElement insertBefore], [Boolean returnDom] ) : Ext.core.Element。
  （2）Ext.core.DomHelper
  API解释
   他可以很容易的操作页面的HTML.和DOM元素
  append( Mixed el, Object/String o, [Boolean returnElement] ) : HTMLElement/Ext.core.Element--------追加一个孩子。
 
  applyStyles---为元素添加样式 eg：Ext.core.DomHelper.applyStyles(Ext.get("p1"),"color:red");
 
  //下面两个是被当做兄弟追加的
  insertAfter( Mixed el, Object o, [Boolean returnElement] ) : 
  insertBefore( Mixed el, Object/String o, [Boolean returnElement] ) :
 
          //创建dom结构，通过给的标签字符串
  createDom( Object/String o ) : HTMLElement
  eg：var html = Ext.core.DomHelper.createDom("<h1>hello</h1>");
 
  （3）Ext
  //方法是执行在文件加载完之后
  onReady( Function fn, Object scope, Boolean withDomReady, Object options ) : void
  get()//不在多说
  query( String path, [Node root] ) : Array
   http://www.w3school.com.cn/xpath/xpath_axes.asp
   语法看 Ext.DomQuery
  getCmp( String id ) : void---返回组建管理器管理的ID组件
  isEmpty( Mixed value, [Boolean allowEmptyString] ) : Boolean
  namespace( String namespace1, String namespace2, String etc ) : Object
  each( Array/NodeList/Mixed iterable, Function fn, Object scope, Boolean reverse ) : Boolean
  apply( Object object, Object config, Object defaults ) : Object
  encode( Mixed o ) : String
  select( String/Array selector, [Boolean unique], [HTMLElement/String root] ) 
  typeOf( Mixed value ) :判断参数是一个什么样的类型，返回的是字符串，eg：string、function 
//这个是直接到页面中获得元素的对象
var div01 = Ext.core.Element.fly("div01");
//鼠标滑过的时候增加一个样式滑出的时候移除样式,值是样式的名称
div01.addClsOnOver("divC");
//这个是直接到Ext.ComponentManagerMap中拿，没有的话，就用第一个到页面中拿，再返回
var input01 = Ext.get("input01");
   
var fn1 = function(){
 alert("单击B按钮调用这个函数")
}
//给一个输入框添加键盘B键响应功能
//key是你要触发的那个键，ctrl是否需要与ctrl键结合，fn是触发函数
input01.addKeyMap({key:Ext.EventObject.B,ctrl:false,fn:fn1,scope:input01});
//和上面一本一样，只是添加更加复杂的，处理起来更加方便
/*第一个触发条件的参数是一个对象(条件可以进行组合):
  {key: (number or array), shift: (true/false), ctrl: (true/false), alt: (true/false)}*/
//第二个是触发函数fn
input01.addKeyListener({key:Ext.EventObject.X,ctrl:true},function(){
 alert("单击ctrl+x")
},input01);

function createChild(){
 var el = document.createElement("h5");
 el.appendChild(document.createTextNode("我是被追加的"));
 return el;
}
Ext.get("div02").appendChild(createChild());
//通过构造对象，来创建DOM
Ext.getBody().createChild({
 tag:'li',
 id:'item1',
 html:'我是第一个个节点'
});

3. ExtJS4.0中util包里面的一些工具类用法。
 
 （1）.Ext.util.CSS
         Ext.util.CSS.createStyleSheet(".c{color:red}","red");
         创建一个样式表，类似于你在css文件里面定义的内容。

         Ext.get("d1").addClsOnOver("c");
         在鼠标滑过时，动态的给某个元素对象的class赋值为刚刚定义的名为c样式表。

         Ext.util.CSS.getRule(".c",true);
         获得当前的样式的对象，可以从这个对象获得一些你需要的参数。        
 
         Ext.util.CSS.swapStyleSheet("sheet1","1.css");第一个参数是当前引用样式的ID，第二个是也是的URL路劲
         动态的切换，你所引用的样式表。（即假如你还有一个样式表2.css，里面1.css定义的样式名称一样，这时你可以用这个函数Ext.util.CSS.swapStyleSheet("sheet2","2.css")把目前引用1.css切换成2.css。）
         一般用于不同风格的样式切换。
         注意ID唯一。

         Ext.util.CSS.removeStyleSheet("red");
         移除当前，页面已经定义了的样式，传入样式的ID即可。

         Ext.util.CSS.updateRule(".c","color","#990055");
         更新某个已经定义了样式中的某个属性的值。

 （2）.Ext.util.ClickRepeater  click的转发器是Ext.util.Observable的子类
Ext.onReady(function(){
 //控制元素在指定时间内被单击(当前元素没有数失去焦点)
 var cl = new Ext.util.ClickRepeater(Ext.get("b4"),{
  delay:3000,//首次单击时候的间隔事件
  interval:4000,//发生首次重复事件调用之后每一次事件的相隔时间
  stopDefault:true,//停止这个el上得默认单击事件
  handler:function(){
   alert("单击我");
  }
 });
 //第一次单击马上会触发事件 如果不去点击其他的元素那么3秒或就会自定执行第二次
 //一或会以4秒的间隔执行相应的程序
})
3）.Ext.util.DelayedTask 代替setTimeout

 （4）.Ext.util.Format 格式化的公共类
         用于一些字符串常用操作、日期以及小数的格式化等。

 （5）.Ext.util.MixedCollection 集合类
         强大之处在于它同时可以存放各工种各样的对象。并且提供很多操作集合里对象的方法。

 （6）.Ext.util.TaskRunner 模拟线程控制
         模拟多线程的实现。
         
Ext.onReady(function(){
 var runner = new Ext.util.TaskRunner();
 var task = {
  run:function(){
   Ext.getDom("t1").value = Ext.util.Format.date(new Date(),"Y-m-d-s");
  },
  interval:1000
 }
 runner.start(task);
 Ext.get("b6").on("click",function(){
 
  runner.stop(task);
 })
})
posted @ 2013-04-27 18:07 赵雪丹 阅读(18) 评论(0) 编辑
Ext4.0新特性以及常用数据处理功能
1. extjs4.0对原生javaScript功能进行了扩展（API中的Utilities模块中的NativeExtensions）

 

    Utilities：常用的一些工具处理类
    Native Extensions
       Ext.Array
       Ext.Number
       Ext.Object
       Ext.String
       Ext.JSON
       Ext.Date
       Ext.Function

具体扩展了那些，请参照具体的API说明，扩展的原理eg：

var Person = {name:'yfc',age:26};
    //alert(Person['name']);
    //extjs4.0提供getKey的函数
    //alert(Ext.Object.getKey(Person,'yfc'));
    Object.prototype.getValue = function(key,defValue){
        if(this[key]){
            return this[key];
        }else{
            return defValue;
        }
    }
alert(Person.getValue("email","pcat@126.com"));
//由于给Object的原型加上了一个getValue的函数，这样所有的对象（都继承Object）默认都会拥有这个函数。
 

2. 事件机制与新特性

 

   （1）给对象加事件：

Ext.get("元素ID").on("click",function(){
      //函数处理部分
});

（2）新特性：create与define（extend 、requires、config、mixins、alias以及statics ）。

create：在ExtJs4.0中你可以通过new方式也可以用create的方式得到一个对象的实例，在4.0版本中建议用create的方式来创建实例，这样ExtJS会对创建的实例进行统一管理。
//create第一个参数为类路径，第二个参数为该类的一些初始化参数值（以对象的形式传递）
var win = Ext.create('Ext.window.Window',{
     width:400,
     height:300,
     title:'uspcat'
       });

win.show();

alias：别名的作用，可以把一个对象的内部函数暴漏处理啊，给其他对象直接调用。eg：
var o = {
 say : function(){
  alert(11111);
        }
}

//通过o.say()调用函数

var fn = Ext.Function.alias(o,'say');
fn();//通过别名的方式我们就可以直接调用fn()等于o.say()。

define：是用来定义一个类的，eg：
//create第一个参数是类的全路径，第二个参数则是类的内容
Ext.define('Bmsys.ml.Window', {
 extend:'Ext.window.Window',
        title: 'Window',
        closeAction: 'hide',
        width: 380,
        height: 300,
        resizable: false,
        modal: true,
        //定义一些自己的扩展参数
        myTitile: 'myWindow',
        setTitle: function(){
              this.title = this.myTitle;
        }
        
        //初始化的方法(类似java中的构造方法)
        initComponent: function(){
              this.setTitle();
              this.callParent(arguments);
        }
&nbsp;});

var win = Ext.create('Bmsys.ml.Window',{
                   titile: 'youWindow';
             }
);

win.show();//此时创建出来窗体的标题是myWindow，说明创建时，传入的初始化参数比构造器先执行。

注意：属性只能在define时定义，不能通过win.myHeight = function(){...}添加属性。

 

requires: JS的异步加载（按需加载），解决了网络js文件大而造成页面打开慢得问题，只有当成需要用到这个类时Ext才去到后台加载包含这个类的js文件；在这里就要，要求我们在写js类的时候要尽量的模块化，一个类就是一个js文件，而且类名与js文件名一致，命名空间定义规范。
//这时候要启用自动加载
Ext.Loader.setConfig({
 enabled:true,
 paths:{
  myApp:'js/Bmsys/ml' //js文件相对路径，需要与命名空间保持一致
 }
});

//这时候只要保证Window.js放在js/Bmsys/ml这个目录下命名空间为Bmsys.ml.Window就可以了。
//这时就不需要在JSP文件中引入Window.js,等到下面的程序被执行时，才会根据命名空间去到后台加载Window.js。
//原理就是通过命名空间与文件路径，拼接好后通过写入<script>标签的方式加载。
var win = Ext.create('Bmsys.ml.Window',{
                   titile: 'youWindow',
                   requires: ['Bmsys.ml.Window']
             }
).show();

config: 这个属性就是把你定义类的属性自动的加上get、set方法，省去自己去写的麻烦事。
Ext.define('Bmsys.ml.Window', {
 extend:'Ext.window.Window',
        title: 'Window',
        width: 380,
        height: 300,
        //定义一些自己的扩展参数
        myTitile: 'myWindow',
        config: {
              myHeight : 800
        }
 });

var win = Ext.create('Bmsys.ml.Window',{});

alert(win.getMyTitle());//报错，没有定义getMyTitle函数
alert(win.getMyHeight());//正常弹出值为800

//放在config里面定义的属性，Ext会自动给这个属性加上get、set方法。

mixins：类的混合（多继承实现），因为我们在用define定义类的时候，extend只能继承一个类。为了拥有其它类定义好的方法及功能，我们可以通过类的混合来实现。
Ext.define("say",{
 cansay:function(){
  alert("hello");
 }
})
Ext.define("sing",{
 sing:function(){
  alert("sing hello 123");
 }
})

//通过类的混合，就可以轻松拥有上面两个类里面的函数。
Ext.define('user',{
 mixins :{
  say : 'say',
  sing: 'sing'
 }
});

var u = Ext.create("user",{});
u.cansay();//say类里面的方法
u.sing();//sing类里面的方法

static：类似java中静态，我们可以定义一些静态的属性以及方法，通过类名'.'的方式来访问。
Ext.define('Computer', {
     statics: {
         factory: function(brand) {
             // 'this' in static methods refer to the class itself
             return new this(brand);
         }
     },
     constructor: function() { ... }
});
//直接通过类名'.'的方式访问静态方法
var dellComputer = Computer.factory('Dell');

3. 数据模型model（MVC中的M层）
 
    数据模型对真实世界中对事物在系统中的抽象，extjs4.0中的mode相当于DB中的table 或 JAVA 中的Class。
 
（1）model的几种创建以及实例的方法。
//我们利用Ext.define来创建我们的模型类
//DB table person(name,age,email)
Ext.define("person",{
 extend:"Ext.data.Model",
 fields:[
  {name:'name',type:'auto'},
  {name:'age',type:'int'},
  {name:'email',type:'auto'}
 ]
});
//定义的时候，不需要每次写extend:"Ext.data.Model"
Ext.regModel("user",{
 fields:[
  {name:'name',type:'auto'},
  {name:'age',type:'int'},
  {name:'email',type:'auto'}
 ]
});
//实例化我们的person类
//1.new关键字
var p = new person({
 name:'uspcat.com',
 age:26,
 email:'yunfengcheng2008@126.com'
});
//alert(p.get('name'));
var p1 = Ext.create("person",{
 name:'uspcat.com',
 age:26,
 email:'yunfengcheng2008@126.com'
});
//alert(p1.get('age'));
var p2 = Ext.ModelMgr.create({
 name:'uspcat.com',
 age:26,
 email:'yunfengcheng2008@126.com'
},'person');
alert(p2.get('email'));

//实例不能直接通过getName得到类名，因为这个方法是类的 class object.getClass.getName
//alert(p2.getName());

//通过类.getName可以获得类名，因为person是模型类的定义，而不是实例
alert(person.getName());

（2）model模型Validations以及通过修改原始类来实现自定义验证器。
//在校验之前，修改原始类里属性的默认值
Ext.data.validations.lengthMessage = "错误的长度";

Ext.onReady(function(){
 //通过apply方法来在原始的校验器类上扩展我们自定义验证机制的的一个新的验证方法
 Ext.apply(Ext.data.validations,{
     //自定义的校验类型函数
  age:function(config, value){
   var min = config.min;
   var max = config.max;
   if(min <= value && value<=max){
    return true;
   }else{
    this.ageMessage = this.ageMessage+"他的范围应该是["+min+"~"+max+"]";
    return false;
   }
  },
  ageMessage:'age数据出现的了错误'
 });
 //定义一个带有校验的模型类 
 Ext.define("person",{
  extend:"Ext.data.Model",
  fields:[
   {name:'name',type:'auto'},
   {name:'age',type:'int'},
   {name:'email',type:'auto'}
  ],
  validations:[
      //type的值就是Ext.data.validations里方法名称
   //field是你要校验字段名
   //field后面的参数就是名称等于type值的函数的参数。
   {type:"length",field:"name",min:2,max:6},
   {type:'age',field:"age",min:0,max:150}
  ]
 });
 var p1 = Ext.create("person",{
  name:'uspcat.com',
  age:-26,
  email:'yunfengcheng2008@126.com'
 }); 
 
 //通过validate()可以得到数据校验的错误集合
 //每个error里面含有两个属性(field---校验字段的名,message---校验函数返回的错误信息)
 var errors = p1.validate();
 var errorInfo = [];
 errors.each(function(v){
  errorInfo.push(v.field+"  "+v.message);
 });
 alert(errorInfo.join("\n"));
});

注意：自定义的校验器，你可以通过利用apply方法来为原始的类增加，也可以通过继承的方式实现。
 
 （3）数据代理proxy：就是通过与后台的交互来完成数据模型，数据填充的服务类。
Ext.define("person",{
 extend:"Ext.data.Model",
 fields:[
  {name:'name',type:'auto'},
  {name:'age',type:'int'},
  {name:'email',type:'auto'}
 ],
 //通过代理从后台获取数据（数据要与model的fields里面的字段相对应）
 proxy:{
  type:'ajax',
  url:'person.jsp'
 }
});
var p = Ext.ModelManager.getModel("person");
//通过load方法来触发proxy加载数据
p.load(1, {
 scope: this,
 //record.data就是加载进来的一个数据实例对象
 success: function(record, operation) {
  alert(record.data.name)
 }
});
（4）Molde的一对多和多对一关系。
//类老师
Ext.regModel("teacher",{
 fideld:[
  {name:'teacherId',type:"int"},
  {name:'name',type:"auto"}
 ],
 //建立老师与学生的1对多关系
 hasMany:{
      //所关联的模型
   model: 'student',
   name : 'getStudent',
   //关系字段
   filterProperty: 'teacher_Id'
 }
});
//学生
Ext.regModel("student",{
 fideld:[
  {name:'studentId',type:"int"},
  {name:'name',type:"auto"},
  {name:"teacher_Id",type:'int'}
 ]
});
//假设t是老师的一个实例，就可以通过t.students 得到子类student的一个store数据集合
3. 数据代理Proxy
 
    数据代理proxy是进行数据读写的主要途径,通过代理操作数据进行CRUD。
 
   CRUD的 每一步操作都会得到唯一的Ext.data.Operation实例，它包含了所有的请求参数。通过构造Ext.data.Operation来传入请求参数。
 
  （1）数据代理proxy目录结构
 
   Ext.data.proxy.Proxy 代理类的根类(它分为客户端(Client)代理和服务器代理(Server))
A、Ext.data.proxy.Client 客户端代理
Ext.data.proxy.Memory 普通的内存代理。
Ext.data.proxy.WebStorage 浏览器客户端存储代理（cookie操作）。
Ext.data.proxy.SessionStorage 浏览器级别代理，浏览器关闭数据消失。
Ext.data.proxy.LocalStorage 本地化的级别代理，数据可以保存在浏览器文件里，浏览器关闭后，下次打开还在(不能夸浏览器)。
 
B、Ext.data.proxy.Server 服务器端代理
Ext.data.proxy.Ajax 异步加载的方式。
Ext.data.proxy.Rest 一种特使的Ajax。
Ext.data.proxy.JsonP 跨域交互的代理（请求的数据url不在同域内）， 跨域是有严重的安全隐患的，extjs的跨域也是需要服务器端坐相应的配合。
Ext.data.proxy.Direct 命令.
 
4.  工作在Proxy下的读写器
 
   （1）Reader : 主要用于将proxy数据代理读取的数据按照不同的规则进行解析,讲解析好的数据保存到Model中
            结构图
             Ext.data.reader.Reader 读取器的根类
            Ext.data.reader.Json JSON格式的读取器
            Ext.data.reader.Array 扩展JSON的Array读取器
            Ext.data.reader.Xml XML格式的读取器
var userData = {
 //读写器默认读取的记录总数的属性
 //total : 200,
 
 //采用我们自定义的变量来标识总条数，这时后需要在读写器中配置total所对应我们自定义的变量
 count:250,
 user:[{auditor:'yunfengcheng',info:{
  userID:'1',
  name:'uspcat.com',
  orders:[
   {id:'001',name:'pen'},
   {id:'002',name:'book'}
  ]
 }}]
};
//model
Ext.regModel("user",{
 fields:[
  {name:'userID',type:'string'},
  {name:'name',type:'string'}
 ],
 //配置一对多的关系
 hasMany: {model: 'order'}
});
Ext.regModel("order",{
 fields:[
  {name:'id',type:'string'},
  {name:'name',type:'string'}
 ],
 //配置多对一的关系
 belongsTo: {type: 'belongsTo', model: 'user'}
});
var mproxy = Ext.create("Ext.data.proxy.Memory",{
 model:'user',
 data:userData,
 //读写时的参数配置
 reader:{
  type:'json',//读取的类型（json/xml/array）
  root:'user',//指定读取开始的根节点
  implicitIncludes:true,//是否级联读取关联的子节点（一对多的关系中体现）
  totalProperty:'count',//配置我们返回的总条数变量名称
  record : 'info'//服务器返回的数据可能很复杂,用record可以筛选出有用的数据信息,装在带Model中，其它的参数忽略。
 }
});
//用内存代理来读取数据，其它的方式一样
mproxy.read(new Ext.data.Operation(),function(result){
 var datas = result.resultSet.records;
 alert(result.resultSet.total);
 Ext.Array.each(datas,function(model){
  alert(model.get('name'));
 });
 var user = result.resultSet.records[0];
 var orders = user.orders();
 orders.each(function(order){
  alert(order.get('name'))
 });     
})
（2）Writer ：把前台的js对象数据按照不同的方式写到后台。
           结构图
            Ext.data.writer.Writer
            Ext.data.writer.Json 对象被解释成JSON的形式传到后台
            Ext.data.writer.Xml  对象被解释成XML的形式传到后台
Ext.regModel("person",{
 fields:[
  'name','age'
 ],
 proxy :{//在proxy下，你可以配置reader（读），同样也可以配置writer（写）
  type:'ajax',
  url:'person.jsp',
  writer:{//配置一些写的参数
   //type:'json'
   type:'xml'  //把js对象以xml的方式，传入后台
  }
 }
});
Ext.ModelMgr.create({
 name:'uspcat.con',
 age:1
},'person').save();
5. Store : 是一个存储数据对象Model的集合缓存,它可以为extjs中的可视化组建提供数据源                     (GridPanel,ComboBox)等。（在ExtJS中占有重要的地位，它也属于Model层）

（1）类结构
          Ext.data.AbstractStore
        Ext.data.Store  没有特殊情况这个类就可以满日常的开发了
      Ext.data.ArrayStore
      Ext.data.DirectStore
      Ext.data.ArrayStore  内置辅助的类
      Ext.data.JsonStroe  内置辅助的类
   Ext.data.TreeStore
 
  （2）Ext.data.Store 使用
  参数
       autoLoad(Boolean/Object) ： 自动加载数据，自动调用load
       data(Array) ： 内置数据对象的数组，初始化的是就要被装在
       model(Model) ： 数据集合相关的模型
       fields(Field) ：字段的集合，程序会自动生成对于的Model，这样我们就不需要再定义model。
  方法
       each( Function f, [Object scope] ) : void 变量数据中的Model
Ext.define("person",{
 extend:'Ext.data.Model',
 fields:[
  {name:'name'},
  {name:'age'}
 ],
 proxy:{
  type:'memory'
 }
})
var s = new Ext.data.Store({
 //model:'person',
 data:[
  {name:'uspcat.com',age:1},
  {name:'yfc',age:26}
 ],
 //有了fields，我们就不需要在单独定义Model并且引用
 fields:[
  {name:'name'},
  {name:'age'}
 ],
 //通过data属性，请偶们已经能够把数据初始化好了
 //proxy是动态的区后台去数据   
 //proxy:{
 // type:'ajax',
 // url:'person.jsp'
 //}   
 //autoLoad:true
});
s.load(function(records, operation, success){
 //遍历
 Ext.Array.each(records,function(model){
  alert(model.get('name'));
 });
 //过滤出字段name='yfc'
 s.filter('name',"yfc");
 s.each(function(model){
  alert(model.get('name'));
 });
 //通过正则来查找数据集里面的记录，返回该记录的索引   
 var index = s.find('name','yfc',0,false,true,false);
 alert(s.getAt(index));//当前的Model对象
});
posted @ 2013-04-27 18:06 赵雪丹 阅读(28) 评论(0) 编辑
EXTJS的基本概念
1. 组件component : 能够以图形化形式呈现界面的类，其中还可以分为容器组件与元件组件。

容器组件:能够包含其它容器或者元件组件的类，其是进行单元化组件开发的基础
元件组件：能图形化形式表现一个片面功能的组件，其不仅在实现了原有传统WEB程序的现有组件，而且还扩展了许多实用的组件，如刻度器、日历、树形列表等。
2. 类

    提供功能的非图形可形的类，它们为图形类提供了有力的支持

    按其功能可分为：数据支持类(Data)、拖放支持类（DD）、布局支持类（layout）、本地状态存储支持类（state）、实用工具类（Util）。

    密封类：不能被扩展的类

    原型类：扩展了javascript标准类库中的类

 

3. 方法

    作为类的功能体现，能够产生改变对象本身产生变化的直接因素

    方法按访问形式可分为公有方法与私有方法。但由于javascript从原理上根本不支持这种结构，因此在EXTJS中，私有与公有方法完全凭借着用户自觉，没有像JAVA那样的强制性。

 

4. 事件

    由类定义的，并且可以在类对象自身状态发生改变的触发。

    只有被定阅的事件才会有效

    如果不需要此事件，应该进行退定，增强程序的执行效率。

 

5. 配置选项

    用以初始化一个EXTJS类对象的手段

    注意，配置选项并不一定就是属性，总算是属性，也有可能出现属性返回的类型与你当初指定的配置选项类型不一致的情况。

 

6. 属性

    能够在程序运行期间，能够被访问，用以了解当前类对象的状态。

    在实际的编程中，EXTJS的属性设置，比较差劲，需要通过了解其源代码，才能了解各种实用属性的用处。

 

7. 命名空间

    能够将编写好的EXTJS类进行有效组织的手段。

    这个也是EXTJS能够称之为优秀AJAX框架的特征之一。

posted @ 2013-04-27 18:03 赵雪丹 阅读(9) 评论(0) 编辑
Extjs4布局layout
posted @ 2013-04-27 18:02 赵雪丹 阅读(19) 评论(0) 编辑
ExtJs4.0 Grid分頁詳解
網上有好多關於Grid分頁的，各種語言都有，但大部分都是一樣的，都只是講了Grid分頁的語法，很少說到如何和後臺的數據庫交互，查出數據，同樣剛接觸Extjs，希望和菜鳥級別的兄弟姐妹們，共同進步。

前臺代碼：

var itemsPerPage = 2;
var store = Ext.create('Ext.data.Store', {
autoLoad: { start: 0, limit: itemsPerPage },
fields: ['AA001', 'AA002', 'AA003', 'AA004', 'AA005', 'AA006', 'AA007'],
pageSize: itemsPerPage,
proxy: {
type: 'ajax',
url: 'HandlerFun.ashx?Type=Support',
reader: {
type: 'json',
root: 'rows',
totalProperty: 'total'
}
}

});


var gridHeight = document.body.clientHeight * 19;


Ext.ClassManager.setAlias('Ext.selection.CheckboxModel', 'selection.checkboxmodel');

var grid = Ext.create('Ext.grid.Panel', {
title: '',
renderTo: "grid",
autoWidth: true,
height: gridHeight,
frame: true,
store: store,
multiSelect: false,
selModel: { selType: 'checkboxmodel' }, //在首列實現checkbox，僅此在首列
columns: [



 


      



