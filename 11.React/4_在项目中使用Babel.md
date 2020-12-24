4.在项目中使用Babel  
20201125

```
1.
安装babel插件
“npm i babel-core babel-loader babel-plugin-transform-runtime -D”
“npm i babel-preset-env babel-preset-stage-0 -D”

2.
安装能够识别转换jsx语法的包
“npm i babel-preset-react -D”

3.
在webpack.config.js中添加babel-loader配置项
        rules : [ //第三方配置规则
            {
                test : /\.js|jsx$/,
                use : 'babel-loader',
                exclude : /node_modules/ //exclude必须要加
            }
        ]

4.
添加.babelrc配置文件(它是json类型的-即不能写单引号，和不能写注释)
{
    "presets": ["env","stage-0","react"],
    "plugins" : ["transform-runtime"]
}
```
