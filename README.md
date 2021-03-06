# manage-system #
基于Vue.js 2.x系列 + Element UI 的后台管理系统解决方案。[线上地址](http://work.omwteam.com/)

[English document](https://github.com/lin-xin/manage-system/blob/master/README_EN.md)

## 前言 ##
随着移动互联网技术的的蓬勃发展，以及手媒体的时代到来，人们更习惯于在手机或平板上使用APP来进行学习与交流，市场上的教育类APP成千上万，但大多数应用商店对于教育类APP缺乏专业性的细致分类，用户想要找到合适的APP无疑于大海捞针。教师使用APP应用于移动学习教学的经验和案例也没有得到充分的分享。

笔者设计并开发一款基于WordPress的Padagogy网站,Padagogy Wheel是澳大利亚学习设计师Alan基于 布鲁姆教育目标分类学提出的电子书包教学法模型，有助于教师设计电子书包环境下的参与式学习，网站的主要作用是分享App使用相关教学案例以及根据Padagogy模型将App分类，使得App的功能在移动学习的领域得到充分的挖掘和利用,本文将介绍该网站从设计到开发的具体流程.


## 功能 ##
- [x] 基于Wordpress网站开发，网站具有CMS系统的基本功能，可以编辑，管理，发布新闻，文章等
- [x] 系统能够提供用邮箱注册用户账号，登录功能
- [x] Padagogy的App信息以Wiki的形式存在于系统之中，每条App信息至少要关联对应的官网链接，和下载地址，每条信息可以关联对应的教学案例或相关的文章
- [x] 所有用户默认具有wiki的编辑，添加,发布,权限，每个用户都可以添加App信息，在发布时，确定wiki的分类信息标签，发布之前的App信息教学案例和相关的应用经验
- [x] 未注册用户能够浏览网站文章，能够根据Padagogy的分类标签，筛选/检索App信息




## 目录结构介绍 ##

	|-- build                            // webpack配置文件
	|-- config                           // 项目打包路径
	|-- src                              // 源码目录
	|   |-- components                   // 组件
	|       |-- common                   // 公共组件
	|           |-- Header.vue           // 公共头部
	|           |-- Home.vue           	 // 公共路由入口
	|           |-- Sidebar.vue          // 公共左边栏
	|		|-- page                   	 // 主要路由页面
	|           |-- BaseCharts.vue       // 基础图表
	|           |-- BaseForm.vue         // 基础表单
	|           |-- BaseTable.vue        // 基础表格
	|           |-- Login.vue          	 // 登录
	|           |-- Markdown.vue         // markdown组件
	|           |-- MixCharts.vue        // 混合图表
	|           |-- Readme.vue           // 自述组件
	|           |-- Upload.vue           // 图片上传
	|           |-- VueEditor.vue        // 富文本编辑器
	|           |-- VueTable.vue         // vue表格组件
	|   |-- App.vue                      // 页面入口文件
	|   |-- main.js                      // 程序入口文件，加载各种公共组件
	|-- .babelrc                         // ES6语法编译配置
	|-- .editorconfig                    // 代码编写规格
	|-- .gitignore                       // 忽略的文件
	|-- index.html                       // 入口html文件
	|-- package.json                     // 项目及工具的依赖配置文件
	|-- README.md                        // 说明


## 安装启动步骤 ##

	git clone git@github.com:yunqiangwu/padagogy_web.git	// 把源码下载到本地
	cd padagogy_web											// 进入项目目录
	start http://padagogy.cn/								// 运行线上项目

## 使用说明与演示 ##

### 登录网站后台 ###
访问Wordpress后台。访问地址：[Wordpress后台管理](http://padagogy.cn/wp-admin/)
用户名：wuyun
密码：wu950429

### 添加App ###
访问Padagogy管理界面后台。访问地址：[管理Padagogy](http://padagogy.cn/wp-admin/edit.php?post_type=padagogy)

### 编辑多重筛选菜单 ###
基于wordpress后台菜单管理开发。访问地址：[Wordpress后台](http://padagogy.cn/wp-admin/nav-menus.php?action=edit&menu=20)

## 其他注意事项 ##
### 一、如果我不想用到上面的某些组件呢，那我怎么在模板中删除掉不影响到其他功能呢？ ###

举个栗子，我不想用 vue-datasource 这个组件，那我需要分四步走。

第一步：删除该组件的路由，在目录 src/router/index.js 中，找到引入改组件的路由，删除下面这段代码。

```JavaScript
{
    path: '/vuetable',
    component: resolve => require(['../components/page/VueTable.vue'], resolve)     // vue-datasource组件
},
```

第二步：删除引入该组件的文件。在目录 src/components/page/ 删除 VueTable.vue 文件。

第三步：删除该页面的入口。在目录 src/components/common/Sidebar.vue 中，找到该入口，删除下面这段代码。
	
```HTML
<el-menu-item index="vuetable">Vue表格组件</el-menu-item>
```

第四步：卸载该组件。执行以下命令：
	
	npm un vue-datasource -S

完成。

### 二、如何切换主题色呢？ ###

第一步：打开 src/main.js 文件，找到引入 element 样式的地方，换成浅绿色主题。

```javascript
import 'element-ui/lib/theme-default/index.css';    // 默认主题
// import '../static/css/theme-green/index.css';       // 浅绿色主题
```

第二步：打开 src/App.vue 文件，找到 style 标签引入样式的地方，切换成浅绿色主题。

```javascript
@import "../static/css/main.css";
@import "../static/css/color-dark.css";     /*深色主题*/
/*@import "../static/css/theme-green/color-green.css";   !*浅绿色主题*!*/
```

第三步：打开 src/components/common/Sidebar.vue 文件，找到 el-menu 标签，把 theme="dark" 去掉即可。

## 项目截图 ##
### 默认皮肤 ###

![Image text](https://github.com/lin-xin/manage-system/raw/master/screenshots/wms1.png)

### 浅绿色皮肤 ###

![Image text](https://github.com/lin-xin/manage-system/raw/master/screenshots/wms2.png)
