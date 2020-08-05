# fed-e-task-03-02
大前端进阶 - 阶段三 - 模块二



Vue.js 源码剖析-响应式原理、虚拟 DOM、模板编译和组件化

一、简答题

1、请简述 Vue 首次渲染的过程。

​	  首先初始化vue实例，执行this.__init()，初始化实例成员和静态成员；执行vm.$mount()，先判断vm中有无render；没有render，通过compileToFunctions将template转变成render；之后执行mountComponent方法，mountComponent方法中先触发beforeMount方法，再声明了updateComponent用于更新dom，并绑定到新建的watcher中，之后触发mounted方法；创建完Watcher时会调用get一次，也就是会执行一次updateComponent，调用render方法，将vm上的render或template转换的render转换成vnode，之后调用方法内部的update方法也就是patch方法，将$el真实dom转换成的vnode和之前生成的vnode加载到真实dom上

2、请简述 Vue 响应式原理。

​		在初始化vue实例时执行initState方法，在initData中，使用observe绑定数据，observe会返回一个Observe类，在Observe类中便利data的数据使用defineReactive进行数据劫持，其中的get方法会收集watcher依赖到dep中，set方法会调用dep.notify()遍历执行dep中的更新函数进行dom更新；当数据变动会出发set方法进行dom更新

3、请简述虚拟 DOM 中 Key 的作用和好处。

​		Key 的作用：设置key可以在比较新旧节点时，对比key值，判断节点是否一样

​		Key 的好处：可以减少dom操作，可以将节点重用

4、请简述 Vue 中模板编译的过程。

​		先判断是否有template，有的话就执行compileToFunctions方法，这个方法 中先从缓存中加载编译好的render，如果缓存中没有，就调用complie，合并options配置，再进入baseComplie方法，通过parse方法将template变成抽象语法树AST，在经过optimize方法将AST进行优化，即将静态树进行标记，可以在patch时跳过静态树，最后通过generate方法返回对应的js字符串和静态树，到此complie执行完成，之后再执行compileToFunctions之后的代码将js字符串转换成函数，最终将函数和静态树放到res下缓存到cache[key]中。