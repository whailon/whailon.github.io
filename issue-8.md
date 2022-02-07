# uniapp自定义全局弹框组件
2022-02-07
-----

## 需求由来
项目中多次出现弹窗提示，且uni.showModal接口样式不符合设计要求

## 实现目标
+ 自定义confirm ui组件
+ 实现接口显示或关闭弹窗

## 具体实现
弹窗组件包括：title(标题)、content(内容)、confirmText(确认按钮文字)、cancelText(取消按钮文字)、showCancel(是否显示取消按钮)、
isShow(弹窗是否显示标识)
这里为了方便使用组件，不使用prop传值，以组件闭包data定义上面属性, uniapp没有全局document对象，但是可以通过vue的$refs接口访问
到组件实例，通过接口参数传递组件实例，然后绑定确认按钮点击事件，取消按钮的点击事件

confirm.js
```bash
function showConfirm(options) {
  if (this.$refs.confirm) {
    Object.assign(this.$refs.confirm, options);
    this.$refs.confirm.isShow = true;
  }

  return new Promise((resolve) => {
    uni.$once("confirmCancel", (e) => {
      uni.$off('confirmOK');
    })
    uni.$once("confirmOK", (e) => {
      uni.$off('confirmCancel');
      resolve(e || true);
    })
  });
}

export  {
    showConfirm
}
```

confirm.vue
```bash
<template>
  <view class="lxu-confirm" ref="lxuConfirm" @tap.stop="clickModal" v-if="isShow">
    <view class="lxu-confirm-container">
      <view class="lxu-confirm-header" v-if="title">
        <text class="header-text">{{title}}</text>
      </view>
      <view class="lxu-confirm-content" v-if="content">
        <text class="content-text" :style="{textAlign: align}">{{content}}</text>
      </view>
      <view class="lxu-confirm-footer">
          <view v-if="showCancel" class="footer-button footer-left" @click="clickLeft" >
            <text>{{cancelText}}</text>
          </view>
          <view class="footer-button" @click="clickRight">
            <text>{{confirmText}}</text>
          </view>
      </view>
    </view>
  </view>
</template>
<script>
	export default {
        data() {
        return {
            isShow: false,
            title: '提示',
            content: " ",
            align: 'center',
            cancelText: '取消',
            confirmText: '确定',
            showCancel: true
        }
        },
		methods: {
			clickModal(){
				return;
			},
			clickLeft() {
				this.closeModal();
				uni.$emit('confirmCancel')
			},
			clickRight() {
				this.closeModal();
				uni.$emit('confirmOK');
			},
			closeModal() {
				this.isShow = false;
			}
		}
	}
</script>
<style scoped>
...
</style>
```

## 如何使用
```bash
import { confirm } from 目录/confirm.js
```
在vue实例前使用

```bash
Vue.prototype.showConfirm = confirm;
```

在页面中注册confirm组件
```bash
<confirm ref="confirm" />
```

因为接口中定义了refs 为confirm,所以注册组件时ref一定要和接口一致