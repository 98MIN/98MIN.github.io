### 防抖节流

#### 防抖

> 当需要执行的方法频繁被触发时，只有当中间间隔超过指定时间间隔，方法才会执行


#### 防抖的使用场景：

 - 联想输入框：用户输入时要进行联想反馈
 - 监听屏幕resize：在监听函数外包裹一层防抖函数

#### 防抖函数实现
```js
    function debounce(fn,delay){
      let timer = null
      return function(){
        clearTimeOut(timer)
        timer = setTimeOut(() => {
          fn.apply(this,arguments)
        },delay)
      }
    }
```

#### 节流

> 当需要执行的方法频繁被触发，只有经过指定时间间隔之后方法才会被触发。

#### 节流的使用场景

- 监听滚动事件
- 鼠标不断点击触发

#### 节流函数实现

```js
    function throttle(fn, delay) {
      let time = ''

      return function () {
        let newDate = Date.now()

        if (newDate - time > delay) {
          fn.apply(this, [...arguments])
          time = newDate
        }
      }
    }
```
