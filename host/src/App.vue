<template>
  <div>
    <label>Show UI <input type="checkbox" v-model="showUI" /></label>
    <div v-if="showUI">
      <HelloWorld msg="message" @click="testme" />
    </div>
  </div>
</template>

<script>
import { defineAsyncComponent } from 'vue'
import Loading from './components/Loading.vue'
import Error from './components/Error.vue'

function defineFederatedComponent(loader) {
  return defineAsyncComponent({
    loader,
    loadingComponent: Loading,
    errorComponent: Error,
    timeout: 1000,
  })
}

export default {
  name: 'App',
  components: {
    HelloWorld: defineFederatedComponent(() => import('library1/HelloWorld')),
    // HelloWorld: defineAsyncComponent({
    //   loader: () => import('library1/HelloWorld'),
    //   loadingComponent: Loading,
    //   errorComponent: Error,
    //   timeout: 1000,
    // })
  },
  data() {
    return {
      message: 'Vue.js application',
      showUI: false,
    }
  },
  methods: {
    async testme() {
      console.log('Testme!')

      function *mygen() {
        for (let i = 0; i < 10; i++) {
          yield i
        }
      }

      const sleep = ms => new Promise(resolve => setTimeout(resolve, ms))

      for (const index of mygen()) {
        await sleep(200)
        console.log('index:', index)
      }
    }
  },
}
</script>

<style>
.h1 {
  color: red;
}
</style>
