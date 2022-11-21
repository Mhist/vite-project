<script setup lang="ts">
import {ref} from 'vue'
const rawHtml: string =
  "在网站上动态渲染任意 HTML 是非常危险的，因为这非常容易造成 XSS 漏洞。";
const dynamicId: string = "15454545";
const isButtonDisabled: boolean = true;
const objectOfAttrs = {
  id: "container",
  class: "wrapper",
};

// const number: number = 1;
const number = ref(0)
const message: string = "message";
const ok: boolean = true;
const id: string = "202211031917";
const seen:boolean = true
const url:string = "www.baidu.com"
const attributeName:string = "href"
const foo:string = 'foo'
const someAttr:string = 'someAttr'
const onSubmit = ref()
onSubmit.value = function (event:string):void {
  console.log(event,"打印修饰符反馈！")
}

const parentClick = ():void=>{
  console.log("父元素被点击")
}

const childClick:any = ():void=>{
  console.log("子元素被点击")
}
type Cls = {
  a:boolean,
  b:boolean
}

const cls:Cls = {
    a:true,
    b:false
}
</script>

<template>
  <div>
    <!-- v-html -->
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
    <!-- v-bind 动态绑定 及简写方式-->
    <div v-bind:id="dynamicId">v-bind看动态id</div>
    <div :id="dynamicId">:省略形式看动态id</div>
    <!-- 绑定布尔值 -->
    <button :disabled="isButtonDisabled">绑定布尔值Button</button>
    <!-- 绑定多个参数 -->
    <div v-bind="objectOfAttrs"></div>
    <div>
        表达式:</div>
        1.加法
      {{ number + 1 }}<br/>
        2.三元表达式
      {{ ok ? "YES" : "NO" }}<br/>
        3.基础API
      {{ message.split("").reverse().join("") }}<br/>
        4.属性变量
      <div :id="`list-${id}`"></div><br/>
    <!-- v-if -->
    <p v-if="seen">v-if :Now you see me</p>
    <a v-bind:href="url"> ... </a>

    <!-- 简写 -->
    <a :href="url"> ... </a>
    <button v-on:click="number++"> {{number}}  </button>
    <!-- 自加的需要变量是响应式的 -->
    <!-- 简写 -->
    <button @click="number++"> {{number}} </button>
          <!--
    注意，参数表达式有一些约束，
    参见下面“动态参数值的限制”与“动态参数语法的限制”章节的解释
    -->
    <!-- 动态参数中表达式的值应当是一个字符串，或者是 null。特殊值 null 意为显式移除该绑定。其他非字符串的值会触发警告。 -->
        <a v-bind:[attributeName]="url"> 百度一下 </a>

        <!-- 简写 -->
        <a :[attributeName]="url"> 百度一下 </a>
        <!-- 警告 -->
        <!-- 这会触发一个编译器警告 -->
        <a :[message]="url"> ... </a>
        <!-- 这里的字符串someAttr中大写会被浏览器强制改为小写 -->
        <!-- 上面的例子将会在 DOM 内嵌模板中被转换为 :[someattr]。如果你的组件拥有 “someAttr” 属性而非 “someattr”，这段代码将不会工作。单文件组件内的模板不受此限制，这里是单文件模板内部、所以会被渲染、且单词被浏览器改为小写形式 -->
        <a :[someAttr]="url"> ... </a>  

        <!-- 修饰符 -->
        <!-- 不加修饰符的时候会一直刷新 -->
        <form @click.prevent="onSubmit"><button type="submit">prevent修饰符</button></form>

        <p>修饰符是以点开头的特殊后缀，表明指令需要以一些特殊的方式被绑定。例如 .prevent 修饰符会告知 v-on 指令对触发的事件调用 event.preventDefault()：</p>

        <!-- 如果不阻止冒泡事件的话、会依次输出：子元素被点击 父元素被点击 -->
        <div @click="parentClick">
          父元素点击
            <div @click.stop="childClick">子元素点击</div>
        </div>

        <div :class="['a','b']">测试样式-数组形式</div>
        <!-- 布尔值为false则不执行挂载对应的类名 -->
        <div :class="[cls]">测试样式-数组形式</div>



    
  </div>
</template>

<style scoped>
.a{
  font-size:20;
  color:rgb(0, 208, 255);
}
.b{
  border: 1px solid red;
}
.b:hover{

filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
