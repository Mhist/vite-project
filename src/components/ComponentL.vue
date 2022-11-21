// <script setup lang="ts">
// import { reactive, ref,shallowRef,markRaw } from 'vue'
// // 如果是组件注册的方式、只需要用字符串形式即可、不需要markRaw形式
// import Avue from '../example/A.vue'
// import Bvue from '../example/B.vue'
// import Cvue from '../example/C.vue'
// const data = reactive([
//   {
//     name:"组件A",
//     component:markRaw(Avue),
//   },
//   {
//     name:"组件B",
//     component:markRaw(Bvue),
//   },
//   {
//     name:"组件C",
//     component:markRaw(Cvue),
//   }
// ])

// const comId = shallowRef(Avue)



// const active = ref(0)

// const switchCom = (item:any,index:number) => {
//   active.value = index
//   comId.value = item.component
// }
// </script>


<script lang="ts">
import { reactive, ref,shallowRef } from 'vue'
import Avue from '../example/A.vue'
import Bvue from '../example/B.vue'
import Cvue from '../example/C.vue'
export default {
    components:{
        Avue,
        Bvue,
        Cvue

    }
}
const data = reactive([
  {
    name:"组件A",
    component:'Avue',
  },
  {
    name:"组件B",
    component:'Bvue',
  },
  {
    name:"组件C",
    component:'Cvue',
  }
])

const comId = shallowRef(Avue)

const active = ref(0)

const switchCom = (item:any,index:number) => {
  active.value = index
  comId.value = item.component
}

</script>

<template>
  <div>
  第十三章、组件基础
       <!-- 动态组件部分 -->
       <div class="box" >
      <div v-for="(item,index) in data">
      <div @click="switchCom(item,index)"  class="btn" :class="active===index?'active':''">{{item.name}}</div>
    </div>
    </div>
    <component :is="comId"></component>
  </div>
</template>

<style scoped>
.box{
  display: flex;
}
.btn {
  width: 100px;
  height: 20px;
  margin: 10px;
  padding: 5px 5px;
  border: 1px solid #ccc;
}

.active{
  background-color: salmon;
}
</style>