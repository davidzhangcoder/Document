5.在项目中使用CSS, 和UI库  
20201128

```
css模块化，只针对 类选择器 和 Id选择器 生效
css模块化, 不会将标签选择器模块化
字体文件用url-loader处理

1.引入CSS
npm i style-loader css-loader -D

            //可以在 css-loader 之后， 通过 ? 追加参数
            //其中，有个固定参数，叫做modules,表示为 普通的css样式表，启用模块化
            {
                test: /\.css$/, use: [
                    { loader: 'style-loader' },
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                                localIdentName: '[path][name]-[local]-[hash:5]'
                            }
                        }
                    } //打包处理CSS样式表的第三方loader
                ]
            },

2.引入Ant Design
npm i antd -S

3.引入字体文件url-loader处理
npm i url-loader -D
npm i file-loader -D (url-loader依赖file-loader)

{ test: /\.ttf|woff|woff2|eot|svt$/, use:'url-loader' } //打包处理字体文件的Loader

4.引入sass-loader (sass-loader依赖node-sass)
npm i sass-loader node-sass -D

5.引入按需导入antd
npm i babel-plugin-import -D
在.babelrc的plugin中加入
["import",{"libraryName":"antd","style":"css"}]
完整配置是
{
    "presets": ["env","stage-0","react"],
    "plugins" : ["transform-runtime",["import",{"libraryName":"antd","style":"css"}]]
}
```

v1-20201224