title: vue3.0快速创建项目
author: suijiafeng
tags: []
categories: []
date: 2018-08-13 22:45:36
---

####  前置条件  ####
更新npm到最新版本 
命令行运行: 

    npm install -g npm 

npm就自动为我们更新到最新版本

使用 npm 全局安装 vue-cli ：
 
    npm i -g @vue/cli

#### 创建项目 ####
执行：
 

    vue create my-project   // my-project是要创建的文件夹

此处有两个选择：
 
`default (babel, eslint) `    // 默认套餐，提供babel和eslint支持

`Manually select features  `  // 自己去选择需要的功能，提供更多的特性选择。

比如如果想要支持 TypeScript ，就应该选择这一项。

可以使用上下方向键来切换选项。

如果只需要 babel 和 eslint 支持，那么选择第一项，就完事了，静静等待 vue 初始化项目。

vue-cli 内置支持了8个功能特性，可以多选：使用方向键在特性选项之间切换，使用空格键选中当前特性，使用 a 键切换选择所有，使用 i 键翻转选项。

对于每一项的功能，此处做个简单描述：

	TypeScript                //支持使用 TypeScript 书写源码
	Progressive Web App (PWA) //Support PWA 支持。
	Router                    //支持 vue-router 。
	Vuex 支持 vuex 。
	CSS Pre-processors        //支持 CSS 预处理器。
	Linter / Formatter        //支持代码风格检查和格式化。
	Unit Testing              //支持单元测试。
	E2E Testing               //支持 E2E 测试。

我选择了 Router，Vuex，CSS Pre-processors，Linter / Formatter

按住enter进入下一步，接下来都是对之前每项选项的更详细的选择。 
css选择SCSS/SASS

Linter / Formatter选择prettier

这一步就是要选择配置文件的位置了。

对于` Babel 、 PostCSS` 等，都可以有自己的配置文件：` .babelrc 、 .postcssrc` 等等，同时也可以把配置信息放在 package.json 里面。此处出于对编辑器（ Visual Studio Code ）的友好支持（编辑器一般默认会在项目根目录下寻找配置文件），选择把配置文件放在外面，选择 `In dedicated config files`
待补充
Save this as a preset for future projects?

这个就是问要不要把当前的这一系列选项配置保存起来，方便下一次创建项目时复用。选择y。

选完之后， vue-cli 就根据前面选择的内容，开始初始化项目了。

#### 启动项目 ####

初始完之后，进入到项目根目录： `cd my-project` 启动项目： `npm run serve` 稍等一会儿，可以看到自动在浏览器中打开了

安装PostCSS插件
通过Vue-cli构建的项目，在项目的根目录下有一个.postcssrc.js，默认情况下已经有了：

		module.exports = {
		        plugins: {
		          autoprefixer: {}
		        }
		}

5
配置成

		module.exports = {
		        plugins: {
		          "postcss-import":{},
		          "postcss-url":{},
		          "autoprefixer": {}
		        }
		}

安装postcss-import和postcss-url插件 

`$ npm install postcss-import`和$ `npm install postcss-url
postcss-import`相关配置点击这里。主要功有是解决@import引入路径问题。使用这个插件，可以让你很轻易的使用本地文件、node_modules或者web_modules的文件。这个插件配合postcss-url让你引入文件变得更轻松。

`postcss-url`相关配置可以点击这里。该插件主要用来处理文件，比如图片文件、字体文件等引用路径的处理。在Vue项目中，vue-loader已具有类似的功能，只需要配置中将vue-loader配置进去。
`autoprefixe`r插件是用来自动处理浏览器前缀的一个插件。如果你配置了`postcss-cssnext`，其中就已具备了autoprefixer的功能。

在配置的时候，未显示的配置相关参数的话，表示使用的是Browserslist指定的列表参数，你也可以像这样来指定last 2 versions 或者 > 5%。如此一来，你在编码时不再需要考虑任何浏览器前缀的问题，可以专心撸码。这也是PostCSS最常用的一个插件之一。

#### 配置插件 ####

我们要完成vw的布局兼容方案，或者说让我们能更专心的撸码，还需要配置下面的几个PostCSS插件：
		
		postcss-aspect-ratio-mini
		postcss-px-to-viewport
		postcss-write-svg
		postcss-cssnext
		cssnano
		postcss-viewport-units
要使用 
安装成功后，在项目根目录下的package.json文件中，可以看到新安装的依赖包：

	"dependencies": {
	    "cssnano": "^3.10.0",
	    "postcss-aspect-ratio-mini": "^0.0.2",
	    "postcss-cssnext": "^3.1.0",
	    "postcss-import": "^11.1.0",
	    "postcss-px-to-viewport": "^0.0.3",
	    "postcss-url": "^7.3.2",
	    "postcss-viewport-units": "^0.1.4",
	    "postcss-write-svg": "^3.0.1",
	    "vue": "^2.5.16",
	    "vue-router": "^3.0.1",
	    "vuex": "^3.0.1"
	  },

