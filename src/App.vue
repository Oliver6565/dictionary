<template>
  <div style="background-color: #6B92B0;">
    <router-view></router-view>
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'

export default {
  setup () {
    const state = reactive({
      count: 0,
    })
  
    return {
      ...toRefs(state),
    }
  }
}
</script>

<style lang="less" scoped>

</style>