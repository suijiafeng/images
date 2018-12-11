title: webpack4的学习与填坑
author: suijiafeng
tags: []
categories: []
date: 2018-07-12 00:56:00
---




在慕课上学习了webpack的课程，做了一些笔记，算分享也算记录吧。教程里的是webpack1和现在的webpack4有很多区别，自己也走了不少的坑，最好使用的时候去看官方文档。
 

https://webpack.js.org/
在填坑的时候也借鉴了很多人写的文章。所以有很多部分是融合了超级多前人的经验总结，然后自己结合实际进行操作的做笔记。部分地方可能有重复，看得懂就好了。

1.全局安装webpack

	npm install -g webpack

2.创建项目文件，初始化项目文件目录

	npm init
 
到项目文件下安装webpack   

	npm install webpack

3.安装全局的webpack-cli

     npm install -g webpack-cli  //获取当前webpack版本号配置文件
4.配置mode 

默认有production和development两种模式可以设置

命令行设置

   webpack --mode development

5.新建入口
在项目文件目录下新建src文件夹，新建index.js文件入口

6.文件打包命令行输入 

	webpack --mode development 或 webpack --mode production

webpack将会默认打包，将./src/index.js文件打包成./dist/main.js文件（自动生成dist文件夹和main.js文件）

7.建立html文件，在项目目录下建立html文件，可以直接引用dist/main.js文件。

注意，我们的 script 引用的文件是 dist/main.js，而不是 index.js。

这正是前端开发领域的一个趋势：开发的源文件（例子中的 index.js）与最终部署的文件（例子中的 dist/main.js）是区分开的，之所以这样，是因为开发环境与用户的使用环境并不一致。比如我们可以在开发环境使用 ES2017 甚至 ES2018 的特性，而用户的浏览器不见得支持 - 这也是 webpack 等打包工具的一个意义，它们能够辅助我们构建出在目标用户浏览器上正常运行的代码。

8.其他参数配置
我们如果需要配置webpack指令的其他参数，只需要在webpack –mode production/development后加上其他参数即可，如：

	webpack --mode development --watch --progress --display-modules --colors --display-reasons
 

9.监控文件,实时刷新
watch选项最为直观，但在默认情况下，watch选项是关闭状态。
启用watch选项

    webpack --mode development --watch

10.刷新浏览器（看官方文档容易填坑，奈何英语emmmm）
https://github.com/webpack/webpack-dev-server

https://webpack.js.org/configuration/dev-server/#devserver
webpack-dev-server,一个基于expressjs的开发服务器，提供实时刷新浏览器页面的功能。

安装webpack-dev-server
首先在项目下安装 webpack-dev-server: 

	npm install -g webpack-dev-server

然后在命令行下执行
	webpack-dev-server --mode development --output-public-path dist

webpack-dev-server是一个轻量级的服务器，修改文件源码后，自动刷新页面将修改同步到页面上安装webpack-dev-server：


> ①全局安装：npm install webpack-dev-server -g 

> ②在项目中安装并将依赖写在package.json文件中:npm install webpack-dev-server --save-dev

> ③使用命令webpack-dev-server --mode development --output-public-path src完成自动刷新，指定publicPath，这部分很容易没有实时刷新。

> ④默认的端口号是8080，如果需要8080端口被占用，就需要改端口，webpack-dev-server --port 3000(将端口号改为3000)，可以直接在webpack.config.js配置文件中配置devServer属性，开启热更新和port。

> ⑤启动服务，输入localhost:端口号，就显示发布的所有根目录，如果项目根目录中没有index.html文件，就会在浏览器中列出项目根目录中的所有的文件夹。

> ⑥当使用webpack-dev-server --mode development --output-public-path src命令时，在每次修改文件，是将文件打包保存在内存中并没有写在磁盘里，这种打包得到的文件和项目根目录中的index.html位于同一级。使用webpack命令将打包后的文件保存在磁盘中例如在index.html文件中引入通过webpack-dev-server --mode development  --output-public-path src打包的build.js
`<script src="build.js"></script>　`　在index.html文件中引入通过webpack命令打包的build.js　

