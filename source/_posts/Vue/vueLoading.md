title: Vue Loading组件
date: 2017-08-18 18:29:00
description:
categories:
- FrontFrame
tags:
- Vue
toc: true
author:
comments:
original:
permalink: 
image: http://img.zcool.cn/community/032bd3557a5abcd0000018c1b74486e.jpg
---
　　**Vue组件探秘**文章适合有一定vue经验，只是简单介绍项目中的搭建与开发的优化之处。知识点，请自行查阅！
<!-- more -->

## 原理

## vue-loading

├── vue-loading/           
	├── loading-rotate.vue       # 旋转
	├── loading.vue            	 # 实体
	└── index.js            		 # 初始化

```javascript
import Vue from 'vue'
import Loading from './loading.vue'
const Indicator = Vue.extend(Loading)
let instance

export default {
  open (options = {}) {
    if (!instance) {
      instance = new Indicator({
        el: document.createElement('div')
      })
    }
    // console.log(instance)
    if (instance.value) return
    instance.text = typeof options === 'string' ? options : options.text || ''
    instance.spinnerType = options.spinnerType || 'snake'
    document.body.appendChild(instance.$el)

    Vue.nextTick(() => {
      instance.value = true
    })
  },

  close () {
    if (instance) {
      instance.value = false
    }
  }
}
```

```vue
<template lang="pug">
	div
	  i.loading.icon_toast
</template>
<style lang="less" scoped>
	.loading {
	  width: 10px;
	  height: 10px;
	  display: inline-block;
	  vertical-align: middle;
	  animation: weuiLoading 1s steps(12, end) infinite;
	  background: transparent
	    url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMjAiIGhlaWdodD0iMTIwIiB2aWV3Qm94PSIwIDAgMTAwIDEwMCI+PHBhdGggZmlsbD0ibm9uZSIgZD0iTTAgMGgxMDB2MTAwSDB6Ii8+PHJlY3Qgd2lkdGg9IjciIGhlaWdodD0iMjAiIHg9IjQ2LjUiIHk9IjQwIiBmaWxsPSIjRTlFOUU5IiByeD0iNSIgcnk9IjUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAgLTMwKSIvPjxyZWN0IHdpZHRoPSI3IiBoZWlnaHQ9IjIwIiB4PSI0Ni41IiB5PSI0MCIgZmlsbD0iIzk4OTY5NyIgcng9IjUiIHJ5PSI1IiB0cmFuc2Zvcm09InJvdGF0ZSgzMCAxMDUuOTggNjUpIi8+PHJlY3Qgd2lkdGg9IjciIGhlaWdodD0iMjAiIHg9IjQ2LjUiIHk9IjQwIiBmaWxsPSIjOUI5OTlBIiByeD0iNSIgcnk9IjUiIHRyYW5zZm9ybT0icm90YXRlKDYwIDc1Ljk4IDY1KSIvPjxyZWN0IHdpZHRoPSI3IiBoZWlnaHQ9IjIwIiB4PSI0Ni41IiB5PSI0MCIgZmlsbD0iI0EzQTFBMiIgcng9IjUiIHJ5PSI1IiB0cmFuc2Zvcm09InJvdGF0ZSg5MCA2NSA2NSkiLz48cmVjdCB3aWR0aD0iNyIgaGVpZ2h0PSIyMCIgeD0iNDYuNSIgeT0iNDAiIGZpbGw9IiNBQkE5QUEiIHJ4PSI1IiByeT0iNSIgdHJhbnNmb3JtPSJyb3RhdGUoMTIwIDU4LjY2IDY1KSIvPjxyZWN0IHdpZHRoPSI3IiBoZWlnaHQ9IjIwIiB4PSI0Ni41IiB5PSI0MCIgZmlsbD0iI0IyQjJCMiIgcng9IjUiIHJ5PSI1IiB0cmFuc2Zvcm09InJvdGF0ZSgxNTAgNTQuMDIgNjUpIi8+PHJlY3Qgd2lkdGg9IjciIGhlaWdodD0iMjAiIHg9IjQ2LjUiIHk9IjQwIiBmaWxsPSIjQkFCOEI5IiByeD0iNSIgcnk9IjUiIHRyYW5zZm9ybT0icm90YXRlKDE4MCA1MCA2NSkiLz48cmVjdCB3aWR0aD0iNyIgaGVpZ2h0PSIyMCIgeD0iNDYuNSIgeT0iNDAiIGZpbGw9IiNDMkMwQzEiIHJ4PSI1IiByeT0iNSIgdHJhbnNmb3JtPSJyb3RhdGUoLTE1MCA0NS45OCA2NSkiLz48cmVjdCB3aWR0aD0iNyIgaGVpZ2h0PSIyMCIgeD0iNDYuNSIgeT0iNDAiIGZpbGw9IiNDQkNCQ0IiIHJ4PSI1IiByeT0iNSIgdHJhbnNmb3JtPSJyb3RhdGUoLTEyMCA0MS4zNCA2NSkiLz48cmVjdCB3aWR0aD0iNyIgaGVpZ2h0PSIyMCIgeD0iNDYuNSIgeT0iNDAiIGZpbGw9IiNEMkQyRDIiIHJ4PSI1IiByeT0iNSIgdHJhbnNmb3JtPSJyb3RhdGUoLTkwIDM1IDY1KSIvPjxyZWN0IHdpZHRoPSI3IiBoZWlnaHQ9IjIwIiB4PSI0Ni41IiB5PSI0MCIgZmlsbD0iI0RBREFEQSIgcng9IjUiIHJ5PSI1IiB0cmFuc2Zvcm09InJvdGF0ZSgtNjAgMjQuMDIgNjUpIi8+PHJlY3Qgd2lkdGg9IjciIGhlaWdodD0iMjAiIHg9IjQ2LjUiIHk9IjQwIiBmaWxsPSIjRTJFMkUyIiByeD0iNSIgcnk9IjUiIHRyYW5zZm9ybT0icm90YXRlKC0zMCAtNS45OCA2NSkiLz48L3N2Zz4=)
	    no-repeat;
	  background-size: 100%;
	  &.loading_transparent {
	    background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120' viewBox='0 0 100 100'%3E%3Cpath fill='none' d='M0 0h100v100H0z'/%3E%3Crect xmlns='http://www.w3.org/2000/svg' width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.56)' rx='5' ry='5' transform='translate(0 -30)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.5)' rx='5' ry='5' transform='rotate(30 105.98 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.43)' rx='5' ry='5' transform='rotate(60 75.98 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.38)' rx='5' ry='5' transform='rotate(90 65 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.32)' rx='5' ry='5' transform='rotate(120 58.66 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.28)' rx='5' ry='5' transform='rotate(150 54.02 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.25)' rx='5' ry='5' transform='rotate(180 50 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.2)' rx='5' ry='5' transform='rotate(-150 45.98 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.17)' rx='5' ry='5' transform='rotate(-120 41.34 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.14)' rx='5' ry='5' transform='rotate(-90 35 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.1)' rx='5' ry='5' transform='rotate(-60 24.02 65)'/%3E%3Crect width='7' height='20' x='46.5' y='40' fill='rgba(255,255,255,.03)' rx='5' ry='5' transform='rotate(-30 -5.98 65)'/%3E%3C/svg%3E");
	  }
	}
	.icon_toast {
	  &.loading {
	    margin: 20px 0 10px;
	    width: 30px;
	    height: 30px;
	    vertical-align: baseline;
	    display: inline-block;
	  }
	}
	@keyframes weuiLoading {
	  0% {
	    transform: rotate3d(0, 0, 1, 0deg);
	  }
	  100% {
	    transform: rotate3d(0, 0, 1, 360deg);
	  }
	}
</style>
```

