### 组件生命周期问题引发的思考
#### 场景描述
A组件嵌套了B组件，B组件的子组件C依赖A提供的数据进行数据请求

![嵌套大意图](life-cycle/context1.png '嵌套大意图')

#### 解决方案
- 使用props逐级传递
![props传递图](life-cycle/context2.png 'props传递图')
通过props逐级传递，在子组件中获取到值进行消费使用。不过这样的处理方式太过复杂，如果组件嵌套不深倒也还好，一旦组件嵌套太深后期维护会很难。
- 使用上下文
> context提供了一个无需为每层组件手动添加props就能在组件树间进行数据传递的方法

![context传递图](life-cycle/context3.png 'context传递图')
通过context生成需要的数据传递给子级，子级进行消费，不需要一级一级去传递props



通过比较，果断选择第二种！context无敌！
#### 问题描述
一切都向着预期有条不紊的进行~就在这时问题来了——子组件的确通过context跨组件获取到了生产者传递的值，但是却是初始值，并不是更新的值。这里要说明一下，在生产者组件中的componentDidMount中有通过请求去更新context，但是在子组件的componentDidMount中却没有获取到这个值。

#### 问题排查
通过debugger发现在子组件的didMount生命周期里面的context并没有如我们所预料的是更新之后的值。问题出在哪呢？明明已经在生产组件中进行了请求更新数据呀！为什么会获取不到呢？等等...我们在生产组件的didMount里面...猜测有可能是因为生命周期执行顺序的原因，于是进行了一番测试。

#### 拨开云雾
![context测试](life-cycle/context4.png 'context测试')
由上图可以看出父子组件渲染流程大致为：
1. 执行父组件render，然后进入子组件
2. 执行子组件的render
3. 如果子组件中还有子组件则重复上面的步骤。
4. 执行子组件的didMount
5. 执行父组件的didMount。
![执行顺序图例](life-cycle/context5.png '执行顺序图例')

#### 最终解决
既然明白了render的一个关系，就很好解决了，在子组件的update生命周期里面监听，进行数据更行就ok了！nice~













