#####1. 安装
安装所有插件
`npm install babel-cli babel-core babel-polyfill es2015 babel-stage-0 --save-dev`  
babel-cli: cli命令。  
babel-core: node api和钩子（require("babel-core/register")，之后调用的js文件会被自动转换成ES5）。  
babel-polyfill: 创建出一个ES2015的运行环境（所有ES2015的功能都可用？例如，如果没有这个插件，那么async解析后无法运行；安装后才能运行）。  

#####2. 使用
在主文件添加`require("babel-polyfill");`和`require("babel-core/register")`，以便实现此文件中调用的js文件（require，ES6的import好像尚不支持），会自动调用ES5的格式的文件（即转换后的文件）。  
*例如, 要执行的文件中require('a.js')，则调用时，实际调用的是a-complicated.js*。  
注：不会影响部署，因为部署时，要把xx-compiled.js**更名**成xx.js，即把complied去掉。如此，a.js就有了。  


