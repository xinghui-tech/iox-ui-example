<template>
  <view>
    <iox-notice-bar wrapable left-icon="/static/logo.png" color="#1989fa" :text="notice" />
    <view class="d-flex flex-column justify-content-center align-items-center">
      <iox-image custom-class="logo" src="/static/iox-ui.jpg" @click="preview" />
      <view class="d-flex justify-content-center">
        <iox-button @click="openDemo">{{title}}</iox-button>
      </view>
    </view>
    <view class="mt-2 ml-2"><iox-icon class="mr-1" name="book"/>使用要点：</view>
    <iox-collapse v-model="active">
        <iox-collapse-item icon="key" title="安装UI库">
          yarn add @zhuyin/iox-ui
        </iox-collapse-item>
        <iox-collapse-item icon="star-o" title="安装微信Typescript类型定义">
          yarn add -D @zhuyin/mp-api-typings
        </iox-collapse-item>
        <iox-collapse-item icon="paint-brush" title="安装less">
          yarn add -D less less-loader
        </iox-collapse-item>
        <iox-collapse-item icon="css3" title="加载样式">
          <iox-image fit="widthFix" width="100%" src="/static/usage/style.png" />
        </iox-collapse-item>
        <iox-collapse-item icon="font-awesome" title="加载字体图标">
          <iox-image fit="widthFix" width="100%" src="/static/usage/font-app.png" />
          <iox-image fit="widthFix" width="100%" src="/static/usage/font-pages.png" />
        </iox-collapse-item>
    </iox-collapse>
  </view>
</template>

<script lang="ts">
import Vue from "vue";
import Component, { mixins } from 'vue-class-component';
import Font from '@zhuyin/iox-ui/lib/mixins/font';

@Component
export default class Index extends mixins(Font){
  notice = '欢迎过使用IOX-UI';
  title = 'IOX UI 使用样例';
  active = 0;

  onLoad() {
  }

  preview() {
    uni.previewImage({
      urls: ['https://res.oss.zhuyin.club/assets/images/iox-ui-qrcode.jpg']
    })
  }

  openDemo() {
    uni.navigateToMiniProgram({
      appId: "wxa3a53e39a5f479e8",
      path: "/pages/index"
    })
  }

  onShareAppMessage() {
    return {
      title: 'IOX UI 使用样例',
      // #ifdef MP-ALIPAY
      desc: 'IOX UI 使用样例'
      // #endif
    };
  }
}
</script>

<style lang="less">
.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.iox-ui {
  height: 300rpx;
  width: 300rpx;
}
</style>
