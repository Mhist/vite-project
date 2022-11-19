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

[模板语法及指令练习：componentA](https://github.com/Mhist/vite-project/blob/master/src/components/ComponentA.vue)

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

# 第三章：响应式基础
[响应式基础：componentB](https://github.com/Mhist/vite-project/blob/master/src/components/ComponentB.vue)

* 定义响应式对象：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy

* 响应式系统原理： https://cn.vuejs.org/guide/extras/reactivity-in-depth.html

* 为响应式对象标注类型（ts结合）： https://cn.vuejs.org/guide/typescript/composition-api.html

```vue
import { reactive } from 'vue'

export default {
  // `setup` 是一个专门用于组合式 API 的特殊钩子函数
  setup() {
    const state = reactive({ count: 0 })

    // 暴露 state 到模板
    return {
      state
    }
  }
}

```

使用这种方式需要定义并通过return返回。

不过一般可以采用以下这种形式、简化操作。注意一个单文件组件最多只允许有一个带setup的script

```vue
<script setup lang="ts">

</script>
```



## 1.DOM 更新时机

```vue
import { nextTick } from 'vue'

function increment() {
  state.count++
  nextTick(() => {
    // 访问更新后的 DOM
  })
}

```

## 2.深度响应性

### （1）、默认深层响应

在vue中默认都是深层响应式的，定义的一个对象内部的属性变化的时候，是能被检测到的。

```vue
import { reactive } from 'vue'

const obj = reactive({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})

function mutateDeeply() {
  // 以下都会按照期望工作
  obj.nested.count++
  obj.arr.push('baz')
}

```

### （2）慎用浅层响应

浅层响应式对象、只是根部的属性才会具有响应式。[响应式 API：进阶 | Vue.js (vuejs.org)](https://cn.vuejs.org/api/reactivity-advanced.html#effectscope)官方建议少用。后续进阶部分可以研究。



## 3.响应式代理 vs. 原始对象

```ts
// 响应式代理与原有对象
const raw = {};
const proxy = reactive(raw);

// 代理对象和原始对象不是全等的
console.log(proxy === raw); // false
```

只有代理对象是响应式的，更改原始对象不会触发更新。因此，使用 Vue 的响应式系统的最佳实践是 **仅使用你声明对象的代理版本**。

为保证访问代理的一致性，对同一个原始对象调用 `reactive()` 会总是返回同样的代理对象，而对一个已存在的代理对象调用 `reactive()` 会返回其本身：

```tsx
// 响应式代理与原有对象
const raw = {};
const proxy = reactive(raw);

// 代理对象和原始对象不是全等的
console.log(proxy === raw); // false
// 在同一个对象上调用 reactive() 会返回相同的代理
console.log(reactive(raw) === proxy) // true

// 在一个代理上调用 reactive() 会返回它自己
console.log(reactive(proxy) === proxy) // true
console.log(reactive(reactive(proxy)) === proxy)//true
```

即对同一个对象通过reactive()进行嵌套响应式处理、返回的是同一个响应式对象。



## 4.局限性

1. 仅对对象类型有效（对象、数组和 `Map`、`Set` 这样的[集合类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects#使用键的集合对象)），而对 `string`、`number` 和 `boolean` 这样的 [原始类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive) 无效。

2. 因为 Vue 的响应式系统是通过属性访问进行追踪的，因此我们必须始终保持对该响应式对象的相同引用。这意味着我们不可以随意地“替换”一个响应式对象，因为这将导致对初始引用的响应性连接丢失：

   ```tsx
   let state3 = reactive({ count: 0 })
   
   // 上面的引用 ({ count: 0 }) 将不再被追踪（响应性连接已丢失！）
   state3 = reactive({ count: 1 })
   
   console.log(state3) //输出： Proxy{count:1}
   
   ```

同时这也意味着当我们将响应式对象的   **属性**    赋值或   **解构**     至本地变量时，或是将该属性传入一个函数时，我们会失去响应性：

```tsx
const state2 = reactive({ count: 0 })

// n 是一个局部变量，同 state.count
// 失去响应性连接
let n = state2.count
// 不影响原始的 state
n++
console.log(state2,n)

// count 也和 state.count 失去了响应性连接
let { count } = state2
// 不会影响原始的 state
count++
console.log(state2,count)

输出：
Proxy {count: 0}[[Handler]]: Object[[Target]]: Object[[IsRevoked]]: false 1
ComponentB.vue:65 Proxy {count: 0}[[Handler]]: Object[[Target]]: Object[[IsRevoked]]: false 1

```

## 5.ref()定义响应式变量

```tsx
import { ref } from 'vue'

const count = ref(0)
console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

简言之，`ref()` 让我们能创造一种对任意值的 “引用”，并能够在不丢失响应性的前提下传递这些引用。这个功能很重要，因为它经常用于将逻辑提取到 [组合函数](https://cn.vuejs.org/guide/reusability/composables.html) 中。

```tsx
const obj = {
  foo: ref(1),
  bar: ref(2)
}

// 该函数接收一个 ref
// 需要通过 .value 取值
// 但它会保持响应性
// ref 被传递给函数或是从一般对象上被解构时，不会丢失响应性：
callSomeFunction(obj.foo)

// 仍然是响应式的
const { foo, bar } = obj

```

## 6.自动解包

* ref 在模板中的解包，在template中即不需要通过.value获取。请注意，仅当 ref 是模板渲染上下文的顶层属性时才适用自动“解包”。

```
const object = { foo: ref(1) }        //顶层  第一层
```

```tsx
{{ object.foo + 1 }}                  // 非顶层 第二层
```

正确写法：

```vue
const object4 = {  foo:ref(1)}
const { foo } = object4

<template>
   <div>{{ foo + 1 }}</div>   显示：2
</template>

```



* 如果将一个新的 ref 赋值给一个关联了已有 ref 的属性，那么它会替换掉旧的 ref：

```
let a = ref(3)
a =ref(4)
console.log(a.value,"a") // 4
```

只有当嵌套在一个深层响应式对象内时，才会发生 ref 解包。当其作为[浅层响应式对象](https://cn.vuejs.org/api/reactivity-advanced.html#shallowreactive)的属性被访问时不会解包。

**数组和集合类型的 ref 解包[#](https://cn.vuejs.org/guide/essentials/reactivity-fundamentals.html#ref-unwrapping-in-arrays-and-collections)**

跟响应式对象不同，当 ref 作为响应式数组或像 `Map` 这种原生集合类型的元素被访问时，不会进行解包。

```tsx
const books = reactive([ref('Vue 3 Guide')])
// 这里需要 .value
console.log(books[0].value)

const map = reactive(new Map([['count', ref(0)]]))
// 这里需要 .value
console.log(map.get('count').value)

```



解包响应式语法糖：通过配置进行**显式启用**

[响应性语法糖 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/extras/reactivity-transform.html#explicit-opt-in)

[用了这招，写vue3太舒服了_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1NS4y1q7xp/?spm_id_from=333.999.list.card_archive.click&vd_source=a05ff4befa7970bea9f70ec158705f66)



# 第四章、计算属性

[计算属性-componentC](https://github.com/Mhist/vite-project/blob/master/src/components/ComponentC.vue)

## 1.缓存

1.`computed()` 方法期望接收一个 getter 函数，返回值为一个**计算属性 ref**。和其他一般的 ref 类似，你可以通过 `publishedBooksMessage.value` 访问计算结果。计算属性 ref 也会在模板中自动解包，因此在模板表达式中引用时无需添加 `.value`。

```vue
<script lang="ts">
import { reactive } from '@vue/reactivity'
import { computed } from '@vue/runtime-core'
export default {
	name: 'ComponentC',
}
</script>
<script setup lang="ts">
const author = reactive({
  name:"作者计算属性",
  books:[
    'vue2-Advanced Guide',
    'vue3-Basic Guide',
    'Vue4-The Mystery'
  ]
})
// 组件中
function calculateBooksMessage() {
  return author.books.length > 0 ? 'Yes' : 'No'
}
const publishedBooksMessage = computed<string>(calculateBooksMessage)


</script>

<template>
  <div>
  <p>Has published books</p>
  <span>{{author.books.length > 0 ?'Yes':'No'}}</span><br/>
  <span>{{publishedBooksMessage}}</span>
    
  </div>
</template>

<style scoped>

</style>

```

若我们将同样的函数定义为一个方法而不是计算属性，两种方式在结果上确实是完全相同的，然而，不同之处在于**计算属性值会基于其响应式依赖被缓存**。一个计算属性仅会在其响应式依赖更新时才重新计算。这意味着只要 `author.books` 不改变，无论多少次访问 `publishedBooksMessage` 都会立即返回先前的计算结果，而不用重复执行 getter 函数。

计算属性有更新的和不更新的、更新的是因为它有响应式依赖、而像

```tsx
const now = computed(() => Date.now())
```

不依赖其他响应式选项、所以不会更新。



## 2.可写的计算属性

计算属性默认是只读的。当你尝试修改一个计算属性时，你会收到一个运行时警告。只在某些特殊场景中你可能才需要用到“可写”的属性，你可以通过同时提供 getter 和 setter 来创建：

```vue
<script lang="ts">
import { reactive,ref } from '@vue/reactivity'
import { computed } from '@vue/runtime-core'
export default {
	name: 'ComponentC',
}
</script>
<script setup lang="ts">
const author = reactive({
  name:"作者计算属性",
  books:[
    'vue2-Advanced Guide',
    'vue3-Basic Guide',
    'Vue4-The Mystery'
  ]
})
// 组件中
function calculateBooksMessage() {
  return author.books.length > 0 ? 'Yes' : 'No'
}
const publishedBooksMessage = computed<string>(calculateBooksMessage)
const now = computed(() => Date.now())


// 可写的计算属性
const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue:string) {
    // 注意：我们这里使用的是解构赋值语法
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
fullName.value = '江 武汉'
let a:Array<string> = fullName.value.split(' ')
console.log(a)
console.log(firstName.value,lastName.value)

</script>

<template>
  <div>
  <p>Has published books</p>
  <span>{{author.books.length > 0 ?'Yes':'No'}}</span><br/>
  <span>{{publishedBooksMessage}}</span><br/>
  <span>{{now}}</span>
    
  </div>
</template>

<style scoped>

</style>

```



### Getter 不应有副作用[#](https://cn.vuejs.org/guide/essentials/computed.html#getters-should-be-side-effect-free)

计算属性的 getter 应只做计算而没有任何其他的副作用，这一点非常重要，请务必牢记。举例来说，**不要在 getter 中做异步请求或者更改 DOM**！一个计算属性的声明中描述的是如何根据其他值派生一个值。因此 getter 的职责应该仅为计算和返回该值。在之后的指引中我们会讨论如何使用[监听器](https://cn.vuejs.org/guide/essentials/watchers.html)根据其他响应式状态的变更来创建副作用。

### 避免直接修改计算属性值[#](https://cn.vuejs.org/guide/essentials/computed.html#avoid-mutating-computed-value)

从计算属性返回的值是派生状态。可以把它看作是一个“临时快照”，每当源状态发生变化时，就会创建一个新的快照。更改快照是没有意义的，因此计算属性的返回值应该被视为只读的，并且永远不应该被更改——应该更新它所依赖的源状态以触发新的计算。



# 第五章、类与样式绑定

[类与样式绑定-componentD](https://github.com/Mhist/vite-project/blob/master/src/components/ComponentD.vue)

