1.新建WebPack项目  
20201119

1
进入项目目录, 快速初始化， 会创建包管理文件package.json
“npm init -y”

2
在项目根目录创建src目录和dist目录

3
在src下建index.html

4
在src下建main.js, 这是WebPack打包入口文件

5
安装Webpack, “npm i webpack -D”

6
安装Webpack-cli, “npm i webpack-cli -D”

7
```
webpack.config.js是配置文件
module.exports＝｛｝
```

Webpack4和5中，默认的打包入口路径是src\index.js

8
```
安装”npm i webpack-dev-server -D”,来实现自动编译
在package.json的script中加入"dev": "webpack-dev-server"
运行 ”npm run dev”
可以配置以下参数
"dev": "webpack-dev-server --port 3000 --hot --host 127.0.0.1"

webpack-dev-server的作用是把生成的main.js放到内存中
```

9
安装“npm i html-webpack-plugin -D”, 来实现把页面生成到内存中去, 并把打包好的js文件注入到页面中去

10
webpack --display-modules --sort-modules-by size  
这个命令可以在打包的时候显示所有打包的模块以及他们的体积，并且按照体积从小到大进行排序  
用于:分析巨大的bundle.js，看看里面都有啥，各个部分占据的体积是多少  

总结  
```
npm init -y
npm i webpack@4.44.2 -D
npm i webpack-cli@3.3.12 -D
npm i webpack-dev-server@3.11.0 -D
npm i html-webpack-plugin@4.5.0 -D

npm i react@17.0.1 react-dom@17.0.1 -S
npm i react-router-dom@5.2.0 -S
npm i prop-types@15.7.2 -S
npm i axios@0.21.0 -S

npm i babel-core@6.26.3 babel-loader@7.1.5 babel-plugin-transform-runtime@6.23.0 -D
npm i babel-preset-env@1.7.0 babel-preset-stage-0@6.24.1 -D
npm i babel-preset-react@6.24.1 -D
npm i babel-plugin-import@1.13.3 -D

npm i redux@4.0.5 -S
npm i react-redux@7.2.2 -S
npm i redux-thunk@2.3.0 -S

npm i style-loader@2.0.0 css-loader@5.0.1 -D
npm i antd@3.17.0 -S
npm i url-loader@4.1.1 -D
npm i file-loader@6.2.0 -D
npm i sass-loader@10.1.0 node-sass@5.0.0 -D
```

v1-20201224