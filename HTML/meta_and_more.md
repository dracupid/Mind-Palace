HTML —— Meta and more
================
> “HTML head 头部分的标签、元素有很多，涉及到浏览器对网页的渲染，SEO 等等，而各个浏览器内核以及各个国内浏览器厂商都有些自己的标签元素,这就造成了很多差异性。移动互联网时代，head 头部结构，移动端的 meta 元素，显得更为重要。” ——FEX

## 1. Document Type Declaration
此标签位于文档最前面，html 标签之前，不区分大小写。告知浏览器使用哪种 HTML 或者 XHTML 规范渲染文档。

#### 语法
```html
<!DOCTYPE root-element PUBLIC "FPI" ["URI"] [
<!-- internal subset declarations -->
]>
```
- [FPI(Formal Public Identifier)](http://en.wikipedia.org/wiki/Formal_Public_Identifier)： 注册//组织//类型 标签//语言
    - 注册：组织是否由国际标准化组织(ISO)注册，+表示是，-表示不是。
    - 组织：即组织名称，如：W3C。
    - 类型：一般是 DTD。
    - 标签：指定公开文本描述，即对所引用的公开文本的唯一描述性名称，后面可附带版本号。
    - 语言：DTD 语言的 ISO 639 语言标识符，如：EN 表示英文，ZH 表示中文。

#### HTML5 (向后兼容，推荐使用)。
```html
<!doctype html>
```

#### HTML 4.01 strict
All HTML elements and attributes, but does NOT INCLUDE presentational or deprecated elements (like font). Framesets are not allowed.
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

#### HTML 4.01 Transitional
All HTML elements and attributes, INCLUDING presentational and deprecated elements (like font). Framesets are not allowed.
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

#### HTML 4.01 Frameset
Equal to HTML 4.01 Transitional, but allows the use of frameset content.
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

对应的也有XHTML版本，这里不赘述

#### 作用

- 对文档进行有效性验证

告诉用户代理和校验器这个文档是按照什么 DTD 写的。这个动作是被动的，每次页面加载时，浏览器并不会下载 DTD 并检查合法性，只有当手动校验页面时才启用。

- 决定浏览器的呈现模式

对于实际操作，通知浏览器读取文档时用哪种解析算法。

> [doctype wiki](http://en.wikipedia.org/wiki/Document_type_declaration)

## 2. 渲染模式
- 标准模式(standards mode)：按照 HTML 与 CSS 的定义渲染
- 怪异模式(quirks mode)：尝试模拟更旧的浏览器的行为
- 近乎标准模式(almost standards mode)：一些浏览器（如，基于 Gecko 的，或者 IE 8 在 strict mode 下）也使用一种尝试于这两者之间妥协，实施了一种表单元格尺寸的怪异行为，除此之外符合标准定义。

如果存在一个完整的 DOCTYPE 则浏览器将会采用标准模式，而如果它缺失或不完整则会采用怪异模式。

> - [模式？标准！](http://padding.me/blog/2014/07/04/mode-or-standard/)
> - [关于浏览器模式和文本模式的困惑](https://www.imququ.com/post/browser-mode-and-document-mode-in-ie.html)

## 3. meta 标签
#### 编码与语言
声明文档使用的字符编码，建议使用utf-8<br/>
下面两个是[等效](http://code.google.com/p/doctype-mirror/wiki/MetaCharsetAttribute)的，建议使用较短的，易于记忆。
```html
<meta charset="utf-8">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
```

设置页面语言
```html
<html lang="zh-cmn-Hans"> 简体中文
<html lang="zh-cmn-Hant"> 繁体中文
<html lang="en"> 英文
```

> [页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"](http://zhi.hu/XyIa)。

#### 内核控制
优先使用 IE 最新版本和 Chrome
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```
360浏览器：使用极速（webkit）内核。
```html
<meta name="renderer" content="webkit">
```
360浏览器：如果安装了Google chrome frame，则使用GCF来渲染页面，否则使用最高版本的IE内核进行渲染。
```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
```
>[360浏览器内核控制Meta标签说明文档](http://se.360.cn/v6/help/meta.html)

百度手机版：不对网站进行转码
```html
<meta http-equiv="Cache-Control" content="no-siteapp" />
```
> [SiteApp转码声明](http://m.baidu.com/pub/help.php?pn=22&ssid=0&from=844b&bd_page_type=1)

#### SEO
页面标题
```html
<title>your title</title>
```
页面关键词
```html
<meta name="keywords" content="your keywords">
```
页面描述内容，150字符以内
```html
<meta name="description" content="your description">
```
定义网页作者
```html
<meta name="author" content="author,email_address">
```
定义网页搜索引擎索引方式，robot terms 是一组使用英文逗号「,」分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。
```html
<meta name="robots" content="index,follow">
```
> robot terms取值: https://msdn.microsoft.com/zh-cn/library/ff724037(v=expression.40).aspx

#### viewport
通常：
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**content 参数**
- width: viewport 宽度(数值/device-width)
- height: viewport 高度(数值/device-height)
- initial-scale: 初始缩放比例
- maximum-scale: 最大缩放比例
- minimum-scale: 最小缩放比例
- user-scalable: 是否允许用户缩放(yes/no)

如果你的网站不是响应式的，请不要使用 initial-scale 或者禁用缩放。
```html
<meta name="viewport" content="width=device-width, user-scalable=yes">
```

> - [Configuring the Viewport](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)
> - [非响应式设计的viewport](http://www.qianduan.net/non-responsive-design-viewport.html)

#### ios
**设备**<br/>
添加到主屏后的标题（>= iOS 6）
```html
<meta name="apple-mobile-web-app-title" content="标题">
```
是否启用 WebApp 全屏模式
```html
<meta name="apple-mobile-web-app-capable" content="yes" />
```
设置状态栏的背景颜色(只有在 "apple-mobile-web-app-capable" content="yes" 时生效)
- default 默认值。
- black 状态栏背景是黑色。
- black-translucent 状态栏背景是黑色半透明。
如果设置为 default 或 black, 网页内容从状态栏底部开始。 如果设置为 black-translucent ,网页内容充满整个屏幕，顶部会被状态栏遮挡。

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```
禁止识自动别电话或电子邮件
```html
<meta name="format-detection" content="telphone=no, email=no" /> <!-- 禁止数字识自动别为电话号码 -->
```

**图标**<br/>
<link rel="" sizes="" href="图片路径" />
- rel="apple-touch-icon": 图片自动处理成圆角和高光等效果。
- rel="apple-touch-icon-precomposed": 禁止系统自动添加效果，直接显示设计原图。
- size: 图片尺寸，不写则是`57x57`。
```html
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png" /> <!-- iPhone 和 iTouch 默认-->
```
- iPad: 72x72 像素
- Retina iPhone 和 Retina iTouch: 114x114
- Retina iPad: 144x144
- iPhone 6 plus上: 180×180
- iPhone 6: 120x120

**启动画面**<br/>
> - 官方文档：https://developer.apple.com/library/ios/qa/qa1686/_index.html
> - 参考文章：http://wxd.ctrip.com/blog/2013/09/ios7-hig-24/

iPad 的启动画面是不包括状态栏区域的；iPhone 和 iPod touch 的启动画面是包含状态栏区域的。

添加智能 App 广告条 Smart App Banner（iOS 6+ Safari）
```html
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"> <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
```

> [Configuring Web Applications](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html#//apple_ref/doc/uid/TP40002051-CH3-SW3)

#### WIN 8
Windows 8 磁贴颜色
```html
<meta name="msapplication-TileColor" content="#000"/>
```
Windows 8 磁贴图标
```html
<meta name="msapplication-TileImage" content="icon.png"/>
```


#### favicon
```html
<link rel="shortcut icon" type="image/ico" href="/favicon.ico" />
```
> [favicon cheat sheet](https://github.com/audreyr/favicon-cheat-sheet)

#### 其他
Chrome 39 控制选项卡颜色
```html
<meta name="theme-color" content="#db5945">
```
> http://updates.html5rocks.com/2014/11/Support-for-theme-color-in-Chrome-39-for-Android

禁止 Chrome 浏览器中自动提示翻译
```html
<meta name="google" value="notranslate">
```
> http://www.w3.org/International/questions/qa-translate-flag

RSS 订阅
```html
<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" />
```

## 4. 移动端的头部标签和meta示例
```html
<!DOCTYPE html> <!-- 使用 HTML5 doctype，不区分大小写 -->
<html lang="zh-cmn-Hans"> <!-- 更加标准的 lang 属性写法 http://zhi.hu/XyIa -->
<head>
    <!-- 声明文档使用的字符编码 -->
    <meta charset='utf-8'>
    <!-- 优先使用 IE 最新版本和 Chrome -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <!-- 页面描述 -->
    <meta name="description" content="不超过150个字符"/>
    <!-- 页面关键词 -->
    <meta name="keywords" content=""/>
    <!-- 网页作者 -->
    <meta name="author" content="name, email@gmail.com"/>
    <!-- 搜索引擎抓取 -->
    <meta name="robots" content="index,follow"/>
    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">
    <!-- No Baidu Siteapp-->
    <meta http-equiv="Cache-Control" content="no-siteapp"/>

    <!-- Add to homescreen for Chrome on Android -->
    <meta name="mobile-web-app-capable" content="yes">
    <!-- iOS 设备 begin -->
    <meta name="apple-mobile-web-app-title" content="标题">
    <!-- 添加到主屏后的标题（iOS 6 新增） -->
    <meta name="apple-mobile-web-app-capable" content="yes"/>
    <!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 -->

    <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
    <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black"/>
    <!-- 设置苹果工具栏颜色 -->
    <meta name="format-detection" content="telphone=no, email=no"/>
    <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">

    <!-- iOS 图标 begin -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>
    <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>
    <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
    <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>
    <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
    <!-- iOS 图标 end -->

    <!-- iOS 启动画面 begin -->
    <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>
    <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>
    <!-- iPad 竖屏 1536x2008（Retina） -->
    <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>
    <!-- iPad 横屏 1024x748（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>
    <!-- iPad 横屏 2048x1496（Retina） -->

    <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>
    <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
    <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>
    <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
    <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
    <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
    <!-- iOS 启动画面 end -->

    <!-- iOS 设备 end -->
    <meta name="msapplication-TileColor" content="#000"/>
    <!-- Windows 8 磁贴颜色 -->
    <meta name="msapplication-TileImage" content="icon.png"/>
    <!-- Windows 8 磁贴图标 -->

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>
    <!-- 添加 RSS 订阅 -->
    <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>
    <!-- 添加 favicon icon -->

    <title>标题</title>
</head>
```

# 参考资料
0. **[Extend and customise HTML5 Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/extend.md)**
0. **[Search and Social Meta Tags 2013](http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013)**
0. [一丝的blog](https://github.com/yisibl/blog/issues/1)
0. [HTML head 头标签](http://fex.baidu.com/blog/2014/10/html-head-tags/) by FEX
0. [移动前端不得不了解的html5 head 头标签](http://www.css88.com/archives/5480)
0. [Meta Extensions](https://wiki.whatwg.org/wiki/MetaExtensions)
0. [http://code.lancepollard.com/complete-list-of-html-meta-tags/](http://code.lancepollard.com/complete-list-of-html-meta-tags/)
0. [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes)
