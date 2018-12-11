title: vue2.0 引入 jQurey 的方式
author: suijiafeng
tags: []
categories: []
date: 2018-05-28 01:03:00
---
最近学习vue，习惯性的通过`<script>`标签引入jquery，写完后报错才想起来，这种方式在vue是不适用的。

1：因为已经安装了vue脚手架，所以需要在webpack中全局引入jquery

打开`package.json`文件，在里面的dependencies加入这行代码，jquery后面的是版本，根据你自己需求更改。

     dependencies:{

    "jquery":"^2.2.3"

     }
然后在命令行中`npm install jquery –save-dev`

大多人应该都是使用的淘宝镜像，所以使用cnpm，如果你不是 ，可以使用npm安装。

2：找到build文件夹下的`webpack.base.conf.js`文件中加入一行代码

		var webpack=require("webpack")

3：然後在webpack.base.conf.js中module.exports的最后加入这行代码，

      plugins: [
    new webpack.optimize.CommonsChunkPlugin('common.js'),
    new webpack.ProvidePlugin({
    jQuery: "jquery",
    $: "jquery"
    })
    ]
4：在main.js中引入,加入下面这行代码

    import $ from 'jquery'
5：最后一步，重新跑一边就好，`npm run dev`

6.验证方法 在APP.vue里进行验证

      //app.vue
      <template>
      <div id="app">
        <img src="./assets/logo.png">


        <a class="alert" href="javascript:;">點我 </a>
      </div>
    </template>
    <script>
    export default {
      name:"app",
    }
    $(document).ready(function(){
      $("a").click(function(){
        $(this).hide();
        alert("這就對了")
      });
    });

    </script>
    <style>

    </style>
能夠弹出 alert 内容，就说明jQuery 能正常使用。