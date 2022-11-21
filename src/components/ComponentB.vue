
<script setup lang="ts">
import { reactive, Ref } from "vue";
import { nextTick } from "vue";
import { ref } from 'vue'
// 显式声明
interface Book {
  count: number;
}
// 会隐式推导
let state: Book = reactive({ count: 0 });
state = reactive({ count: 1 });



function increment() {
  state.count++;
  nextTick(() => {
    // 访问更新后的 DOM
    console.log("更新后的dom", state);
  });
}

const obj = reactive({
  nested: { count: 0 },
  arr: ["foo", "bar"],
});

function mutateDeeply() {
  // 以下都会按照期望工作
  obj.nested.count++;
  obj.arr.push("baz");
}

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


const state2 = reactive({ count: 0 })

// n 是一个局部变量，同 state.count
// 失去响应性连接
let n = state2.count
state2.count++
// 不影响原始的 state
n++
console.log(state2,n)

// count 也和 state.count 失去了响应性连接
let { count } = state2
// 不会影响原始的 state
count++
console.log(state2,count)

let state3 = reactive({ count: 0 })

// 上面的引用 ({ count: 0 }) 将不再被追踪（响应性连接已丢失！）
state3 = reactive({ count: 1 })
console.log(state3) //Proxy{count:1}

// 利用ref定义响应式变量


const count2 = ref(0)
console.log(count2.value)

// 响应式是对象：value属性会完整替换内部对象属性 
const objectRef = ref({ count: 0 })

// 这是响应式的替换
objectRef.value = { count: 1 }

const count4 = ref(0)
const state4 = reactive({count4})
console.log(state4.count4)    // 0
state4.count4 = 4
console.log(count4.value) //4


const object4 = {  foo:ref(1)}
const { foo } = object4

let a = ref(3)
a =ref(4)
console.log(a.value,"a") // 4

</script>

<template>
  <div>
    <div @click="increment()">
      {{ state.count }}
    </div>
    <!-- 页面与数据都会发生变化 -->
    <div @click="mutateDeeply">{{ obj.arr }}-{{ obj.nested }}</div>
   <div>{{ foo + 1 }}</div>

  </div>
</template>

<style scoped>
</style>
