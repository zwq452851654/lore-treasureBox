# react
##### react的生命周期
> - componentWillMount: 渲染前调用，用户端和客户端都可以调用
> - componentDidMount: 第一次渲染调用，生成DOM结构
> - componentWillReceiveProps: props被更新时调用
> - shouldComponentUpdate: 在props或state被更新时调用，返回false或者true，当返回false时将不在往下执行对应的周期函数
> - componentWillUpdate: 接受一个新的props或state对this.props或this.state进行赋值
> - componentDidUpdate: 组件更新后调用
> - componentWillUnmount: 组件在移除dom之前调用



# js问题
##### 防抖、节流
> - 防抖：指的事在连续触发事件的情况下，在指定时间内只执行一次，如果在指定时间内又触发了，那就重现计算开始时间
> - 节流：指的是在连续触发后的n秒内指执行一次，减少函数执行的频次

#### js作用域
> 指的是：每个变量和函数都有其作用范围，超出无效，这个叫做作用域

#### js基础
> - 举例3种强制类型转换和2中隐式类型转换
>   - 强制类型：parseInt、parseFloat、Number
>   - 隐式类型： = =   、  = = =
> - 数组的几个方法：
>   - filter: 数组中的元素不变，个数可能参数变化
>   - map: 数组中的个数不变，但数组元素发生改变
>   - some: 判断数组中的元素是否满足指定的条件，其中一项满足条件则返回true
>   - every: 判断数组中的元素是否都满足指定的条件，其中一项不满足则返回false，反之返回true


##### js原型及继承
> - 属性继承：call、apply：使用会比较耗内存
> - 原型继承：将new出来的实例赋值给要继承的对象（继承被继承对象的所有属性和方法）
> - 原型拷贝：
>   1. 通过for in 被继承对象prototype上的属性方法进行拷贝
>   2. 直接 new 一个实例进行拷贝
> - 原型链继承：将被继承的对象直接new给另一对象的prototype，然后通过_protot__进行链式查找
> - 混合继承： 将子类名对象的prototype的constructor指向自己，然后把 __proto__ 指向被继承对象的prototype
> - ES6的继承：通过class 子类名 extends 父类名 然在constructor里使用super()进行继承

##### es6的箭头函数和普通函数的区别
> - 没有prototype，所以没有自己的this
> - 不能作为构造函数进行使用
> - 没有自己的anguments



##### Promise:
> - 因js的代码都是单线程的且都是同步执行，promise是为了解决异步编程提供的一种方案
> - 有三种状态分别为: pending、fulfilled、rejected
> - promise由new关键字及其构造函数创建，有两个参数分别为：resolve、reject
> - 异步操作成功，成功结果作为参数传入resolve
> - 异步操作失败，失败结果作为参数传入rejted
> - 然后以then的方法接收参数并进行对应的处理
> - promise.all方法: 参数为数组或者字符串，传入的参数一个失败则整体失败，反正则成功
> - promise.finally: 无论执行结果怎么都将执行此方法


##### js闭包
>  - 什么是闭包: 闭包指的有权访问另一个函数作用域变量的函数
>    - 特性:  
>    1. 函数里嵌套函数；
>    2. 函数内部可以引用函数外部的参数和变量；
>    3. 参数和变量不被垃圾回收机制所回收
>    - 好处:  
>    1. 保护私有变量安全，实现封装； 
>    2. 内存中维护一个变量，可以做缓存； 
>    3. 匿名自执行函数可以减少内存消耗
>    - 坏处: 
>    1. 私有变量不被销毁，增大内存消耗，造成内存泄漏;
>    2. 闭包设计跨作用域访问，存在性能损失



##### http和https的区别，应用场景
> - 区别:
>   - http是超文本传输协议，是明文传输，https是具有安全性的ssl加密传输协议
>   - 连接方式不同，默认端口也不用，前者80，后者443
>   - http连接是无状态的	
> - 工作特点和流程
>   - http是一个由请求和响应组成，由客户端向服务端发起，且无状态


##### new操作符具体干了什么呢?
> - 创建一个空对象，并把this指向该对象，并集成该函数的原型
> - 把属性和方法都加到this这个对象里


# vue
##### mvvm的理解

##### route 原理   
> vue Router 是用过hash和history两种方式实现前端路由

##### vue组件中的data为什么必须是一个函数
> - data以函数返回值的形式定义，这样每次复用组件的时候都会得到一份新的data
> - 相当于每个组件实例都有一个私有的数据空间，各自维护各自的，不会造成混乱
> - 单纯的写成对象形式，这样所有的组件都共有了一个data，这样改一个就全部都改了


##### 对响应式数据的理解
- 数据类型分为两种：数组和对象
- 对象：核心就是通过**Object.defineProperty**进行劫持
- 在初始化数据的时候给data中的所有属性使用Object.defineProperty重写定义，当页面取对应的属性时会进行依赖收集，当数据发生改变的时候通知相关的依赖进行更新操作
- 数组：通过**函数劫持**的方式，重写了数组的方法
- 将data中的数组，进行原型链改写，指向自定义的数组方法，在当调用数组方法时其实执行的就是改写后的方法，这样就可以通知依赖进行更新了

