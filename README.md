# iox-ui
<p align="center">
    <img alt="logo" src="https://res.oss.zhuyin.club/assets/images/iox-ui.png" width="120" height="120" style="margin-bottom: 10px;">
</p>
<h1 align="center">IOX UI</h1>

IOX UI参考Vant（轻量、可靠的移动端 Vue 组件库）的设计和实现，在微信小程序组件库版本[vant-weapp](https://github.com/youzan/vant-weapp "vant-weapp")基础上实现的[uniapp](https://github.com/dcloudio/uni-app)版本。

针对uniapp的一些特性进行了修改和调整，同时增加一些新的组件，对一些组件功能也有所增强。

>当前参考的vant-weapp版本为：1.5.0。

## 安装
安装UI库：
>yarn add @zhuyin/iox-ui

安装微信typescript类型定义：
>yarn add -D @zhuyin/mp-api-typings

安装less：
>yarn add -D less less-loader

增加Vue对[TypeScript 支持](https://cn.vuejs.org/v2/guide/typescript.html)

## UNIAPP使用
参考uniapp的[easycom](https://uniapp.dcloud.io/collocation/pages?id=easycom)配置。
### 引入
>pages.json

```json
{
  //...
  "easycom": {
		"autoscan": true,
		"custom": {
			"iox-(.*)": "@zhuyin/iox-ui/lib/widget/iox-$1/iox-$1.vue"
		}
  }
  //...
}
```

### 使用
```vue
<template>
    <view>
      <iox-icon name="loading" />
    </view>
</template>

<script>
    // 这里不用import引入，也不需要在components内注册iox-icon组件。template里就可以直接用
    export default {
        data() {
            return {

            }
        }
    }
</script>
```

### 加载字体图标
全局加载
>App.vue

```js
export default Vue.extend({
  mpType: 'app',
  globalData: {
    ioxIconUrl: 'https://res.oss.zhuyin.club/assets/fonts/fontawesome-webfont.woff'
  },
  onLaunch(options: App.LaunchShowOption) {
    console.log("App Launch");
    const fontUrl = (this as any).globalData.ioxIconUrl;
    wx.loadFontFace({
      global: true,
      family: 'FontAwesome',
      source: `url("${fontUrl}")`,
      success: console.log,
      fail: console.warn
    });
    this.checkUpdate();
  }
}
```

每个页面加载：
>index.vue

```js
export default Vue.extend({
    created() {
        const app = getApp().$vm;
        const info = getSystemInfoSync();
        if (info && compareVersion(info.SDKVersion, '2.10.0') < 0) {
            const fontUrl = app.globalData.ioxIconUrl;
            uni.loadFontFace({
                family: 'FontAwesome',
                source: `url("${fontUrl}")`,
                success: console.log,
                fail: console.warn
            });
        }
    }
}
```

## 加载样式
创建一个空文件
>/src/sytle/iox-ui.less

全局加载
>App.vue

```vue
<style lang="less">
@import "~@zhuyin/iox-ui/lib/style/index.less";
</style>
```

## 参考手册
<img alt="logo" src="https://img.yzcdn.cn/vant/logo.png" width="32" height="32" style="margin-bottom: 10px;" align="middle">https://youzan.github.io/vant/

**说明：** 由于小程序原生实现和Vue实现会有一些差异，差异化的使用请参考源代码里面的demo。
