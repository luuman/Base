title:  ES6 节流和防抖详解
date: 2019-08-27 14:11:20
description: 
categories:
- Induce
tags:
- JavaScript
toc:
author:
comments:
original:
permalink: 
image: http://www.easyfinance.com.cn/Finance/images/Article/2019-02/21-09-50-55500711650_banner.jpg
---
　　**自用笔记：**在浏览器`DOM`事件里面，有一些事件会随着用户的操作不间断触发。比如：重新调整浏览器窗口大小（resize），浏览器页面滚动（scroll），鼠标移动（mousemove）。也就是说用户在触发这些浏览器操作的时候，如果脚本里面绑定了对应的事件处理方法，这个方法就不停的触发。
这并不是我们想要的，因为有的时候如果事件处理方法比较庞大，DOM 操作比如复杂，还不断的触发此类事件就会造成性能上的损失，导致用户体验下降（UI 反映慢、浏览器卡死等）。所以通常来讲我们会给相应事件添加延迟执行的逻辑。
debounce 与 throttle 是开发中常用的高阶函数，作用都是为了防止函数被高频调用，换句话说就是，用来控制某个函数在一定时间内执行多少次。
<!-- more -->

## 效果可视化
<div class="box">
  <div id="moveonme" >
    在此区域移动你的鼠标
  </div>
  <canvas id="paintonme" width="800" height="600"></canvas>
</div>

## 节流概念(Throttle)
定义： 如果一个函数持续的，频繁地触发，那么让它在一定的时间间隔后再触发。由于执行速度过快，并携带相邻数据相差不大，节流可以高效的优化执行效果。

### 应用场景
> scroll、touchmove

### 节流实现

#### 首次执行
通过时间比对，屏蔽多次提交，缺点：最后一个动作不会被触发
```javascript
function throttles(fn, wait = 100){
  let last = 0;
  console.log('节流函数 启动')
  return function(){
    let curr = +new Date();
    // 强制转换为数字Number
    if(curr - last > wait){
      fn.apply(this, arguments);
      last = curr;
    }
  }
}
let fun = new throttle(test, 2000)
function test(e) {
  console.log(e)
}
let funss = (m, n) => Array.apply(null, new Array(m)).map(() => n++)
let arr = funss(100, 1)
arr.forEach(item => {
  fun('funcs')
})
// 节流函数 启动
// funcs

window.onresize = throttle(test, 200);
window.onresize = function () {
  fun('funcs')
}
```

#### 首次不执行
首次不执行，`delay`时间内只执行滞后一次，通过判断`timer`，进行判断延迟执行，预执行期间，去除其他执行请求。
```javascript
function throttles2(fn, delay = 100){
  //首先设定一个变量，在没有执行我们的定时器时为null
  let timer = null;
  return function(){
    //当我们发现这个定时器存在时，则表示定时器已经在运行中，需要返回
    if(timer) return;
    timer = setTimeout(() => {
      fn.apply(this,arguments);
      timer = null;
    }, delay);
  }
}
function test(e) {
  console.log(e)
}
let fun = new throttle(test, 2000)
let funss = (m, n) => Array.apply(null, new Array(m)).map(() => n++)
let arr = funss(100, 1)
arr.forEach(item => {
  fun('funcs')
})
```
### throttle
优点：成功的优化最后一针的位置
```javascript
function throttle (fn, wait = 250, options) {
  let lastTime, timerId
  return function () {
    let context = options || this
    let currentTime = +new Date
    let args = arguments
    if (lastTime && currentTime < lastTime + wait) {
      clearTimeout(timeId)
      timeId = setTimeout(function() {
        lastTime = currentTime
        fn.apply(context, args)
      }, wait);
    } else {
      lastTime = currentTime
      fn.apply(context, args)
    }
  }
}
```

