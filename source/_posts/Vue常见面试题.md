---
title: vue 常见面试题（持续更新ing...）
date: 2020-09-24 10:00:14
tags: vue
categories: vue
cover: "/img/articleImg/vue.png"
top: 1
---

# vue 常见面试题

1. vue 优点

  - 轻量级框架，只关注视图层，是一个构建数据的视图集合，大小只有几十 kb；简单易学：国人开发，中文文档，不存在语言障碍，易于理解和学习

  - 双向数据绑定：保留了 Angular 的特点，在数据操作方面更为简单

  - 组件化：保留了 React 的优点，实现了 html 的封装和重用，在构建单页面应用方面有着独特的优势

  - 视图，数据，结构分离：使数据的更改更为简单，不需要进行逻辑代码的修改，只需要操作数据就能完成相关操作

  - 虚拟 DOM：DOM 操作是非常耗费性能的，不再使用原生的 dom 操作节点，极大解放了 DOM 操作

2. 父组件如何向子组件传递数据？

  在父组件中，调用子组件的标签上以属性绑定的方式进行传递值，子组件通过 props 进行接收，数据不可直接更改

3. 子组件如何向父组件传递数据？

  在子组件调用 \$emit 方法，定义一个方法名，然后后面跟需要传递的参数，在父组件中，调用子组件的标签上通过 @定义的方法名=自定义方法，去接收子组件传递的数据

4. v-show 和 v-if 指令的共同点和不同点

  - 共同点是这两个指令都能控制元素的显示和隐藏

  不同点就是

  - v-if 会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。它是惰性的，如果在初始渲染时条件为假，则不会渲染，直到条件第一次变为真时，才会开始渲染条件块

  - v-show 不管初始条件是什么，元素总是会被渲染，只是简单地切换元素的 CSS 属性 display

5. 如何让 CSS 只在当前组件中起作用

  在 style 标签上加上 scoped 即可

6. <keep-alive></keep-alive>的作用是什么?

  keep-alive 可以在组件切换时，保存其包裹的组件的状态，使其不被销毁，防止多次渲染。其拥有两个独立的生命周期钩子函数 actived 和 deactived，使用 keep-alive 包裹的组件在切换时不会被销毁，而是缓存到内存中并执行 deactived 钩子函数，命中缓存渲染后会执行 actived 钩子函数

7. 如何获取 dom

  - 可以通过 js 原生方法获取相应的元素

  - 在标签上添加 ref="name", 然后在代码中 this.\$refs.name 就获取到该标签了

8. 说出几种 vue 当中的指令和它的用法？

  - v-model: 数据绑定

  - v-if、v-show: 控制元素的显示和隐藏

  - v-bind: 属性绑定

  - v-on: 事件绑定

  - v-once: 只绑定一次(只渲染该元素或组件一次, 不会根据数据的改变而改变)

  - v-for: 数据循环

9. vue-loader 是什么？使用它的用途有哪些？

  - vue 文件的一个加载器, 将 /template/js/style 转换成 js 模块
  - 用途: js 可以写 es6、style 样式可以用 scss 或 less, template 可以用 jade 等

10. 为什么使用 key

  - 用 key 给每个元素添加一个唯一的标识, Diff 算法就可以正确的识别此节点, 主要作用就是为了高效的更新虚拟 DOM

11. axios 及安装

  - axios 是一个请求后台资源的模块, 通过 npm install axios --save 安装, 在 js 中通过 import 导入该模块, 然后 .get 或 .post, 如果成果则返回 .then 函数, 失败则返回 .catch 函数

12. axios 解决跨域

  ```
      // step1 通过 proxy 解决跨域, 配置一个 BaseURL
      Axios.defaults.baseURL = '/api'
      // step2 修改配置文件
      module.exports = {
          devServer: {
              proxy: {
                  '/api': {
                      // 此处的写法，目的是为了 将 /api 替换成 https://www.baidu.com/
                      target: 'https://www.baidu.com/',
                      // 允许跨域
                      changeOrigin: true,
                      ws: true,
                      pathRewrite: {
                          '^/api': ''
                      }
                  }
              }
          }
      }
  ```

13. v-model 的使用
  - v-model 用于表单数据的双向绑定, 其实就是一个语法糖, 背后就做了两个操作: 1. v-bind 绑定一个 value 属性, 2. 通过 v-on 给当前元素绑定 input 事件

14. Vue3 为什么使用 Proxy 代替 Object.definedProperty

  - Object.definedProperty 只能检测到属性的获取和设置，对于新增和删除是没办法检测的。在数据初始化时，由于不知道哪些数据会被用到，Vue 是直接递归观测全部数据，这会导致性能多余的消耗。

  - Proxy 劫持整个对象，对象属性的增加和删除都能检测到。Proxy 并不能监听到内部深层的对象变化，因此 Vue3.0 的处理方式是在 getter 中去递归响应式，只有真正访问到的内部对象才会变成响应式，而不是无脑递归，在很大程度上提升了性能。