接下来在.postcssrc.js文件对新安装的PostCSS插件进行配置：

	module.exports = {
	  plugins: {
	    "postcss-import": {},
	    "postcss-url": {},
	    //"autoprefixer": {},
	    "postcss-aspect-ratio-mini": {},
	    "postcss-write-svg": {
	      utf8: false
	    },
	    "postcss-cssnext": {},
	    "postcss-px-to-viewport": {
	      viewportWidth: 750, //视窗的宽度，对应的是我们设计稿的宽度，一般是750
	      viewportHeight: 1334, //视窗的高度，根据750设备的宽度来置顶，一般指定1334，也可以不配置
	      unitPrecision: 3, //指定'px'转换为视窗单位值的小数位数（很多时候无法整除）
	      viewportUnit: 'vw', //指定需要转换成的视窗单位，建议使用vw
	      selectorBlackList: ['.ignore', '.hairlines', '.g-vw-no'], //指定不转行为视窗单位的类，可以自定义，可以无限添加，建议定义一至两个通用的类名
	      minPixeValue: 1, //小于或等于'1px'不转换为视窗单位，你也可以设置为你想要的值
	      mediaQuery: false //允许在媒体查询中转换'px'
	    },
	    "postcss-viewport-units": {},
	    "cssnano": {
	      preset: "advanced",
	      autoprefixer: false,
	      "postcss-zindex": false
	    }
	  }
	}

特别声明：由于cssnext和cssnano都具有autoprefixer,事实上只需要一个，所以把默认的autoprefixer删除掉，然后把cssnano中的autoprefixer设置为false。对于其他的插件使用，稍后会简单的介绍。

由于配置文件修改了，所以重新跑一下npm run dev。

项目就可以正常看到了。接下来简单的介绍一下后面安装的几个插件的作用。

#### 打包上线 ####

在开发完项目之后，就应该打包上线了。 vue-cli 也提供了打包的命令，在项目根目录下执行： 

    npm run build 

执行完之后，可以看到在项目根目录下多出了一个 dist 目录，该目录下就是打包好的所有静态资源，直接部署到静态资源服务器就好了。

下面作个总结

 Vue3.0 与 Vue2.0 区别：

####  一、创建项目命令的变化。 ####

	vue create my-project //vue3.0创建方式
	vue init webpack my-project   //Vue2.0 创建方式 

同时3.0 版本包括默认预设配置 和 用户自定义配置

- TypeScript
- Progressive Web App (PWA) Support
- Router
- Vuex
- CSS Pre-processors
- Linter / Formatter
- Unit Testing
- E2E Testing

####  二、 项目目录结构变化：  ####

我们对比发现 vue-cli 3.0 默认项目目录相比 2.0 来说精简了很多。
 
- 移除了配置文件目录， config 和 build 文件夹。
- 移除了 static 文件夹，新增 public 文件夹，并且 index.html 移动到 public 中。
- 在 src 文件夹中新增了 views 文件夹，用于分类 视图组件 和 公共组件。

#### 三.移除了配置文件目录后如何自定义配置。 ####

从 3.0 版本开始，在项目的根目录放置一个 vue.config.js 文件, 可以配置该项目的很多方面。

vue.config.js 应该导出一个对象，例如：

		
		module.exports = {
		 baseUrl: '/',
		 outputDir: 'dist',
		 lintOnSave: true,
		 compiler: false,
		 // 调整内部的 webpack 配置。
		 // 查阅 https://github.com/vuejs/vue-doc-zh-cn/vue-cli/webpack.md
		 chainWebpack: () => {},
		 configureWebpack: () => {},
		 // 配置 webpack-dev-server 行为。
		 devServer: {
		  open: process.platform === 'darwin',
		  host: '0.0.0.0',
		  port: 8080,
		  https: false,
		  hotOnly: false,
		  // 查阅 https://github.com/vuejs/vue-doc-zh-cn/vue-cli/cli-service.md#配置代理
		  proxy: null, // string | Object
		  before: app => {}
		 }
		 ....
		}



调整 webpack 配置最简单的方式就是在 vue.config.js 中的 configureWebpack 选项提供一个对象，该对象将会被 webpack-merge 合并入最终的 webpack 配置。

示例代码：配置 webpack 新增一个插件。
	
	// vue.config.js
	module.exports = {
	 configureWebpack: {
	  plugins: [
	   new MyAwesomeWebpackPlugin()
	  ]
	 }
	}
修改插件选项的参数你需要熟悉 webpack-chain 的 API 并阅读一些源码以便了解如何权衡这个选项的全部配置项，但是它给了你比直接修改 webpack 配置中的值更灵活且安全的方式。

	// vue.config.js
	module.exports = {
	  chainWebpack: config => {
	    config
	      .plugin('html')
	      .tap(args => {
	        return [/* new args to pass to html-webpack-plugin's constructor */]
	      })
	  }
	}

#### 四. ESLint、Babel、browserslist 相关配置： ####


- Babel 可以通过 .babelrc 或 package.json 中的 babel 字段进行配置。
 
- ESLint 可以通过 .eslintrc 或 package.json 文件中的 eslintConfig 字段进行配置。

- 你可能注意到了 package.json 中的 browserslist 字段指定了该项目的目标浏览器支持范围。

#### 五. 关于 public 目录的调整。 ####

vue 约定 public/index.html 作为入口模板会通过 html-webpack-plugin 插件处理。在构建过程中，资源链接将会自动注入其中。除此之外，vue-cli 也自动注入资源提示( preload/prefetch ), 在启用 PWA 插件时注入 manifest/icon 链接, 并且引入(inlines) webpack runtime / chunk manifest 清单已获得最佳性能。

在 JavaScript 或者 SCSS 中通过 相对路径 引用的资源会经过 webpack 处理。放置在 public 文件的资源可以通过绝对路径引用，这些资源将会被复制，而不经过 webpack 处理。

小提示：图片最好使用相对路径经过 webpack 处理，这样可以避免很多因为修改网站根目录导致的图片404问题。

