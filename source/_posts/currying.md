### 柯里化

参考文章: [js系列文章之函数柯里化](https://github.com/mqyqingfeng/Blog/issues/42)

#### 定义
> In mathematics and computer science, currying is the technique of translating the evaluation of a function that takes multiple arguments into evaluating a sequence of functions, each with a single argument.

翻译成中文:

在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。


#### 理解
通过闭包将参数保存并判断是否达到执行函数的临界点（参数个数是否大于或等于等待执行的函数参数个数）。达到则开始执行，否则继续执行Currying函数。


#### 实现
```js
/**
 * 函数柯里化
 * @param {*} fn
 * @param  {...any} params
 */

function currying(fn, ...params) {
  return function(...args) {
    let _args = [...params, ...args]

    if (_args.length >= fn.length) {
      return fn.apply(this, _args)
    } else {
      return currying.call(this, fn, ..._args)
    }
  }
}
```
