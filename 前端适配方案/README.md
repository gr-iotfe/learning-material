## 这个目录下存放了需要全局使用的公共 css 文件和 js 文件

# 内容

- 已有的 scss 宏用于解决 **1px 边框问题** 和 **不同设备中字体显示大小不同问题**
- 目前使用手淘团队的 lib-flexible 库和 rem 单位来使 **不同设备上的普通元素的显示一致**，虽然是比较古老的解决方法，但好在稳定和使用简单

# 使用

- ## scss 宏的使用：

通过`import 'static/ui/style/index.scss'`引入

使用方法:

**1像素边框**

目前定义了以下几个宏，**参数不定且有默认值**，不传参会使用默认值
```css
// 元素的整体边框,考虑到有圆角的需求，可以传两个参数：颜色(def: #000)和圆角大小(def: 0px)
  @include border-1px(red, 50%)
  也可以这样：
  @include border-1px(#ccc)

// 元素的上边框，传一个参数：颜色(def: #000)
  @include border-top-1px(#ccc)

// 元素的下边框，传一个参数：颜色(def: #000)
  @include border-bottom-1px(#ccc)

// 元素的左边框，传一个参数：颜色(def: #000)
  @include border-left-1px(#ccc)

// 元素的右边框，传一个参数：颜色(def: #000)
  @include border-right-1px(#ccc)

// 取消某个元素的边框（如列表渲染后需特殊处理的那个元素）,无参可传
  @include border-none()
```

使用此1px边框需要给应用到的那个DOM元素加 `.border-1px`class名称，以表示其使用了1像素边框，
> ps: 此类名实际是用于选择伪元素并对其进行压缩之用，少了此类名边框会变粗或不显示

使用例：
```html
<li class='item-li border-1px'>message</li>
```
在css中:
```css
.item-li { @include border-top-1px(red) }
```
对某个元素取消此样式：
```css
.item-li { @include border-none() }
```

**字体大小适配**

使用时：用`@include font-size()` 代替`font-size`属性 ，`font-size()`中字体大小为 屏幕宽度为414px（iPhone 7 Plus） 时的文字大小
 > ps: 以屏幕宽度414px为基准，在290~560px 的范围内进行等比缩放，超出范围的仍使用边界值；且考虑到一些浏览器可能不支持小数单位，计算时加入了取整操作，大小变化较突兀；如需要设置字符字体的大小，可能还需要取为偶数。

例如：
```css
.item { @include font-size(36px) }
```
会被解析为：
```css
// screen.width === 322px
.item { font-size: 28px }
// screen.width === 414px
.item { font-size: 36px }
// screen.width === 500px
.item { font-size: 42px }
```


- ## 使用lib-flexible 库实现整体布局适配：
  使用rem单位作为所有长度的度量单位，屏幕宽度为10rem，屏幕上的任何一段长度的表示使用 *其与屏幕宽度的比值 乘以 10rem *来得到**，如屏幕宽度为320px时，设计稿上 `width: 32px` 应被写为 `width: 1rem`

> PS: lib-flexible 的基本原理是将屏幕宽度统一分成 10 份，使用一份的宽度来对 html 的 font-size 重新赋值，这样所有的设备上 1rem 的长度都是屏幕宽度的 0.1 倍，所有的长度单位都使用 rem 之后其真实长度都会随着屏幕宽度变化而变化；一些关于 dpr 的设置现在没有用到

在 html 中通过 CDN 引入（因已对源码进行了部分修改，项目中应使用本地文件引入方式）

```html
<script src="http://g.tbcdn.cn/mtb/lib-flexible/{{0.3.4}}/??flexible_css.js,flexible.js"></script>
```

或使用本地文件（使用webpack打包要将引入index.html的js和css放在static中，否则打包后找不到；开发环境使用 debug 文件）

```html
<script type="text/javascript" src="static/lib-flexible/flexible_css.debug.js"></script>
<script type="text/javascript" src="static/lib-flexible/flexible.debug.js"></script>
```

# 预览

- demo 工程里可预览效果：在 demo 目录下：`npm install` -- `npm run dev`，然后访问 localhost:8080

# 一些思考

> 对于具有不同dpr的设备应加载不同的图片，以提升显示性能，如对于相同的一幅100px*100px的图片，在dpr等于1的设备上应使用100 * 100分辨率的图片，而在dpr等于2的设备上应使用200 * 200分辨率的图片。

> 对于字体大小适配的问题，将字体大小统一与屏幕宽度成比例增加的方法不一定是最佳方案，一个体验更好的目标是：在此基础上还能进行调整，使得小屏幕上字体显示的更大（字体大小有下限），在大屏幕上字数能显示的更多（字体大小有上限）

> 使用lib-flexible可手动设置viewport，html的font-size及html的其他一些属性，也可区分android与ios设备，如果以后有需要可以修改。


                                                                              create by csm