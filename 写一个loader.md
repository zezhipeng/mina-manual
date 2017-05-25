## vue-loader
<img src="https://camo.githubusercontent.com/14e5f4477f49cf0fc0d8f228facb17772a0b1025/687474703a2f2f626c6f672e6576616e796f752e6d652f696d616765732f7675652d636f6d706f6e656e742e706e67" alt="" width="600px">

这是一张 `.vue` 文件的截图，相信用过 `.vue` 开发的老铁都能体会到其流畅顺滑的开发方式了吧。

#### 小程序也能这样开发吗？

答案是肯定能的，只要我们利用已有 vue-loader 的解析模块，便能便能很容易的编写出一个 loader 出来，来满足我们

### vue-template-compiler

通过阅读 vue-loader 的源码，我们就可以发现他就是用了[vue-template-compiler](https://github.com/YiSiWang/vue-template-compiler)来解析 `.vue` 文件，并且返回

```javascript
{
  template: ...,
  styles: ...,
  script: ...
}
```
这样的 object。所以如果我们假如自定义一个`.mina`文件（或者直接用`.vue`）格式文件，利用[vue-template-compiler](https://github.com/YiSiWang/vue-template-compiler)解析分离，然后生成相应的三个文件就可以了。

<br>
### 编写 loader

在根目录下新建 `mina-loader` 文件夹。在里面新建 index.js 文件
```
const loaderUtils = require('loader-utils')
const { parseComponent } = require('vue-template-compiler')

module.exports = function (content) {
  this.cacheable()

  const parts = parseComponent(content)

  console.log(parts)
  return ``
}


```