##### 为什么vue采用异步渲染
- 因vue是组件级的更新，为防止一改数据就进行更新，所有采用异步更新，提升性能
- 做法：就是将多个watcher放到一个队列里，并进行相同依赖的过滤，当数据都修改完成的时候在去异步执行

##### nextTick实现原理
> 在调用nextTick的时候将传入的callback方法存在一个数组中，然后通过promise回调
> 在进行回调的时候进行判断兼容性：
- 首先尝试采用promise回调
- 再尝试采用MutationObserver回调
- 再尝试采用setImmediate回调
- 最终采用setTimeout回调


##### vue中computed的特点
> 做了一个dirty 实现了缓存机制，默认为true，在执行过后修改为false，当依赖的属性改变后再改为true，然后重新计算，否则每次取的都是上一次计算的值

##### computed watch method的区别
> - method 只要把方法用到模板上了，只要一变化就会重写渲染，性能开销较大
> - computed  具体缓存的特性，只有依赖的属性发现变化了才会重新计算（一个数据受多个数据影响）
> - watch 只要数据一变就立马执行（一个数据影响多个数据）

##### watch原理
> - 在组件初始化的时候，会调用initWatcher函数，给所有进行监听的属性进行实例化
> - 然后在new Watcher时会传入对应的key值，cb和options
> - 然后在结尾还会调用watcher.prototpye.get()方法，将获取到值并存在watcher.value中
> - 在执行get时进行依赖收集，实现对属性的监听。
> - 最后在数据进行变更时去执行watcher.prototype.update()

##### watch中的deep、immediate
> - deep：设置为true时可监听到对象的某个值发生改变
> - immediate：设置true时，将以当前表达式的值进行触发回调

##### vue的生命周期
> - beforeCreate
> - created
> - beforeMount
> - mounted
> - beforeUpdate
> - updated
> - beforeDestroy
> - destroyed

##### 用VNode来描述一个dom结构
> ... ...

##### 简述vue中的diff算法原理
> 1. 先同级比较，在比较子节点
> 2. 判断一方有儿子一方没有儿子的情况
> 3. 比较都有儿子的情况
> 4. 递归比较子节点

##### v-html的使用会带来什么问题
> - 可能会导致xss的攻击，
> - v-html更新的是html元素的innerHTML，不会进行vue的模板编译，而是当做普通的html插入
> - 组件中的scoped对v-html插入的html不起作用，因为html没有被vue的模板编译器所处理
> - 返回的js不会被执行，因为浏览器在渲染的时候并没有将此js进行渲染（解决方法：可以在nextTick中动态创并插入script标签）

##### vue 的插槽
> - 什么是作用域插槽：就是父组件在向子组件传递插槽模板时要使用子组件件数据的问题，因为他们各自的模板都是在各自的作用域中编译的（解决方法：可以将插槽的数据作为属性进行v-bind绑定传递）



##### 描述组渲染和更新过程
> - 组件渲染描述：组件渲染时会通过vue.extend方法构建子组件的构造函数，并进行实例化，最终手动调用$mount()进行挂载
> - 更新过程：修改data，触发setter -> 执行rander函数生成新的newVnode -> 然后patch，核心就是diff算法

##### vue的事件绑定原理
> - 原生dom事件绑定采用的是addEventListener实现的
> - 组件绑定的事件采用$on方法


##### v-model的实现原理及如何自定义v-model
> v-model在内部为不同输入元素使用不同的属性及绑定不同的事件
> - input和textarea元素使用的value和input事件
> - choutbox和radio使用的是value和change
> - select 是value和change事件


##### 父子组件的渲染顺序
> ... ...


##### 组件的通信
> - 父向子通过props，子向父通过$on、$emit
> - 获取父子组件实例的方式：$parent、$children
> - 通过写ref的方式调用组件的属性或方法
> - event Bus 跨组件通信
> - vuex

##### vue中相同逻辑如何抽离
> vue.mixin(混入)

##### 为什么要使用异步组件
> 当一个组件比较复杂且庞大的时候使用异步组件会更高效，实现按需加载


##### keep-alive的了解
> 对组件进行缓存
> - 两个属性：include：匹配到的组件进行缓存、exclude：匹配到的组件不被缓存
> - 两个生命周期：当组件被缓存的时候组件的生命周期将失效，然后取代的则是activated、deactivated
> - LRU算法

##### vue3有哪些改进
> - 采用了ts来编写
> - 支持 composition API
> - 响应式数据原理改成proxy
> - vdom的对比算法更新，只更新绑定了动态数据的部分vdom

##### vue-router中的导航守卫有哪些
> - 全局：
>   - beforeEach
>   - afterEach
> - 路由守卫：
>   - beforeEnter
> - 组件内的：
>   - beforeRouteEnter
>   - beforRouteUpdate
>   - beforRouteLeave


##### 代码优化
> - 不要将所有的数据都放到data里，因为data里的数据都会增加setter和getter，会收集对应的watcher
> - vue在v-for时需要给每个元素绑定事件时可以用事件代理
> - 利用好keep-alive缓存组件
> - 组件的拆分
> - 根据需求使用好v-if和v-show
> - key值的使用，确保唯一性，避免使用索引
> - Object.freeze冻结数据
> - 合理使用路由懒加载和组件异步加载









