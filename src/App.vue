<template>
  <div id="app">
    <button @click="toggle = !toggle">Toggle Sandbox</button>
    <Sandbox v-if="toggle" />
  </div>
</template>

<script>
import Sandbox from '@/components/Sandbox'

export default {
  name: 'App',

  components: {
    Sandbox,
  },

  data: () => ({
    toggle: true,
  }),
}
</script>
