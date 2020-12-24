3.在项目中使用React  
20201124

```
1.引入相关的包
“npm i react react-dom -S”

2.
//1.这两个导入的时候，接收的成员名称，必须这么写
import React from 'react';
import ReactDOM from 'react-dom';

//2.创建虚拟DOM元素
// 参数1：创建元素的类型，字符串，表示元素名称
// 参数2：是一个对象或null，表示当前这个DOM元素的属性
// 参数3：子节点 (包括其他虚拟DOM 或 文本子节点)
// 参数n:
const myh1 = React.createElement('h1' , { id:'h1id' } , 'this is h1' );

//3.使用使用ReactDOM把虚拟DOM渲染到页面上
// 参数1：渲染的那个虚拟DOM
// 参数2：指定页面的容器,应该是DOM元素
ReactDOM.render(myh1,document.getElementById('app'))

//4.在index.html中加入
    <div id="app">
    </div>

3.省略jsx文件后缀名
打开webpack.config.js,并在导出的配置对象中，新增如下节点
   resolve : {
        extensions : ['.js','.jsx','.json'] //表示这几个文件的后缀名，可以省略不写
    }

4.配置@路径，在resolve中加入alias,如
    resolve : {
        extensions : ['.js','.jsx','.json'], //表示这几个文件的后缀名，可以省略不写
        alias : {
            '@' : path.join(__dirname, './src')
        }
    }

5.引入React-Route包
npm i react-router-dom -S

6.引入类型校验的包
npm i prop-types -S

7.引入Redux包
npm i redux -S

8.引入React-Redux包
npm i react-redux -S

9.引入Redux-Thunk包
npm i redux-thunk -S

10.引入Axios包
npm i axios -S
```