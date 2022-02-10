---
id: a9rQgXJP0U6OEz7FYcPVy
title: Vue2 Vs Vue3
desc: ''
updated: 1644507545012
created: 1644504271182
---

## vue2 常见的缺陷

1. 从开发维护的角度：Vue2 是使用 Flow.js 来做类型校验。但是 Flow.js 已经停止维护，整个社区都在转向typescript。  
2. 从社区二次开发的角度： Vue2 内部运行时，是直接执行浏览器 API。但是这样就会在 Vue2 的跨端方案中带来问题，要么直接在 Vue 源码中进行维护，比如 Weex；要么复制一份 Vue 的代码，把浏览器 API 换成客户端或者小程序的，比如 mpvue，缺点是很难随 Vue 一起更新版本。  
3. 从普通开发者的角度：Vue2 响应式并不是真正意义上的代理，而是基于 `Object.defineProperty()` 实现的。并且，Option API 在组织代码较多的组件的时候不容易维护。

## Vue3 新特性

1. 响应式系统： proxy 代理。Vue2 的 defineProperty 无法对不存在的属性进行拦截，所以 Vue2 中的所有数据必须要在 data 里声明。而 proxy 拦截 obj 这个数据，但 obj 具体是什么属性，proxy 都会拦截，另外 proxy 还可以监听更多的数据格式， 比如 Set、Map。这一特性导致 Vue3 不兼容 IE11 以下的浏览器。  
2. 自定义渲染器：Vue2 内部所有的模块都是揉在一起的，这样做会导致不好扩展的问题。Vue3 利用 monorepo 管理方式，响应式、编译和运行时全部独立出来了，如图所示：

![自定义渲染器](/assets/images/2022-02-10-23-12-22.png)

这样带来的好处是，可以在 Node.js 和 React 中使用响应式。渲染的逻辑也拆成了平台无关渲染逻辑和浏览器渲染 API 两部分。在开发其他平台，例如小程序、小游戏、客户端的时候，就不用全部 fork Vue 的代码，只需要实现平台的渲染逻辑就可以了。  
3. 全部模块使用 TypeScript 重构：类型系统带来了更方便的 提示，并且让我们的代码能够更健壮。
4. Composition API:
    首先说 Option API 几个严重的问题： 所有的数据都挂载在 this 之上，对 TypeScript 的类型推导很不友好，并且这样也不好做 tree-shaking 清理代码；代码不好复用，Vue2 的组件很难抽离通用逻辑，只能使用 mixin，还会带来命名冲突的问题。
    Composition API 的好处：所有的 API 都是 import 进来的，对 tree-shaking很友好，没使用的功能，在打包的时候会被清理掉，减小包的体积；代码方便复用，可以把一个功能的所有 methods、data 封装在一个独立的函数里，复用代码非常容易。
