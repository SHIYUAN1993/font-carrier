# font-carrier

font-carrier是一个功能强大的字体操作库，使用它你可以随心所欲的操作字体。

一个字体font,包含若干字形glyph。比如我们浏览器里渲染`我`,浏览器就会去当前设置的font里面找到 `我`对应的字形glyph，使用它的形状来渲染。不同的字体的`我`的字形形状不一，所以才有差别。

font-carrier封装了简单的api,让你可以将某个svg,设置成一个字对应的字形。也可以通过解析已有字体，拿到某个字在这个字体下面对应的svg。让你通过svg的维度随意修改字体展现样式。

我们不生产字体，我们只是字形的搬运工


# features

* 支持创建一个空白字体
* 支持解析已有字体(ttf,svg)
* 支持使用svg来设置字的展现
* 支持解析svg的转换还有各种非path图形
* 支持针对某一个字，导出对应的svg
* 支持导出四种浏览器主流字体（ttf,eot,woff,svg）
* 支持设置各种字体相关内容


# getting start

如果对iconfont还不是很了解的，请先参考这篇[文章](http://purplebamboo.github.io/2014/01/09/iconfont/)

## install


```
npm install font-carrier --save
```


## use

### 1.你可以创建一个空白字体，或者解析一个已有的字体，这样都可以得到一个字体对象

``` js
var fontCarrier = require('font-carrier')

//创建空白字体对象
var font = fontCarrier.create()

//从其他字体解析
var transFont = fontCarrier.transfer('./test/test.ttf')
```

### 2.拿到字体对象后，你就可以使用svg随意操作字体了

``` js
//可以设置某个字对应的形状,当然unicode也是支持的
font.setSvg('我',fs.readFileSync('./test/svgs/circle.svg').toString())

//也可以使用setGlyph可以设置更多信息
font.setGlyph('我',{
  glyphName:'我',
  horizAdvX:'1024',//设置这个字形的画布大小为1024
  svg:fs.readFileSync('./test/svgs/circle.svg').toString()
})

//可以针对字直接拿到对应的svg
var svg = font.getSvg('我')

//也可以先拿到对应的字形对象，再导出对应的svg
var glyph = transFont.getGlyph('我')
glyph.toSvg()

```

### 3.使用get,set各种操作完后，你可以选择导出字体

``` js
//默认会导出svg,ttf,eot,woff四种字体，
//可以不传path,这样会默认返回一个包含四个字体buffer的对象
font.output({
  path:'./iconfont'
})

```

### 4.导出字体后就可以在web中使用了

``` html
<style type="text/css">
  @font-face {font-family: 'iconfont';
      src: url('iconfont.eot'); /* IE9*/
      src: url('iconfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
      url('iconfont.woff') format('woff'), /* chrome、firefox */
      url('iconfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
      url('iconfont.svg#uxiconfont') format('svg'); /* iOS 4.1- */
  }

  .iconfont{font-family:"iconfont";font-size:16px;font-style:normal;}
</style>

<i class="iconfont">我</i>
//此时渲染出来的图形就是你设置的svg的样子

```

## example

更多实例，请参考[这里](./doc/example.md)

## api

详细请看[这里](./doc/api.md)


## test

运行`npm test`之后访问 ./test/index.html


# licence

MIT

