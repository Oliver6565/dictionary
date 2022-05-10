<template>
    <div class="container">
        Start to type. to draw A dream ...
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
.container{
    border: 10px solid #94C9F2;
    border-radius: 10px;
    padding: 10px;
}
</style>