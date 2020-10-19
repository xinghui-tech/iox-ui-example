<template>
  <view>
    <view class="content">
      <iox-image custom-class="logo" src="/static/iox-ui.jpg" @click="preview" />
      <view class="text-area">
        <text class="title">{{title}}</text>
      </view>
    </view>
  </view>
</template>

<script lang="ts">
import Vue from "vue";
import Component, { mixins } from 'vue-class-component';
import Font from '@zhuyin/iox-ui/lib/mixins/font';

@Component
export default class Index extends mixins(Font){
  title = 'IOX UI 使用样例'

  onLoad() {
  }

  preview() {
    uni.previewImage({
      urls: ['https://res.oss.zhuyin.club/assets/images/iox-ui-qrcode.jpg']
    })
  }

  onShareAppMessage() {
  }
}
</script>

<style lang="less">
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}

.iox-ui {
  height: 300rpx;
  width: 300rpx;
}
</style>