```vue
<template>
  <transition name="vue-loading">
    <div class="loading_toast" v-show="show">
      <div class="mask"></div>
      <div class="toast" :style="{ position: position }">
        <loading-rotate></loading-rotate>
        <p class="content">{{text || 'loading'}}<slot></slot></p>
      </div>
    </div>
  </transition>
</template>

<script>
import loadingRotate from './loading-rotate'

  export default {
    props: {
      value: {
        type: Boolean,
        default: false
      },
      text: String,
      position: String
    },
    created () {
      this.show = this.value
    },
    data () {
      return {
        show: false
      }
    },
    watch: {
      value (val) {
        this.show = val
      },
      show (val) {
        this.$emit('input', val)
      }
    },
    components: {
      'loading-rotate': loadingRotate
    }
  }
</script>

<style lang="less" scoped>
  @import "../../../assets/less/mixins.less";
  .vue-loading-enter, .vue-loading-leave-active {
    opacity: 0;
  }
  .vue-loading-leave-active, .vue-loading-enter-active {
    transition: opacity 300ms;
  }
  .mask {
    position: fixed;
    z-index: 1000;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    /*background: rgba(0, 0, 0, .6);*/
  }
  .toast {
    position: fixed;
    z-index: 5000;
    width: 100px;
    min-height: 100px;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
    background: rgba(17,17,17,0.7);
    text-align: center;
    border-radius: 10px;
    color: #FFFFFF;
    
    .content {
      padding: 0 6px 10px;
      font-size: 14px;
      word-wrap: break-word;
    }
  }
</style>
```