### lodash
缺点无法获取参数，时间比对问题，属于首次执行的防抖的方法
```javascript
function throttle(fn, wait, options) {
  wait = wait || 0;
  var timerId, lastTime = 0;
  function throttled() {
    var currentTime = new Date();
    if (currentTime >= lastTime + wait) {
      fn();
      lastTime = currentTime;
    } else {
      if (timerId) {
        clearTimeout(timerId);
        timerId = null;
      }
      timerId = setTimeout(function() {
        fn()
      }, wait);
   }
  }
  return throttled;
}
```

### underscore
underscore提供了一系列函数式接口
```javascript
// 返回一个函数，只要这段时间被调戏就不会触发。函数停止后N毫秒触发，
debounce = function(func, wait, immediate) {
  var timeout, result;
  var later = function(context, args) {
    timeout = null;
    if (args) result = func.apply(context, args);
  };
  var debounced = restArgs(function(args) {
    if (timeout) clearTimeout(timeout);
    if (immediate) {
      var callNow = !timeout;
      timeout = setTimeout(later, wait);
      if (callNow) result = func.apply(this, args);
    } else {
      timeout = _.delay(later, wait, this, args);
    }
    return result;
  });
  debounced.cancel = function() {
    clearTimeout(timeout);
    timeout = null;
  };
  return debounced;
};
let fun = new debounce(test, 2000)
let funss = (m, n) => Array.apply(null, new Array(m)).map(() => n++)
let arr = funss(100, 1)
arr.forEach(item => {
  fun('funcs')
})

// Returns a function, that, when invoked, will only be triggered at most once
// during a given window of time. Normally, the throttled function will run
// as much as it can, without ever going more than once per `wait` duration;
// but if you'd like to disable the execution on the leading edge, pass
// `{leading: false}`. To disable execution on the trailing edge, ditto.
throttle = function(func, wait, options) {
  var timeout, context, args, result;
  var previous = 0;
  if (!options) options = {};
  var later = function() {
    previous = options.leading === false ? 0 : new Date();
    timeout = null;
    result = func.apply(context, args);
    if (!timeout) context = args = null; //显示地释放内存，防止内存泄漏
  };
  var throttled = function() {
    var now = new Date();
    if (!previous && options.leading === false) previous = now;
    var remaining = wait - (now - previous);
    context = this;
    args = arguments;
    if (remaining <= 0 || remaining > wait) {
      if (timeout) {
        clearTimeout(timeout);
        timeout = null;
      }
      previous = now;
      result = func.apply(context, args);
      if (!timeout) context = args = null;
    } else if (!timeout && options.trailing !== false) {
      timeout = setTimeout(later, remaining);
    }
    return result;
  };
  throttled.cancel = function() {
    clearTimeout(timeout);
    previous = 0;
    timeout = context = args = null;
  };
  return throttled;
};
```


## 防抖概念(Debounce)
定义： 如果一个函数在一段时间间隔中，持续地触发，那么只在它结束后过一段时间只执行一次。

注意：这里的抖动停止表示你停止了触发这个函数，从这个时间点开始计算，当间隔时间等于你设定时间，才会执行里面的回调函数。如果你一直在触发这个函数并且两次触发间隔小于设定时间，则一定不会到回调函数那一步。·

### 应用场景
> input验证、搜索联想、resize

防抖实现
思路：首次运行时把定时器赋值给一个变量，第二次执行时，如果间隔没超过定时器设定的时间则会清除掉定时器，重新设定定时器，依次反复，当我们停止下来时，没有执行清除定时器，超过一定时间后触发回调函数。

