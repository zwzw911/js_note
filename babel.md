#####1. 安装
安装所有插件
`npm install babel-cli babel-core babel-polyfill es2015 babel-stage-0 --save-dev`  
babel-cli: cli命令。  
babel-core: node api和钩子（require("babel-core/register")，之后调用的js文件会被自动转换成ES5）。  
babel-polyfill: 创建出一个ES2015的运行环境（所有ES2015的功能都可用？例如，如果没有这个插件，那么async解析后无法运行；安装后才能运行）。  

#####2. 使用
在主程序添加`require("babel-polyfill");`和`require("babel-core/register")`，以便实现此