## 全局实例化

```vue
import Loading from '~/components/common/vue-loading'
Vue.prototype.$Loading = Loading
Vue.use(Loading)
```

## 接口封装

```javascript
import * as Tool from '~/utils/vuex'

Tool.open()
Tool.close()
```


```javascript
import store from '~/store/index.js'
// console.log('showToast')
export const toast = (str, icon) => {
  // console.log('showToast')
  store().dispatch('showToast', true)
  if (icon === 'success') {
    store().dispatch('showSuccess', true)
    store().dispatch('showFail', false)
  } else {
    store().dispatch('showSuccess', false)
    store().dispatch('showFail', true)
  }
  store().dispatch('toastMsg', str)
  setTimeout(() => {
    store().dispatch('showToast', false)
  }, 1500)
  // console.groupEnd()
}

export const alert = (str) => {
  console.log('showAlert')
  store().dispatch('showAlert', true)
  store().dispatch('alertMsg', str)
  setTimeout(() => {
    store().dispatch('showAlert', false)
  }, 1500)
  // console.groupEnd()
}

export const open = (text, open) => {
  console.log(`%cAXIOS ${text}`, 'color:blue;')
  if (open) {
    store().dispatch('openLoading', text)
  }
}

export const close = () => {
  store().dispatch('closeLoading')
  // console.groupEnd()
}
```

```javascript

import * as types from '../mutation-types'
import Loading from '~/components/common/vue-loading'

const state = {
  loading: false,
  loadingList: [],
  loadingCounet: 0,
  loadingcountUp: null,
  showToast: false,
  leftNavStatus: false,
  showSuccess: true,
  showFail: false,
  toastMsg: '操作成功',
  showTimePicker: false,
  alertMsg: '退出登录',
  showAlert: false
}

const actions = {
  openLoading ({ commit }, playload) {
    commit(types.COM_PUSH_LOADING, playload)
  },
  closeLoading ({ commit }) {
    commit(types.COM_SHIFT_LOADING)
  },
  setLoadingState ({ commit }, status) {
    commit(types.COM_LOADING_STATUS, status)
  },
  setNavState ({ commit }, status) {
    commit(types.COM_NAV_STATUS, status)
  },
  showToast ({ commit }, status) {
    commit(types.COM_SHOW_TOAST, status)
  },
  showSuccess ({ commit }, status) {
    commit(types.COM_SHOW_SUCCESS, status)
  },
  showFail ({ commit }, status) {
    commit(types.COM_SHOW_FAIL, status)
  },
  toastMsg ({ commit }, str) {
    commit(types.COM_TOAST_MSG, str)
  },
  showAlert ({ commit }, status) {
    commit(types.COM_SHOW_ALERT, status)
  },
  alertMsg ({ commit }, str) {
    commit(types.COM_ALERT_MSG, str)
  },
  showTimePicker ({ commit }, status) {
    commit(types.COM_SHOW_TIME_PICKER, status)
  }
}

const getters = {
  loading: state => state.loading,
  isLoading: state => state.loadingList.length > 0,
  showToast: state => state.showToast,
  showAlert: state => state.showAlert
}

const mutations = {
  [types.COM_LOADING_STATUS] (state, status) {
    state.loading = status
  },
  [types.COM_PUSH_LOADING] (state, playload) {
    state.loadingList.push({text: playload || '玩命加载中...'})
    Loading.open('加载中……')
    state.count = 1
    state.countUp = setInterval(() => {
      state.count += 1
    }, 1000)
  },
  [types.COM_SHIFT_LOADING] (state) {
    state.loadingList.shift()
    Loading.close()
    clearInterval(state.countUp)
  },

  [types.COM_SHOW_TOAST] (state, status) {
    state.showToast = status
  },

  [types.COM_SHOW_SUCCESS] (state, status) {
    state.showSuccess = status
  },

  [types.COM_SHOW_FAIL] (state, status) {
    state.showFail = status
  },

  [types.COM_TOAST_MSG] (state, str) {
    state.toastMsg = str
  },

  [types.COM_NAV_STATUS] (state, status) {
    state.leftNavStatus = status
  },

  [types.COM_SHOW_TIME_PICKER] (state, status) {
    state.showTimePicker = status
  },

  [types.COM_SHOW_ALERT] (state, status) {
    state.showAlert = status
  },
  [types.COM_ALERT_MSG] (state, str) {
    state.alertMsg = str
  }
}

export default {
  state,
  actions,
  getters,
  mutations
}
```

