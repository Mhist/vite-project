

<template>
  <div >
    <ComponentA v-if="false"  />
    <ComponentB v-if="false"  />
    <ComponentC v-if="false"  />
    <ComponentD v-if="false"  />
    <ComponentE v-if="false"  />
    <ComponentF v-if="false"  />
    <ComponentG v-if="false"  />
    <ComponentH v-if="false"  />
    <ComponentI v-if="false"  />
    <ComponentJ v-if="false"  />
    <ComponentK v-if="false"  />
    <ComponentL v-if="true"  />
 

  </div>
</template>

<script  lang="ts" setup>
import { reactive, ref,shallowRef,markRaw } from 'vue'
import ComponentA from '../src/components/ComponentA.vue'
import ComponentB from '../src/components/ComponentB.vue'
import ComponentC from '../src/components/ComponentC.vue'
import ComponentD from '../src/components/ComponentD.vue'
import ComponentE from '../src/components/ComponentE.vue'
import ComponentF from '../src/components/ComponentF.vue'
import ComponentG from '../src/components/ComponentG.vue'
import ComponentH from '../src/components/ComponentH.vue'
import ComponentI from '../src/components/ComponentI.vue'
import ComponentJ from '../src/components/ComponentJ.vue'
import ComponentK from '../src/components/ComponentK.vue'
import ComponentL from '../src/components/ComponentL.vue'

</script>
<style scoped>

</style>
