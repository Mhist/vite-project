

<template>
  <div>
    <ComponentA v-if="false"  />
    <ComponentB v-if="false"  />
    <ComponentC v-if="false"  />
    <ComponentD v-if="true"  />
    
  </div>
</template>

<script  lang="ts" setup>
import ComponentA from '../src/components/ComponentA.vue'
import ComponentB from '../src/components/ComponentB.vue'
import ComponentC from '../src/components/ComponentC.vue'
import ComponentD from '../src/components/ComponentD.vue'


</script>
<style scoped>
</style>
