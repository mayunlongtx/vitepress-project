# 小程序开发问题

## 富文本

### 使用微信 [rich-text](https://developers.weixin.qq.com/miniprogram/dev/component/rich-text.html)

::: details 效果

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221024144446.png)
:::

::: details 代码示例

```javascript
// javascript
Page({
  data: {
    nodes: `<p>我是普通的标签</p>\n<p>&nbsp;</p>\n<p>
    <p><a href=\"https://www.baidu.com/\" target=\"_blank\" rel=\"noopener\">我是url</a></p>
    <p><a href=\"https://xxxxx.pdf\" target=\"_blank\" rel=\"noopener\">我是文件</a></p>
    <img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2F8%2F549cf5201acb9.jpg&refer=http%3A%2F%2Fpic1.win4000.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1669006938&t=36c83de484db3fb99305e418d602b6f8" /></p>``,
  },
});
```

```html
// wxml <rich-text nodes="{{nodes}}"></rich-text>
```

:::
::: warning DOM 操作

假如需要获生成的`DOM`可以参考官方的文档

 相关文档： [wx.createSelectorQuery](https://developers.weixin.qq.com/miniprogram/dev/api/wxml/wx.createSelectorQuery.html) 、[获取界面上的节点信息](https://developers.weixin.qq.com/miniprogram/dev/framework/view/selector.html)

我感觉不是很方便，所以去搜了一下插件，找到了 [mp-html](https://jin-yufeng.gitee.io/mp-html/#/overview/feature)

:::

### 使用 `mp-html`

::: details 效果

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221024144513.png)

:::

::: details 代码示例

```javascript
// javascript
Page({
  data: {
    nodes: `<p>我是普通的标签</p>\n<p>&nbsp;</p>\n<p>
    <p><a href=\"https://www.baidu.com/\" target=\"_blank\" rel=\"noopener\">我是url</a></p>
    <p><a href=\"https://xxxxx.pdf\" target=\"_blank\" rel=\"noopener\">我是文件</a></p>
    <img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2F8%2F549cf5201acb9.jpg&refer=http%3A%2F%2Fpic1.win4000.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1669006938&t=36c83de484db3fb99305e418d602b6f8" /></p>``,
  },
});
```

```html
// wxml <mp-html content="{{nodes}}" />
```

```javascript
// index.json
{
  "usingComponents": {
  	"mp-html": "/components/mp-html/index",
	}
}
```

:::
::: tip 参考文档

相关文档：[文档地址](https://jin-yufeng.gitee.io/mp-html/#/overview/feature)、[源码地址](https://github.com/jin-yufeng/mp-html)

:::

## 分享

::: tip 页面分享

[小程序页面分享](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/practice/appshare.html)

:::

### 自定义分享

::: details 效果

![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221024150536.png)
:::

::: details 代码示例

- js

```javascript
// index.ts
Page({
  //
  onShareAppMessage: function (res) {
    // 可以通过判断 res.from 判断触发分享的方式。
    // 注意 path 必须以 / 开头。分享图片尺寸推荐宽高比为5:4，如500*400。
    return {
      title: "一个好东西",
      path: "/pages/index/index",
      imageUrl:
        "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2F8%2F549cf5201acb9.jpg&refer=http%3A%2F%2Fpic1.win4000.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1669006938&t=36c83de484db3fb99305e418d602b6f8",
    };
  },
});
```

- wxml

```javascript
// index.wxml
<button open-type="share" class="btn-share" hover-class="none">
  分享
</button>
```

:::

::: tip 参考文档
通过给 `button` 组件设置属性 `open-type="share"`，可以在用户点击按钮后触发 `Page.onShareAppMessage `事件分享

相关文档：[小程序页面分享](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/practice/appshare.html)
:::

## 右上角提示

::: details 效果
![](https://raw.githubusercontent.com/mayunlongtx/my-drawing-bed/main/marldown-img/20221024152422.png)
:::
::: details 代码示例

- json

```javascript
// index.json
{
  "usingComponents": {
  		"add-tips": "/components/add-tips/index"
	}
}
```

- wxml
```javascript
// index.wxml
<add-tips />
```
:::

::: warning 注意事项
如果使用了自定义导航，那么久需要将 `<add-tips />` 放到自定义导航的 `DOM` 中
:::

::: tip 参考文档

[源码地址](https://github.com/mayunlongtx/add-tips)
:::
