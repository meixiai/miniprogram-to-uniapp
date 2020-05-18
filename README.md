# 微信小程序转换为uni-app项目   
   
输入小程序项目路径，输出uni-app项目。
 
        
## 安装(请在CMD或终端里直接输入即可安装，无须下载代码！！！)   
   
```js
$ npm install miniprogram-to-uniapp -g
```
   
## 升级版本   
   
```js
$ npm update miniprogram-to-uniapp -g
```
   
## 使用方法

```sh
Usage: wtu [options]

Options:

  -V, --version     output the version number [版本信息]
  -i, --input       the input path for weixin miniprogram project [输入目录]
  -h, --help        output usage information [帮助信息]
  -c, --cli         the type of output project is vue-cli, which default value is false [是否转换为vue-cli项目，默认false]
  -w, --wxs         transform wxs file to js file, which default value is false [是否将wxs文件转换为js文件，默认false]
  -z, --vant        transform vant-weapp project to uni-app, automatic check [是否支持转换vant项目，默认为false]
  -r, --rename      rename wx.xxx() to uni.xxx(), which default value is false [是否转换wx.xxx()为uni.xxx()，默认false]
  -m, --merge       merge wxss file to vue file, which default value is false [是否合并wxss到vue文件，默认false]

```

Examples:

```sh
$ wtu -i miniprogramProject
```

vue-cli mode [转换项目为vue-cli项目(因vue-cli项目门槛较高，且该功能长时间未维护，不推荐使用)]:
```sh
$ wtu -i miniprogramProject -c
```

Transform wxs file to js file [转换项目并将wxs文件转换为js文件(因uni-app已支持wxs，此功能未维护)]:
```sh
$ wtu -i miniprogramProject -w
```

## 使用指南

