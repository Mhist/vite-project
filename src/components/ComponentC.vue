<script setup lang="ts">
import { reactive,ref } from '@vue/reactivity'
import { computed } from '@vue/runtime-core'
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
