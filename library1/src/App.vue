<template>
  <HelloWorld msg="Hello!" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      message: 'Vue.js application',
    }
  },
}
</script>

<style>
.h1 {
  color: red;
}
</style>