本插件详细使用教程，请参照：[miniprogram-to-uniapp使用指南](http://ask.dcloud.net.cn/article/36037)。

使用时遇到问题，请仔细阅读： [miniprogram to uniapp 工具答疑](https://github.com/zhangdaren/articles/blob/master/miniprogram-to-uniapp%E5%B7%A5%E5%85%B7%E7%AD%94%E7%96%91.md)

对于使用有疑问或建议，欢迎加入QQ群：780359397 进行讨论。

<a target="_blank" href="http://shang.qq.com/wpa/qunwpa?idkey=6cccd111e447ed70ee0c17672a452bf71e7e62cfa6b427bbd746df2d32297b64"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="小程序转uni-app讨论群" title="小程序转uni-app讨论群"></a>

## 已完成   
* 支持有/无云开发的小程序项目转换为uni-app项目(cloudfunctions目录将被忽略，uni-app结合小程序云开发见：[使用uni-app进行微信小程序云开发经验分享](https://ask.dcloud.net.cn/article/35933))   
* 支持解析TypeScript小程序项目   
* 支持解析使用npm模块的小程序项目   
* 支持解析include标签   
* 支持解析template标签   
* 支持解析Behavior文件为mixins文件   
* 支持*.js', *.wxml和*.wxss文件进行相应转换，并做了大量的优化   
* 支持识别App、Page、Component、VantComponent、Behavior和纯Javascript文件的转换   
* 
* 修复变量名与函数重名的情况   
* 合并使用require导入的wxs文件   
* 搜索未在data声明，而直接在setData()里使用的变量，并修复   
* 使用[jyf-parser](https://ext.dcloud.net.cn/plugin?id=805)替换wxParse(感谢网友 “爱瑞巴勒康忙北鼻” 的建议)   
* 因uni-app会将所有非static目录的资源文件删除，因此将所有资源文件移入static目录，并修复所有能修复到的路径(目前uni编译时会将非static目录的文件复制一份到static目录，但并不完全，因此本功能仍保留)   
* 
* 支持wxs文件转换，可以通过参数配置(-w)，默认为false(目前uni-app已支持wxs，不再推荐转换wxs)   
* 支持vue-cli模式，可以通过参数配置(-c)，默认为false，即生成为vue-cli项目，转换完成需运行npm -i安装包，然后再导入hbuilder x里开发(建议爱折腾人士使用)  
* 支持vant转换，可以通过参数配置(-z)，默认为false：（现已尽可能自动识别，而无须添加参数；另外，转换后的项目，目前仅支持v3和h5两个平台）  
* 支持wx.xxx()转换为uni.xxx()，可以通过参数配置(-r)，默认为false（虽然uni已经对wx相关函数做了兼容，但仍有很多朋友有此需求，特作为可配置项，按需自取）  
   
  
## 不支持转换的功能及组件
* 不支持转换反编译后的小程序项目   
* 不支持转换使用uni-app编译的小程序项目   
* 不支持转换使用redux开发的小程序(代表为：网易云信小程序DEMO)   
* 不支持转换使用wxpage开发的小程序(https://github.com/tvfe/wxpage)   
* 不支持转换使用腾讯omi开发的小程序(https://github.com/Tencent/omi)   
* 不支持转换小程序抽象节点componentGenerics   
* 不支持component里的pageLifetimes生命周期，请手动绕过   
* 不支持使用js系统关键字作为函数或变量名(如default、import、return、switch等)   
* 不支持以$开头的变量名称，如```Page({data:{$data:{name:"hello"}}})```，刚好$data是vue内置变量，so不支持，需手动修复  
* 更多，请参照[miniprogram to uniapp 工具答疑](https://github.com/zhangdaren/articles/blob/master/miniprogram-to-uniapp%E5%B7%A5%E5%85%B7%E7%AD%94%E7%96%91.md)   
  

## 更新记录   
### v1.0.64(20200518)   
* [新增] template套娃的处理   
* [新增] 命令行[-m]参数，用于将wxss并入vue文件，默认为false(即不并入vue文件)    
* [更新] this.properties.xxx转换为this.xxx   
* [更新] jyf-parser的版本为v2.12.0(2020-05-13)   
* [更新] 补上subPackages分包页面遗漏的style样式   
* [更新] setData代码，解决变量未在data定义而进行setData时报错的问题(感谢网友☆_☆的研究)   
* [优化] getApp()转换方式   
* [优化] 调整vant组件加载方式   
* [修复] app.vue里代码转换有问题的bug   
* [修复] wxss里含DINCond-Medium.ttf字体的处理   
* [修复] 项目仅含app.js和app.wxss，而无app.wxml的情况   
* [修复] 小程序插件加载逻辑，解决小程序第三方插件找不到的问题   
* [修复] 支持转换```t.requirejs("jquery"),Page({...}})```或```getApp,Page({...})```这类代码   

## [历史更新记录](ReleaseNote.md)   

## 感谢   
* 感谢转转大佬的文章：[[AST实战]从零开始写一个wepy转VUE的工具](https://juejin.im/post/5c877cd35188257e3b14a1bc#heading-14)， 本项目基于此文章里面的代码开发，在此表示感谢~   
* 感谢网友[没有好名字了]给予帮助。   
* 感谢DCloud官方大佬[安静]给予帮助。   
* 感谢网友[☆_☆]给予帮助。   
* 感谢网友☆_☆提供增强版setData。     
* 感谢官方大佬DCloud_heavensoft的文章：[微信小程序转换uni-app详细指南](http://ask.dcloud.net.cn/article/35786)，补充了我一些未考虑到的规则。   
* 工具使用[jyf-parser](https://ext.dcloud.net.cn/plugin?id=805)替换wxParse，表示感谢~   
* 感谢为本项目提供建议以及帮助的热心网友们~~   
    
      
## 参考资料   
0. [[AST实战]从零开始写一个wepy转VUE的工具](https://juejin.im/post/5c877cd35188257e3b14a1bc#heading-14)   此文获益良多   
1. [https://astexplorer.net/](https://astexplorer.net/)   AST可视化工具   
2. [Babylon-AST初探-代码生成(Create)](https://summerrouxin.github.io/2018/05/22/ast-create/Javascript-Babylon-AST-create/)   系列文章(作者还是个程序媛噢~)   
3. [Babel 插件手册](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md#toc-inserting-into-a-container)  中文版Babel插件手册   
5. [Babel官网](https://babeljs.io/docs/en/babel-types)   有问题直接阅读官方文档哈   
6. [微信小程序转换uni-app详细指南](http://ask.dcloud.net.cn/article/35786)  补充了我一些未考虑到的规则。   
7. 更新babel版本，命令：npx babel-upgrade --write
8. 发布npm版本：npm publish --acces=public
   
   
## 最后
如果觉得帮助到你的话，可以支持一下作者，请作者喝杯咖啡哈~
这样会更有动力更新哈~~
非常感谢~~

![微信支付](https://zhangdaren.github.io/articles/img/WeChanQR.png)![支付宝支付](https://zhangdaren.github.io/articles/img/AliPayQR.png)


## LICENSE
This repo is released under the [MIT](http://opensource.org/licenses/MIT).
