mistake-of-using-zm-fe-x
========================

记录一些使用zm-fe-x项目的一些坑


2014.12.12
  1.common为每个站点的公用文件夹，home为zmlearn站点，新开站点或则是新开zmlearn的子站点需重开文件夹。
  2.整个项目以widget模块为单位，以模块开发。
  3.根目录下的widget文件夹的每个模块（例如nav模块），当引用该模块下的tpl文件，fisp会自动加载该模块的css和js文件，
    js文件只是包装成amd模式，还需在tpl文件中调用require('home:widget/nav/nav.js');才能执行。
  
