# Vue 3 + TypeScript + Vite

# 第一章、vue3学习

## 1. 学习资源

1.官方文档：[Vue.js - 渐进式 JavaScript 框架 | Vue.js (vuejs.org)](https://cn.vuejs.org/)

2.学习教程：[Vue3 + vite + Ts + pinia + 实战 + 源码 +electron_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1dS4y1y7vd/)

教程知识点梳理：

* Vue3最新setup语法糖
* Vite构建工具
* Typescript
* Pinia状态管理
* Linux Nginx
* 云计算 K8S docker等
* Nodejs
* NestJs

## 2. vite工具

**Vite**下一代的前端工具链，为开发提供极速响应[Vite | 下一代的前端工具链 (vitejs.dev)](https://cn.vitejs.dev/)

当前版本：v3.2.0

## 3. 新建vite-project
```bash
npm create vite@latest
```

>  vite-project
>
> │  ├─ .vscode
>
> │  │  └─ extensions.json
>
> │  ├─ index.html
>
> │  ├─ package-lock.json
>
> │  ├─ package.json
>
> │  ├─ public
>
> │  │  └─ vite.svg
>
> │  ├─ README.md
>
> │  ├─ src
>
> │  │  ├─ App.vue
>
> │  │  ├─ assets
>
> │  │  │  └─ vue.svg
>
> │  │  ├─ components
>
> │  │  │  └─ HelloWorld.vue
>
> │  │  ├─ main.ts
>
> │  │  ├─ style.css
>
> │  │  └─ vite-env.d.ts
>
> │  ├─ tsconfig.json
>
> │  ├─ tsconfig.node.json
>
> │  └─ vite.config.ts



## 4. tsconfig.json

官方的配置选项：[tsconfig.json · TypeScript中文网 · TypeScript——JavaScript的超集 (tslang.cn)](https://www.tslang.cn/docs/handbook/tsconfig-json.html)

[05_TS编译选项（1）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Xy4y1v7S2?p=6&vd_source=a05ff4befa7970bea9f70ec158705f66)



## 5. 图标样式

```css
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
```





# 第二章： 模板语法与vue指令



## 1.模板语法：

```vue
<script setup lang="ts">
const msg:string = "VUE模板语法初体验"
</script>

<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>

</template>

<style scoped>
</style>
```

## 2.指令

指令由 `v-` 作为前缀，表明它们是一些由 Vue 提供的特殊 attribute，你可能已经猜到了，它们将为渲染的 DOM 应用特殊的响应式行为。

* v-bind
* v-on
* v-if
* v-else-if
* v-else
* v-for
* v-show
* v-model

## 3.修饰符

* stop
* prevent
* number







