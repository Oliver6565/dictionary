<template>
  <div style="background-color: #6B92B0;">
    <router-view></router-view>
    {{ a.split(',').map(v=>{return v+'ii'}) }}
    <p v-text="b"></p>
    <form action="/">
      <button @click.prevent="f1">click</button>
      <div :style="style1">style test</div>
      <div :class="class1">class test</div>
    </form>
  </div>
</template>

<script setup>
const count=0,
a='我是,一个字符串',
b= 199929991299,
f1 =()=>{console.log('???')},
style1={display:'none'},
class1={display:'none'}

</script>

<style lang="less" scoped>

</style>