15. Vue 如何检测数组更新？

  - Vue 内部重写数组原型链，当数组发生变化时，除了执行原生的数组方法外，还会调用 dep.notify 通知 Watcher 更新。触发数组更新的方法共7种
      - push
      - pop
      - shift
      - unshift
      - splice
      - sort
      - reverse

16. Vue 组件中 data 为什么要求是函数

  - Vue 构造实例使用的是同一个构造函数，data 直接使用对象会导致实例的共享引用，即组件间的状态会相互影响。通常发生共享引用，都是组件复用的情况。使用函数返回一个对象，由于是不同引用，自然可以避免这个问题发生。

# vue 路由面试题

1. mvvm 框架是什么？
   mvvm 即 Model-View-ViewModel，mvvm 的设计原理是基于 mvc 的
   mvvm 是 Model-View-ViewModel 的缩写，Model 代表数据模型负责业务逻辑和数据封装，View 代表 UI 组件负责界面和显示，ViewModel 监听模型数据的改变和控制视图行为，处理用户交互，简单来说就是通过双向数据绑定把 View 层和 Model 层连接起来。在 MVVM 架构下，View 和 Model 没有直接联系，而是通过 ViewModel 进行交互，我们只关注业务逻辑，不需要手动操作 DOM，不需要关注 View 和 Model 的同步工作

2. vue-router 是什么?它有哪些组件
   - vue-router 是 Vue.js 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌
   - 组件有：`<router-link>` 和 `<router-view>` 和 `<keep-alive>`
   
3. active-class 是哪个组件的属性？
   active-class 是 router-link 的终端属性，用来做选中样式的切换，当 router-link 标签被点击时将会应用这个样式

4. 怎么定义 vue-router 的动态路由? 怎么获取传过来的值
   - 动态路由的创建，主要是使用 path 属性过程中，使用动态路径参数，以冒号开头，如下：
       ```
        {
            path: '/details/:id',
            name: 'Details',
            components: Details
        }
       ```
   访问 details 目录下的所有文件，最终都会将这些文件映射到 Detail 组件上
   - 当匹配到 details 目录下的路由时，参数值会被设置到 this.$route.params 下，所以通过这个数据可以获取动态参数
     this.$route.params.id
     
5. vue-router 有哪几种导航钩子?
   - 全局前置守位
       ```
      const router = nwe VueRouter({})
       router.beforeEach((to, from, next) => {
          // to: Router，代表要进入的目标，它是一个路由对象
          // from: Router，代表当前正要离开的路由，也是一个路由对象
          // next: Function，必须调用的方法，具体执行效果则依赖 next 方法调用的参数
       
          // next(): 进入管道中的下一个钩子，如果全部的钩子执行完了，则导航的状态就是 confirmed
          // next(false): 终端当前的导航，如果浏览器 url 改变，那么 url 会重置到 from 路由对应的地址
          // next('/') || next({ path: '/' }): 跳转到一个不同的地址，当前导航终端，执行新的导航
          next(); // next 方法必须调用，否则钩子函数就无法 resolved
       })
       ```
   - 全局后置钩子
      ```
        router.afterEach((to, from) => {
          // 后置钩子并没有 next 函数，也不会改变导航本身
        });
      ```
   - 路由独享钩子
      ```
       const router = new VueRouter({
         routes: [
           {
             path: '/home',
             component: Home,
             beforeEnter: (to, from, next) => {
               // 参数与全局前置守位一样
             },
           },
         ],
       });
      ```

   - 组件内导航钩子
      ```
       const Home = {
         template: '<div></div>',
         beforeRouteEnter: (to, from, next) => {
           // 在渲染该组件的对应路由被 confirm 前调用
           // 不能获取组件实例 this，因为当守位执行前，组件实例还没被创建
         },
         beforeRouteUpdate: (to, from, next) => {
           // 在当前路由改变，但是该组件被复用时调用
           // 例如: 对于一个动态参数的路径 /home:id，在 /home/1 和 /home/2 之间跳转的时候
           // 由于会渲染同样的 Home 组件，因此组件实例会被复用，而这个钩子就会在这个情况下被调用
           // 可以访问组件实例 this
         },
         beforeRouteLeave: (to, from, next) => {
           // 导航离开该组件对应的路由时调用
           // 可以访问组件实例 this
         },
       };
       ```

   - beforeRouterEnter 不能访问 this，因为守位在导航确认前被调用，因此新组件还没有被创建，可以通过传一个回调给 next 来访问组件实例。在导航被确认的时候执行回调，并把实例作为回调的方法参数
      ```
       const Home = {
         template: '<div></div>',
         beforeRouterEnter: (to, from, next) => {
           next(
             (vm = {
               // 通过 vm 访问组件实例
             })
           );
         },
       };
      ```

6. route 和 router 的区别
   router 为 VueRouter 的实例，是一个全局路由对象，包含了路由跳转的方法，钩子函数等
   route 是路由信息对象 || 跳转的路由对象，每一个路由都会有一个 route 对象，是一个局部对象，包含 path，params，hash，query，fullPath，matched，name 等路由信息参数

