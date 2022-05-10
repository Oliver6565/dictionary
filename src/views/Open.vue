<template>
    <div class="open">
        <Search></Search>
        <Content></Content>
    </div>
</template>

<script>
import Search from '../components/search.vue'
import Content from '../components/content.vue'
import { reactive, toRefs } from 'vue'

export default {
    components:{ Search, Content },
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
.open{
    color:#FCDFB3;
    background-color: #6B92B0;
}
</style>