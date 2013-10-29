# 准备要点 #
----------


## 1 兼容IE浏览器 ##

因为IE浏览器与各大浏览器区别太大，为了尽可能的保证在所有浏览器中有一致的体验，很多时候需要单独对待IE浏览器。为了保证代码精简及一致，ZUI只支持IE8+。为了保证IE能够使用最新渲染模式而不是兼容模式，在html文档头部应加入以下代码：

    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        ...

针对IE7及更早的版本，应该给出提示，让用户升级浏览器。在`body`之后加入以下代码可以有选择性的出现浏览器升级提示，并给出链接引导用户访问[abetterbrowser.org](http://abetterbrowser.org/)：

    <body>
        <!--[if lt IE 8]>
            <p class="abetterbrowser">您正在使用 <strong>过时的</strong> 浏览器. 是时候 <a href="http://abetterbrowser.org/">更换一个更好的浏览器</a> 来提升用户体验.</p>
        <![endif]-->
        ...

因为IE8及早期版本不支持HTML5标签，所以针对IE8浏览器，我们引入html5shiv来使得HTML5标签在IE8中也能使用。在HTML文档的script区域加入以下代码（示例中html5shiv库来自maxcdn）：

    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
    <![endif]-->

因为IE8及早期版本同样不支持media query来实现响应式布局，我们同样可以通过条件注释引入respond.js来帮助ie实现该功能。（示例中的respond.js来自maxcdn，可以和html5shiv共享同一个条件注释区域。）

    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
    <![endif]-->


## 2 css normalize ##

为了能在不同的浏览器具有一直的体验，采用开源项目 [normalize.css](http://necolas.github.io/normalize.css/) 进行样式重置。


## 3 响应式布局 ##

现代web应用应该支持响应式布局。栅格系统已提供良好的基础构建响应式布局页面，同时也提供一些辅助工具类来控制内容在不同设备的展现方式。

在ZUI中提供针对4中不同尺寸的设备屏幕进行分别控制。

    屏幕                    名称       尺寸
    超小屏幕（手机）         xs        <768px
	小屏幕（平板）           sm        >=768px
    中等屏幕（笔记本电脑）    md        >=992px
    大屏幕（桌面电脑）        lg        >=1200px

针对4种屏幕类型各定义两种辅助类来在不同的设备上显示或隐藏内容。

                  超小屏幕   小屏幕   中等屏幕   大屏幕
    .visible-xs   可见       隐藏     隐藏      隐藏
    .visible-sm   隐藏       可见     隐藏      隐藏
    .visible-md   隐藏       隐藏     可见      隐藏
    .visible-lg   隐藏       隐藏     隐藏      可见
    .hidden-xs    隐藏       可见     可见      可见
    .hidden-sm    可见       隐藏     可见      可见
    .hidden-md    可见       可见     隐藏      可见
    .hidden-lg    可见       可见     可见      隐藏

其中显示辅助类`.visible-xs`、`.visible-sm`、`.visible-md`、`.visible-lg`可以组合使用，同理对于隐藏辅助类也可以组合使用以达到不同的效果。但不要将显示辅助类和隐藏辅助类混合使用。

ZUI也提供用来控制打印机的显示与隐藏的辅助类。显示和隐藏不能同时使用。

- `.visible-print`：在打印时显示，在浏览器正常浏览时隐藏。
- `.hidden-print`：在浏览器正常浏览时显示，在打印时隐藏。


## 4 栅格系统 ##

- 采用bootstrap3的网格设计。具体使用参考[bootstrap3-grid](http://v3.bootcss.com/css/#grid)
- 通过.container包含行（row），行再包含列（column）。
- 系统默认12列
- 分为col-xs-*/col-sm-*/col-md-*/col-lg-*四种设计分别对应超小屏幕(<768)/小屏幕(>=768)/中等屏幕(>=992)/大屏幕(>=1200)
- 通过col-xs-offset-*来向右偏移，通过col-xs-pull-*/col-xs-push-*来左右移动


## 5 排版 ##

### 5.1 字体 ###

在ZUI中我们定义了三种字体家族已适应不同的场合。这些字体在中英文环境下都能够很好的显示。

    无衬线字体    "Helvetica Neue", Helvetica, Tahoma, Arial, sans-serif
    衬线字体      Georgia, "Times New Roman", Times, serif
    等宽字体      Monaco, Menlo, Consolas, "Courier New", monospace

使用[无衬线字体](http://zh.wikipedia.org/wiki/%E7%84%A1%E8%A5%AF%E7%B7%9A%E5%AD%97%E9%AB%94)来作为页面的默认字体，因为无衬线字体非常适合在屏幕上显示；衬线字体作为一个额外的选择，但并不推荐在小字号中使用，但可以用于特殊文字或者标题中；等宽字体用来显示程序代码。

默认的字体大小为14px，以保证在所有屏幕上都能有最佳效果。ZUI中也允许使用更小号的字体，不过不要小于12px。默认行高为字体大小的1.428倍，一般为20px。一至六级标题的行高为字体大小的1.2。

### 5.2 文字排版 ###

文字是组成页面的重要内容，一个好的排版是构建好的用户界面的基石。应根据我们的设计原则来进行文字排版。下表中列举了web设计时会用到的文字排版方式。

    页面标题    <h1>    36px 粗体  在一个页面只有一个页面标题。
    二级标题    <h2>    30px 粗体  为页面第二级标题，可能在一个页面中使用到多个二级标题。
    三级标题    <h3>    24px 粗体  页面第三级标题，嵌套在二级标题下使用。
    四级标题    <h4>    18px 粗体  页面第四级标题，嵌套在三级标题下使用。
    五级标题    <h5>    14px 粗体  颜色灰色  页面第五级标题，嵌套在四级标题下使用。
    六级标题    <h6>    12px 粗体  颜色灰色  页面第六级标题，嵌套在五级标题下使用。
    段落        <p>     14px    正文中大部分由段落组成。段落的行高为20px。段落间在垂直方向上有10px边距。
    突出的段落  <p class="lead">    18px    突出的段落具有更大的字体，在一个段落上加.lead类。
    粗体文本    <strong>14px    通常粗体文本用来强调内容。
    斜体文本    <em>    14px 斜体    
    小的文本    <small> 12px 颜色灰色 small文本字体只有正常字体大小的85%，通常为12px。
    超链接      <a>     14px    超链接具有不同的颜色以区别其他文本，超链接仅当鼠标悬停时会增加下划线。
    块级引用    <blockquote> 14px    用于显示一大段引用的内容。
    内嵌的引用  <q>     14px    用于在正文行内显示引用的术语。
    代码       <pre><code> 14px 等宽字体   代码区域会加上方框，并使用等宽字体显示，详细代码显示规定请参见节