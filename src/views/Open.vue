<template>
    <div class="open">
        <Search @sendMsg="handle"></Search>
        <Content :Msg="Msg"></Content>
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
            Msg:''
        })
        
        const handle=(value)=>{
            state.Msg = value
        }

        return {
            ...toRefs(state),
            handle,
        }
    }
}
</script>

<style lang="less" scoped>
.open{
    
}
</style>