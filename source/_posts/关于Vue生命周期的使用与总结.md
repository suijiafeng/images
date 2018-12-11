title: 关于Vue生命周期的使用与总结
author: suijiafeng
tags: []
categories: []
date: 2018-06-19 22:45:00
---


 所有的生命周期钩子自动绑定 this 上下文到实例中，因此可以通过其访问数据、运算等，下边会按照生命周期函数执行顺序来讲解


1. beforeCreate

    实例初始化后，创建完成之前被调用

2. created

    实例创建完成后被立即调用，这个时候还没有开始挂载 不能访问 $el

3. beforeMount

    挂载开始之前调用，即将开始挂载

    对比：对应 react componentWillMount 在完成首次渲染之前调用 此时仍可以修改组件的状态

4. mounted

    实例挂载之后调用，但是并不是所有子组件也都一起挂载完成，如果需要整个视图渲染完毕 可以使用 this.$nextTick(function () {})

    对比：对应 react componentDidMount 完成首次渲染之后调用， 可以在这里操作DOM

5. beforeUpdate

    数据更新完成前调用，发生在虚拟DOM重新渲染和打补丁前，在这里进一步的更改状态，不会触发重新渲染

    对比：对应 react componentWillUpdate 接受状态的改变，进行渲染之前调用，不同的是 vue 中允许在这一步更改状态；而 react 则禁止，如果要更改状态要在 react 的 componentWillReceiveProps 声明周期中进行

6. updated

    更改数据重新渲染虚拟DOM后调用，在这里，组件DOM已经更新，可以执行依赖DOM的操作，但是应该避免在这里更改状态，与 mounted 一样，不能保证所有子组件都挂载完成，可以使用 this.nextTick(function () {})` 进行全部渲染完的操作

    对比：对应 react componentDidUpdate 完成渲染新的props或者state后调用，此时可以访问到新的DOM元素

7. beforeDestroy

    实例销毁之前调用，在这一步，实例仍然可用

    对比：对应 react componentWillUnmount 组件销毁之前调用，做一些清理工作

8. destroyed

    实例销毁之后调用

    对比：react 中没有这个生命周期钩子

9. 其他

    react 中有 componentWillReceiveProps 这个钩子，用来组件接受更新时调用，可以再次更新 props 或者 state, 在 vue 中虽然没有这个声明周期钩子，但是 vue 实例提供一个 watch 属性，可以用来监视状态改变，与 componentWillReceiveProps 功能类似

    react 中有 shouldComponentUpdate 这个钩子，用来判断决定组件是否需要更新，以减少重新渲染，提升性能；在 vue 中组件是否需要更新，由 vue 框架主动判断，不在需要开发者在这个函数中操作了


总结一下他们大致的用处：![](http://suijiafeng.com/images/bg.jpg)

    beforecreate : 可以在这加个loading事件

    created ：在这结束loading，还做一些初始化，实现函数自执行 

    mounted ： 在这发起axios请求，拿回数据，配合路由钩子做一些事情

    beforeDestory： destoryed ：当前组件已被删除，清空相关内容