### 首次立即执行
首次执行，延后多次执行的最后一次时间。同上
```javascript
function throttle(fn, wait = 100, options) {
  let timerId, lastTime = 0;
  console.log('节流函数 启动')
  return function() {
    let currentTime = new Date();
    if (currentTime >= lastTime + wait) {
      console.log(timerId, lastTime)
      fn.apply(this, arguments);
      lastTime = currentTime;
    } else {
      if (timerId) {
        clearTimeout(timerId);
        timerId = null;
      }
      timerId = setTimeout(() => {
        console.log(timerId, lastTime)
        fn.apply(this, arguments);
      }, wait);
    }
  }
}
function test(e) {
  console.log('test', e)
}
let fun = new throttle(test, 2000)
let funss = (m, n) => Array.apply(null, new Array(m)).map(() => n++)
let arr = funss(100, 1)
arr.forEach(item => {
  console.log(item)
  fun('funcs')
})
```

### 延迟执行最后一个指令
```javascript
function debounce(fn, delay) {
  let timerId;
  return function (...args) {
    if (timerId) {
      clearTimeout(timerId);
    }
    timerId = setTimeout(() => {
      fn(...args);
      timerId = null;
    }, delay);
  }
}
```

```javascript
function debounce (fn, wait, options) {
  var timeout;
  return function () {
    var context = options || this, args = arguments;
    var later = function () {
      timeout = null;
      fn.apply(context, args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
},
```

```javascript
function debounce(fn, wait, options) {
  var timer = null;
  var previous = null;
  return function () {
    var now = +new Date();
    if ( !previous ) previous = now;
    if ( options && now - previous > options ) {
      fn();
      // 重置上一次开始时间为本次结束时间
      previous = now;
      clearTimeout(timer);
    } else {
      clearTimeout(timer);
      timer = setTimeout(function() {
        fn();
        previous = null;
      }, wait);
    }
  }
};
```
```javascript
function debounce(fn, delay = 200, atBegin = true) {
  let timer = null, last = 0,during;
  return function () {
    let self = this, args = arguments;
    var exec = function () {
      fn.apply(self, args);
    }
    if (atBegin && !timer) {
      exec();
      atBegin = false;
    } else {
      during = Date.now() - last;
      if (during > delay) {
        exec();
      } else {
        if (timer) clearTimeout(timer);
        timer = setTimeout(function () {
          exec();
        }, delay);
      }
    }
    last = Date.now();
  }
}
```

```javascript
// 避免在滚动时过分的更新定位
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// 点击后就调用 `renewToken`，但5分钟内超过1次。
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);

// 取消一个 trailing 的节流调用
jQuery(window).on('popstate', throttled.cancel);
```

```javascript
// 避免窗口在变动时出现昂贵的计算开销。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// 当点击时 `sendMail` 随后就被调用。
jQuery(element).on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
}));

// 确保 `batchLog` 调用1次之后，1秒内会被触发。
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
var source = new EventSource('/stream');
jQuery(source).on('message', debounced);

// 取消一个 trailing 的防抖动调用
jQuery(window).on('popstate', debounced.cancel);
以上就是节流和防抖的全部介绍
```



<!-- <iframe width="100%" height="700px" src=""></iframe> -->

<style>
  body {
    font-family: "Roboto","Helvetica",Arial;
    font-weight: 200;
  }
  .box{
    width: 100%;
    overflow: hidden;
  }
  #moveonme {
    width: 100%;
    height: 200px;
    border: 1px solid #aaa;
    box-sizing: border-box;
    padding: 25px;
    text-align: center;
    font-size: 18px;
  }
  .backtoblog {
    width: 200px;
    padding: 10px;
    background: #f5f5f5;
    border: 1px solid #aaa;
    color: #777;
    display: inline-block;
    text-decoration: none;
    transition: 0.2s all;
    box-sizing: border-box;
    position: relative;
    top: -1px;
    text-align: center;
  }
  #paintonme{
    /*background: #FFF;*/
  }
  .backtoblog:hover {
    border: 1px solid #aaa;
    background: transparent;
  }
</style>