7. vue-router 响应路由参数的变化
   - 用 watch 检测
       // 监听当前路由发送变化的时候执行
       ```
        watch: {
            $route(to, from) {
              console.log(to.path)
              // 对路由变化做出响应
            }
        }
       ```
   - 组件内导航钩子函数
      ```
        beforeRouterUpdate(to, from, next){
            // to do something
        }
      ```

8. vue-router 传参
   - Params
     1. 只能使用 name，不能使用 path
     2. 参数不会显示在路径上
     3. 浏览器强制刷新参数会被清空
        ```
          // 传递参数
          this.$router.push({
            name: Home,
            params: {
              number: 1,
            },
          });
          // 接收参数
          const p = this.$route.params;
        ```
   - Query
     1. 参数会显示在 url 地址栏，刷新不会被清空
     2. name 可以使用 path 路径
        ```
          // 传递参数
          this.$router.push({
            path: Home,
            query: {
              number: 1,
            },
          });
          // 接收参数
          const p = this.$route.query;
        ```
9. vue-router 的两种模式
   - hash
     原理是 onhashchange 事件，可以在 window 对象上监听这个事件
         window.onhashchange = function (e) {
           console.log(e.oldURL, e.newURL);
           let hash = location.hash.slice(1);
         };
   - history
     1. 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法
     2. 需要后台配置支持。如果刷新时，服务器没有响应资源，会抛出 404 的错误

10. vue-router 实现路由懒加载（ 动态加载路由 ）
    把不同路由对应的组件分割成不同的代码块，然后当路由被访问时才加载对应的组件即为路由的懒加载，可以加快项目的加载速度，提高效率
    ```
      const router = new VueRouter({
          routes: [
            {
                path: '/home',
                name: 'Home',
                component: () => import('../views/home')
            }
          ]
      })
    ```
  
11. route 和 router 的区别

  - router 是 VueRouter 的实例，在 script 标签中想要导航到不同的 URL,使用 router.push 方法。返回上一个历史 history 用 $router.to(-1)

  - $route 为 当前 router 跳转对象。里面可以获取当前路由的 name, path, query, params 等。

# Vue 生命周期面试题

1. 什么是 vue 生命周期

   vue 声明周期是指 vue 实例对象从创建、数据初始化、挂载、更新、销毁的过程

2. vue 生命周期的作用是什么

   准确的控制了数据流和其对 DOM 的影响。或者说给了开发者在不同阶段添加代码的机会

3. 第一次页面加载会触发哪几个钩子

   会触发 beforeCreate、created、beforeMount、mounted

4. 简述每个周期具体适合哪些场景

   - beforeCreate：在 new 一个 vue 实例后，只有一些默认的生命周期钩子和默认事件，其它东西都还没创建。在 beforeCreate 生命周期执行的时候，data 和 methods 中的数据都还没初始化，不能在这个阶段使用 data 中的数据和 methods 中的方法

   - created：data 和 methods 都已经初始化好了，如果要调用 methods 中的方法，或者操作 data 中的数据，最早可以在这个阶段操作

   - beforeMount：执行到这个钩子的时候，在内存中已经编译好了模板，但是还没有挂载到页面中，此时，页面还是旧的

   - mounted：执行到这里，表示 vue 实例已经初始化完成了。组件脱离了创建阶段，进入到了运行阶段，如果想要通过插件操作页面上的 DOM 节点，最早可以在这个阶段操作

   - beforeUpdate：当执行这个钩子时，页面中显示的数据是旧的，data 的数据是更新后的，页面还没和最新的数据保持同步

   - updated：页面显示的数据已经和 data 的数据保持同步了，都是最新的

   - beforeDestroy：vue 实例从运行阶段到了销毁阶段，这个时候实例上的 data，methods，指令，过滤器都是出于可用状态，还没有真正被销毁

   - destroyed：这个时候实例上的 data，methods，指令，过滤器都已经出于不可用状态。组件已经被销毁了

5. created 和 mounted 的区别

   - created：在模板渲染完成前调用，即通常初始化某些属性值，然后再渲染成视图

   - mounted：在模板渲染完成后调用，通常是初始化页面完成后，再对 HTML 的 dom 节点进行一些需要的操作

6. vue 获取数据在哪个周期函数

   获取数据一般在 created/beforeMount/mounted 周期函数皆可，如果要操作 DOM，那只能在 mounted

7. 请详细说下你对 vue 生命周期的理解？

   总共分为 8 个阶段。创建前/后，挂载前/后，更新前/后，销毁前/后

   - 创建前/后：在 beforeCreate 阶段，vue 实例的挂载元素(el)和数据对象(data)都为 undefined，还未初始化。在 created 阶段，vue 实例的数据对象(data)有了，el 还没有

   - 挂载前/后：在 beforeMount 阶段，vue 实例的 el 和 data 都已经初始化了，但还是挂载之前为虚拟的 DOM 节点，data.message 还没替换。在 mounted 阶段，vue 实例挂载完成，data.message 完成渲染

   - 更新前/后：当 data 数据变化时，会触发 beforeUpdate 和 updated 方法

   - 销毁前/后：在执行 destroy 方法后，data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 绑定，但是 dom 结构依然存在