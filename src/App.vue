

<template>
  <div>
    <ComponentA v-if="true"  />
    <ComponentB v-if="true"  />
    
  </div>
</template>

<script  lang="ts">
import ComponentA from '../src/components/ComponentA.vue'
import ComponentB from '../src/components/ComponentB.vue'

export default {
  name: 'App',
  components: {
    ComponentA,
    ComponentB,
  }
}

</script>
<style scoped>
</style>
