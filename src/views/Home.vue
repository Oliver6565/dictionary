<template>
  <div>
    <div class="nav_open"><router-link to="/open">open</router-link></div>
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
.nav_open {
  text-align: center;
  font-size: 50px;
  a{
    color:#ccc;
    text-decoration: none;
  }
  a:hover{
    color:#FCDFB3;
  }
}
</style>