> `<script src="./build/build.js"></script>`
--inline 内联模式，在开发服务器的两种不同模式之间切换。默认情况下, 应用程序将被启用内嵌模式。这意味着将在包中插入一个脚本来处理实时重装, 并且生成消息将出现在浏览器控制台中。
--hot 启用热模块更换功能

//////以上是搜索了各个教程里面说的，但是实际操作还是有问题，
index.html入口文件是在根目录下，没有进行配置content-base，因为配置了之后会只打包配置的目录文件，默认是根文件。配置了output的publicPath（很重要，删掉之后就不能自动刷新了，应该是webpack-dev-server将每次打包的文件根据output设置生成在publicPath目录下，而文件本身依旧是手动打包的，无法查看到自动刷新打包的文件），只配置了端口，没有配置hot:true和inline:true(最开始配置了，但是有报错，所以删掉莫名OK了）

> ⑦webpack自带的watch命令与webpack-dev-server的区别
--watch是文件修改后自动打包，webpack-dev-server是修改后发布到服务器上

 

> ⑧webpack-dev-server --mode development --content-base src --inline --hot//显示只针对src路径下的文件刷新,文件修改之后浏览器自动刷新，如果要打开的文件和打包的文件不在一个文件夹内，最好不要设定文件夹
 
11.打包css文件

在项目目录下安装处理css文件的loader命令行输入：

	npm install css-loader style-loader --save-dev
	css-loader //处理css文件

style-loader //将css-loader处理后的文件作为样式标签`<style>`插入到html文件中

在处理css文件的时候要指定loader，如在index.js文件里输入

	require('style-loader!css-loader!./style.css')

或者直接在命令行输入

	webpack --mode development --module-bind 

"css=style-loader!css-loader"
12--progress(查看进度)
13--display-modules(显示隐藏的模块)
14 --display-reasons(显示打包原因)
 
15.配置，webpack需要传入配置对象，因此进行新建配置文件webpack.config.js，或者使用node.js内置的path模块进行配置，并在它前面加上 __dirname这个全局变量。可以防止不同操作系统之间的文件路径问题，并且可以使相对路径按照预期工作。

①先写moudule.exports={};进行配置；

②入口文件配置，entry="入口文件路径，如./src/js/main.js";

③输出文件配置，output={path:__dirname+"输出文件路径，如/dist/js/bundle.js"};//要创建dist文件夹
__dirname为运行时的当前路径；
另一种方式，先定义const path = require("path");//引入nodejs的path模块

然后在输出文件路径path:path.resolve(__dirname,"./dist/js/bundle.js");

//path.resolve()方法解析了当前路径，将相对路径改为绝对路径。
④重新指定配置文件名

webpack --config 文件名

如webpack --config webpack.dev.config.js

16.定义执行脚本，可以在package.json中设置

在script中设置，如设置"webpack":"webpack --mode development --config webpack.config.js --progress --display-modules --colors --display-reason",//--colors(彩色显示)
直接执行上面的脚本npm run webpack

17.entry配置（chunk），

①字符串表示，单输入，所有依赖都要在入口文件中指定，如entry:"./src/js/main.js",

②数组表示，多输入，两个需要打包到一起的文件可以在配置文件的entry中用数组表示，如entry:["./app/entry1", "./app/entry2"],//这两个文件将会打包到一起

③对象表示（哈希），多页面入口，entry:{page1:"./page1",page2:["./src/a.js","./src/b.js"]},

这三种方式都会把文件打包到输出文件中。

18.output配置，

①单个入口起点，就设置一个出口，如output:
{filename:'bundle.js',path:'/dist/js'}

②多个入口起点，可以设置name或者hash，如output:{filename:'[name].js',path:__dirname+'/dist/js'}
或output:{filename:'[name]-[hash].js',path:__dirname+'/dist/js'}
或output:{filename:'[name]-[chunkhash].js',path:__dirname+'/dist/js'}

hash值可以认为是版本号或者MD5值保证每个文件的唯一性，每一次修改之后生成文件的hash值不一样，文件名不一样
。
③publicPath可以理解为占位符。当需要上线的时候可以将服务器地址设置到这个参数中，output:

	{path:'xxx',filename:'xxx',publicPath:'http://cdn.com/'}
 
插件（plugin）
插件是 webpack 的支柱功能。webpack 自身也是构建在 webpack 配置中用到的相同的插件系统之上。插件目的在于解决 loader 无法实现的其他事。

19.插件html-webpack-plugin
要引用之前先安装,在项目文件目录下安装 npm install html-webpack-plugin --save-dev
安装好之后，在webpack.config.js配置文件中对插件的引用
var htmlWebpackPlugin = require('html-webpack-plugin');//commonJS写法
在module.exports中添加plugin部分进行插件初始化，
插件列表，当多个bundle需要共享一些相同的插件时，CommonChunkPlugin可以将这些依赖项提取到一个共享包中，以免重复。
plugins:[
    new webpack.optimize.CommonsChunkPlugin({
        .....
    }),
    new htmlChunkPlugin({
        template:'index.html',//自定义模板
        filename:'index-[hash].html',//生成文件名
        inject:'head',//指定链接注入在<head>标签中还是<body>标签中，为false值时表示不自动注入文件中，需要手动设置
        title:'webpack demo',//传递参数，可以在index.html模板中引用
        minify:{//压缩html文件，具体参数设置可以查看官方文档
            
        }
    })
]
index.html引用配置文件中的参数，JS语法模式，要使用JS语句可以使用<%%>将每行代码包裹起来。赋值可以使用<%=xxx %>，如<%=htmlWebpackPlugin.options.title%>就可以取到配置文件中定义的title的值。
在配置文件中可以任意的配置参数向html文件进行传参。
自定义引用的js文件可以直接写到html文件中
如在html文件中相对应的位置写，

`	<script src="<%=htmlWebpackPlugin.files.chunks.main.entry %>"></script>
	<script src="<%=htmlWebpackPlugin.chunks.a.entry%>"></script>`

chunk是文件入口
以上是单文件引用的示例，多文件引用则需要调用多次的html-webpack-plugin插件，设置方式相同
多页面使用同一个页面模板，可以定义htmlWebpackPlugin插件中的chunks参数，进行设置不同的页面引用不同的chunks，如设置chunks:['main','a']
excludeChunks:['a'],//指出排除的chunk
直接将公共初始化脚本嵌入到html页面中，inline方式，在html模板中加上脚本源码引用代码，
如

`	<script type="text/javascript">
	<%=compilation.assets[htmlWebpackPlugin.files.chunks.main.entry.substr(htmlWebpackPlugin.files.publicPath.length)].source()%>
	</script>`
	//.substr()的作用是将删除publicPath部分的绝对路径获取文件的相对路径。

按照文件顺序引用js文件可以手动设置for循环出htmlWebpackPlugin.files.chunks的entry值插入文件中。
 
20.loader
loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。
 
本质上，webpack loader 将所有类型的文件，转换为应用程序的依赖图（和最终的 bundle）可以直接引用的模块。
loader能够import导入任何类型的模块。
在webpack的配置中loader有两个目标：

①.test属性，用于表示出应该被对应的loader进行转换的某个或某些文件。

②.use属性，表示进行转换时，应该使用那个loader。

使用方式：
①配置，在webpack.config.js中指定
②内联，在每个import语句中显示指定loader
③CLI，在shell命令中指定
 
在webpack.config.js中配置loader

在module.exports中添加属性module
如安装babel插件（js编译器），使用此插件转换ES6代码，如何安装根据官网进行安装：
    module:{
        rules:[
        { test:/\.js$/,
            exclude:/node_modules/,
            loader:"babel-loader"
            }
        ]
    }
    
设置preset，指定preset（预配置）设置如何处理js文件

①在rules中设置query:{presets:['latest']}

②在根目录下创建一个.babelrc文件,其中内容为：
{
    "presets":["env"]
}
③在package.json中，增加babel属性：
"babel":{
"presets":["latset"]
}
 
21.优化
可以在配置文件中，设置打包范围，如exclude设置不处理哪些模块，include处理哪些文件下的内容。
具体可以看官方文档进行配置。


 