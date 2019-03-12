一. Webpack简介

1. Webpack是什么

      webpack其实就是一个Javascript应用程序的静态模块快打包器

2.Webpack有什么作用

模块化打包：webpack会将项目的资源文件当成一个一个模块，模块之间会有依赖关系，webpack将会对这些有依赖关系的文件进行处理，让浏览器可以识别出来。最后，webpack会将应用程序需要的每个模块打包成一个或者多个bundle.

二. Webpack 环境配置和简单打包

1.安装node

2.创建package.json文件

	npm init

3. 安装webpack

	本地安装：

		npm install —save-dev webpack

		npm install —save-dev webpack-cli

	全局安装：

		npm install —g webpack webpack-cli

4.打包

	默认entry入口： src/index.js

	默认output出口：dist/main.js

	打包模式：

	webpack —mode development

	webpack —mode production


package.json
"scripts":{
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
}
三. 配置webpack.config.js

1. 新建一个webpack.config.js

2. 配置入口entry(所需打包的文件路径)

	(1) 单入口

		a. 单文件： 

			例如： entry: './src/index.js'

	        b. 多文件

			在你想要多个依赖文件一起注入，并且将他们的依赖导向到一个"chunk"时，传入数组的方式就很有用。

			例如：entry: [‘./src/index.js','./src/index2.js',…...’]

	(2) 多入口

		例如：

			entry: {	

				pageOne: './src/pageOne/index.js',

				pageTwo: './src/pageTwo/index.js',

				pageThree: './src/pageThree/index.js'

			}	

3. 配置出口output

	a. 单出口


output:{
    path: path.resolve(__dirname,'dist'),
    filename: 'bundle.js'
}
	b. 多出口(要和对入口搭配使用，pageOne就是这里的[name])


output: {
    path: path.resolve(__dirname,'dist'),
    filename: '[name].js'
}
(1) path指文件打包后的存放路径

(2) path.resolve()方法将路径或路径片段的序列处理成绝对路径

(3) _direname 标识当前文件所在的目录的绝对路径

(4) filename 是打包后的文件的名称

四. 配置Webpack-dev-server

1. 了解 webpack-dev-server

	webpack-dev-server 是用来配置本地服务器的，使用它可以为webpack打包生成资源文件提供web服务。

	webpack-dev-server主要提供的两个功能：

	(1) 为静态文件提供web服务

	(2) 自动刷新和热替换(HMR)

2. 安装webpack-dev-server

	npm install —save-dev -webpack-dev-server

3. 配置webpack.config.js文件

	devServer: {

		contentBase: './build',  //设置服务器访问的基本目录

		host: 'localhost', //服务器的ip地址

		port: 8080, //端口

		open: true, //自动打开页面

	}

四. Webpack4 loader

1.Loader

	含义：

		loader让webpack能够去处理那些非Js文件(webpack自身之理解js), loader可以将所有类型的文件转换为webpack能够处理的有效模块，然后就可以利用webpack的打包功能，对它们进行处理。

		本质上，webpack loader将所有类型的文件，转换为应用程序的依赖图，可以直接引用的模块。


> 注意，loader能够import导入任何类型的模块(例如：css模块), 这是webpack特有的功能，其他打包程序或任务执行器的可能并不支持，我们认为这种语言扩展是有很必要的，因为这可以使开发人员创建出更准确的依赖关系图。
		在webpack的配置中loader有两个目标：

		(1)test 属性，用于标识出应该被对应的loader进行转换的某个或某些文件。

		(2)use 属性，表示进行转换时，应用使用哪个loader.


npm install sytle-loader css-loader
2.配置loader

		(1) 在webpack.config.js 文件配置module中的rules

		在webpack的配置中loader有两个目标：

			a. test 属性，用于标识出应该被对应的loader进行转换的某个或某些文件

			b. use 属性，表示进行转换时，应该使用哪个 loader

3.编译less和sass

		(1) 安装less loader

			安装less-loader和less

		(2) 安装sass loader

			安装sass-loader和node-sass

4.使用PostCss处理浏览器前缀

		(1) 安装loader

			安装postcss-loader和autoprefixer

		(2) 配置loader

			需要和autoprefixer一起搭配使用

5.文件处理

		(1) 文件处理

			安装file-loader

		(2) 选项配置

			name: 为文件配置自定义文件名字

			context: 配置自定义文件的上下文，默认为webpack.config.js

			publicPath: 给你的文件配置自定public发布目录

			outputPath: 为你的文件配置自定义outpu输出目录

		(3) 第三方库文件处理

			

6. babel编译ES6

		(1) babel转化语法所依赖项：

		babel-loader: 负责es6语法转化

		babel-core: babel核心包

		babel-preset-env: 告诉babel使用哪种转码规则进行文件处理

		(2) 配置config文件

		exclude表示不再指定目录查找相关文件


module:{
    rules:[
        {
            test:/\.js$/,
            exclude:/node_modules/,
            use:'babel-loader'
        }
    ]
}
五. Webpack4 插件

1.生成html

	HtmlWebpackPlugin

	npm install html-webpack-plugin —save-dev



2.提取分离css

mini-css-extract-plugin插件

npm install —save-dev mini-css-extract-plugin

配置：


test: /\.css$/,
use: ExtractTextPlugin.extract({
    fallback: "style-loader",
    use: "css-loader"
})
​
plugins: [
        new ExtractTextPlugin("./css/index.csss")
    ]
3.压缩css以及优化css结构

插件：optimize-css-assets-webpack-plugin

4.拷贝静态文件

插件：copy-webpack-plugin

5.清除文件

插件：clean-webpack-plugin

五. Webpack4 其他配置

1.webpack处理html引用图片

插件：html-loader


{
    test: /\.(html)$/,
    use: {
        loader: "html-loader",
        options: {
            attrs: ["img:src","img.data-src"]
        }
    }
}
sourcemap调试

模块热替换


devServer:{
    hot: true,
    hotOnly: true //只热更新，不会自动刷新页面
}
​
new webpack.NameModulesPlugin(),
new webpack.HotModuleReplacementPlugin()
​
​
index.js 
if(module.hot){
    module.hot.accept();
}
区分开发环境和生产环境

插件：webpack-merge

原理: 把webpack.config.js 拆分为

	 webpack.common.conf.js 放公共的配置，如果入口entry，出口output，常用loader以及插件等。

	webpack.dev.config.js 是开发环境上的配置，如果devServer配置，模块热替换等方面开发的配置

	webpack.prod.conf.js 是在生产环境上的配置，比如提取分离css，压缩css，和js等

webpack打包优化技巧

减少文件搜索范围

a. 优化resolve.extensions配置

	在导入语句没带文件后缀时，Webpack会自动带上后缀去尝试问询文件是否存在。

后缀尝试列表要尽量的小，不要把项目中不可能存在的情况写到后缀尝试列表中

频率出现最高的文件后缀要优先放在最前面，以做到尽快的退出寻找过程

在源码中写导入语句时，要尽可能的带上后缀，从而可以避免寻找过程，例如在你确定的情况下把require('./data')协程require('./data.json')


resolve: {
    //尽可能的减少后缀尝试的可能性
    extensions:['js']
}
b. 优化 resolve.modules配置

	resolve.modules 用于配置 Webpack 去哪些目录下寻找第三方模块

	resolve.modules 的默认值是 ['node_modules'],会采用向上递归搜索的方式查找


resolve: {
    // 尽可能的减少后缀尝试的可能性
    extensions:['js'],
    // 使用绝对路径指明第三方模块存放的位置，以减少搜索步骤
    modules: [
        resolve("src"),
        resolve("node_modules")
    ]
}
c. 优化resolve.alias配置

	resolve.alias 配置项通过别名来把原导入路径映射成一个新的导入路径


alias:{
    'react'： resolve('./node_modules/react/dist/react.min.js'),
    'assets'： resolve('./public/assets')
}
d. 缩小文件匹配范围

	Include: 需要处理的文件的位置

	Exclude: 排除掉不需要处理的文件的位置


{
    test: /\.js$/,
    include: [resolve('src')],
    exclude: /node_modules/,
    use: {
        loader: 'babel-loader',
        options: {
            presets:['@babel/preset-env']
        }
    }
}


设置noParse

防止webpack解析那些任何与给定正则表达式相匹配的文件，忽略的文件中不应该含有import,require,define的调用，或者任何其他导入机制，忽略大型的library可以提高构建性能，比如jquery,elementUI等库。 

给babel-loader设置缓存

babel-loader提供了cacheDirectory特定选项（默认：false）:设置时，给定的目录将用于缓存加载器的结果。




{
    use:{
        laoder:'babel-loader?cacheDirectory=true',
        options:{
            presets:['@babel/preset-env']
        }
    }
}
4.happyPack

	基本原理：在webpack构建中，我们需要使用Loader对js，css,图片，字体等文件做转换操作，并且转换的文件数量也是非常大，且这些转换操作不能并发处理文件，而是需要一个一个文件进行处理，HappyPack的基本原理是将这部分任务分解到多个子进程中去并行处理，子进程处理完成之后吧结果发送到主进程中，从而减少总的构建时间。

npm install --save-dev happypack



六. Webpack4 课程总结

课程资源


