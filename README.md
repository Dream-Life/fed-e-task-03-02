# fed-e-task-03-02
大前端进阶 - 阶段三 - 模块二



Vue.js 源码剖析-响应式原理、虚拟 DOM、模板编译和组件化

一、简答题

1、请简述 Vue 首次渲染的过程。

​	  首先初始化vue实例，执行this.__init()，初始化实例成员和静态成员；执行vm.$mount()，先判断vm中有无render；没有render，通过compileToFunctions将template转变成render；之后执行mountComponent方法，mountComponent方法中先触发beforeMount方法，再声明了updateComponent用于更新dom，并绑定到新建的watcher中，之后触发mounted方法；创建完Watcher时会调用get一次，也就是会执行一次updateComponent，调用render方法，将vm上的render或template转换的render转换成vnode，之后调用方法内部的update方法也就是patch方法，将$el真实dom转换成的vnode和之前生成的vnode加载到真实dom上

2、请简述 Vue 响应式原理。

3、请简述虚拟 DOM 中 Key 的作用和好处。

4、请简述 Vue 中模板编译的过程。