<script type="text/javascript">
  var helpers = {
    /**
     * debouncing, executes the function if there was no new event in $wait milliseconds
     * @param func
     * @param wait
     * @param options
     * @returns {Function}
     */
    debounce: function (fn, wait, options) {
      var timeout;
      return function () {
        var context = options || this, args = arguments;
        var later = function () {
          timeout = null;
          fn.apply(context, args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
      };
    },
    throttles: function (fn, wait = 200, options) {
      let last = 0;
      console.log('节流函数 启动')
      return function(){
        let curr = +new Date();
        // 强制转换为数字Number
        if(curr - last > wait){
          fn.apply(this, arguments);
          last = curr;
        }
      }
    },
    /**
     * in case of a "storm of events", this executes once every $threshold
     * @param fn
     * @param threshhold
     * @param options
     * @returns {Function}
     */
    throttle: function (fn, wait = 250, options) {
      var lastTime, timerId;
      return function () {
        var context = options || this;
        var currentTime = +new Date,
          args = arguments;
        if (lastTime && currentTime < lastTime + wait) {
          // hold on to it
          clearTimeout(timerId);
          timerId = setTimeout(function () {
            lastTime = currentTime;
            fn.apply(context, args);
          }, wait);
        } else {
          lastTime = currentTime;
          fn.apply(context, args);
        }
      };
    }
  }
  function NIM_demo(){
    this.canvas =   document.getElementById("paintonme");
    this.context =  this.canvas.getContext("2d");
    this.movearea = document.getElementById("moveonme");
    this.canvasTimeScale = 5 * 1000;
    this.paintColors = ["#bbd", "#464", "#d99", "#d77", "#d44"];
    this.totalLanes =  this.paintColors.length;
    this.leftMargin = 100;
    var self = this;
    this.init = function(){
      // this.canvas.width = window.innerWidth - 200;
      this.flush();
      this.movearea.addEventListener("mousemove", this.regularHandler);
      this.movearea.addEventListener("mousemove", helpers.debounce(self.debounceHandler, 100, this));
      this.movearea.addEventListener("mousemove", helpers.throttle(self.throttleHander, 100, this));
      this.movearea.addEventListener("mousemove", helpers.throttles(self.throttleHanders, 100,this));
    }
    /**
     * painting the rectangle / line
     * @param lane
     * @param time
     */
    this.paintRect = function(lane,time){
      if(time > this.canvasTimeScale){
        this.startTime += time;
        time = 0;
        this.flush()
      }
      // console.log(lane,time);
      this.context.fillStyle = this.paintColors[lane];
      var x = (this.canvas.width - this.leftMargin) / this.canvasTimeScale * time + this.leftMargin;
      var y = this.canvas.height / this.totalLanes * lane;
      var height = this.canvas.height / this.totalLanes;
      var width = 1;
      this.context.fillRect(x, y, width, height);
    }
    this.flush = function(){
      this.context.fillStyle = "#000";
      this.context.fillRect(0,0,this.canvas.width,this.canvas.height);
      this.context.font = "200 18px Roboto,Helvetica,Arial";
      this.context.fillStyle = this.paintColors[0];
      this.context.fillText("Regular", 0, 100);
      this.context.fillStyle = this.paintColors[1];
      this.context.fillText("debounce", 0, 200);
      this.context.fillStyle = this.paintColors[2];
      this.context.fillText("throttle", 0, 300);
      this.context.fillStyle = this.paintColors[3];
      this.context.fillText("throttles", 0, 400);
    }
    /**
     * get the time difference
     * @returns {number}
     */
    this.getTimeDiff = function(){
      var time = new Date().getTime();
      if(!this.startTime){
        this.startTime = time;
      }
      time -= this.startTime;
      return time;
    }
    this.regularHandler = function(){
      self.paintRect(0, self.getTimeDiff());
    }
    this.debounceHandler = function(){
      self.paintRect(1, self.getTimeDiff());
    }
    this.throttleHander = function(){
      self.paintRect(2, self.getTimeDiff());
    }
    this.throttleHanders = function(){
      self.paintRect(3, self.getTimeDiff());
    }
  }
  var demo = new NIM_demo();
  demo.init();
</script>