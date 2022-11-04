

<template>
  <div>
    <ComponentA v-if="false"  />
    <ComponentB v-if="false"  />
    <ComponentC v-if="true"  />
    
  </div>
</template>

<script  lang="ts">
import ComponentA from '../src/components/ComponentA.vue'
import ComponentB from '../src/components/ComponentB.vue'
import ComponentC from '../src/components/ComponentC.vue'

export default {
  name: 'App',
  components: {
    ComponentA,
    ComponentB,
    ComponentC,
  }
}

</script>
<style scoped>
</style>
