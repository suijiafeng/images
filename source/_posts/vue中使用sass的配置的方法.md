title: vue中使用sass的配置的方法
author: suijiafeng
tags: []
categories: []
date: 2018-03-02 00:56:00
---

1、创建一个基于 webpack 模板的新项目

	$ vue init webpack myvue

2、在当前目录下，安装依赖

	$ cd myvue
	$ npm install

3、安装sass的依赖包

	npm install --save-dev sass-loader
	//sass-loader依赖于node-sass
	npm install --save-dev node-sass

4、在build文件夹下的webpack.base.conf.js的rules里面添加配置

	{
	  test: /\.sass$/,
	  loaders: ['style', 'css', 'sass']
	}

5、在APP.vue中修改style标签

	<style lang="scss">