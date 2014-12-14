mistake-of-using-zm-fe-x
========================

#记录一些使用zm-fe-x项目的一些坑


##2014.12.12

  1.common为每个站点的公用文件夹，home为zmlearn站点，新开站点或则是新开zmlearn的子站点需重开文件夹。
  
  2.整个项目以widget模块为单位，以模块开发。
  
  3.根目录下的widget文件夹的每个模块（例如nav模块），当引用该模块下的tpl文件，fisp会自动加载该模块的css和js文件，
    js文件只是包装成amd模式，还需在tpl文件中调用require('home:widget/nav/nav.js')才能执行。
    
##2014.12.13

  1.官方文档对page对应的静态文件的位置有三种不同的说法
  
    第一种：
    
    页面(page)：存放在 模块根目录/page 下，url访问路径为/模块名/page/页面名，
    
    例如path_to_user_module/page/view.tpl，访问url为：/user/page/view。页面静态资源存储的位置为：

    tpl ：path_to_module/page/页面名.tpl
    
     js ：path_to_module/page/页面名.js
     
    css ：path_to_module/page/页面名.css
    
    第二种：
    
        ---module1 //module1子系统
    |     |      |---test
    |     |      |---config
    |     |      |---page
    |     |            └── index.tpl
    |     |      |---widget
    |     |      |---static
    |     |      |     └── index //index.tpl模板对应的静态资源
    |     |      |          └── index.js
    |     |      |          └── index.css
    |     |      |---fis-conf.js //fis配置文件
    
    第三种：
    
    页面模板静态资源对应页面模板的同名静态资源，FIS-Plus会在页面自动进行加载，用户不需要在页面中声明加载。
    
    tpl ：模板根目录/page/页面名.tpl
    
    js ：模板根目录/page/页面名/页面名.js
    
    css ：模板根目录/page/页面名/页面名.css
    
    鼎爷答复：页面级别的静态资源没什么规则，一般会放到static目录下。另外文档上面的错误是历史遗留问题，感谢反馈，修复后会在
    
    http://oak.baidu.com 下进行展示。
    
    2.在widget下的js组件require不了css和tpl文件
    
    3.在css文件中依赖其他css时，可用以下方法。当时我的坑是在less文件加以下代码，但是由于less文件编译后把注释去掉了，所以一直没有
    
    获取依赖成功。
    
    /**
    
     * demo.css
     
     * @require reset.css
     
     */
##2014.12.14
  1.用于测试的数据文件（包括模拟ajax异步请求的处理数据文件）都需要放在模板根目录下的test文件夹，同时需要在server.conf文件中添加
  规则。
  
  例子：rewrite ^\/api\/validatemobile\?mobile=\d{11,11}$ test/home/api/validatemobile.json
                                            |                            |     
                                            
                                            |--这是匹配某个请求路径      |--这是该请求的response数据,注意：该数据的
                                            
                                            |--的正则表达式              |--地址应该为release后服务器上对应的地址
  
  
  
