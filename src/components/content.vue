<template>
    <div class="container">
        <div v-if="Msg==''">Start to type. to draw A dream ...</div>
        <div v-else>
            <span>{{tip}}</span>
            <div v-for="(item,index) in wordlist" :key="index">
                <p> 
                    <span>{{item.word}}</span>--
                    <span>{{item.phonetic}}</span>--
                    <audio controls>
                            <source :src="item.phonetics[0].audio">
                        </audio>
                    <!-- <span v-for="item2 in item.phonetics ">---{{item2.text}}
                    <audio controls>
                            <source :src="item2.audio">
                        </audio>
                    </span> -->
                    <span></span>
                </p>
                <div class="meaning">
                    
                    {{item.meanings}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, toRefs,watch,watchEffect } from 'vue'
import axios from 'axios'
export default {
    props:{
        Msg:String
    },
    setup (props) {
        const state = reactive({
            tip:'',
            wordlist:[]
        })
        const getData = async (url)=>{
            try{
                const {data:res} = await axios.get(url);
                console.log(res)    // 返回的是一个数组
                state.tip='搜索结果如下'
                state.wordlist = res

            }catch(err){
                state.tip = '搜索不到该单词'
                return
            }
        }
        watchEffect(()=>{
           if(props.Msg=='') return
           const url = 'https://api.dictionaryapi.dev/api/v2/entries/en/'+props.Msg
           getData(url)
        })
     
        return {
            ...toRefs(state),
        }
    }
}
</script>

<style lang="less" scoped>
.container{
    color:#FCDFB3;
    border: 10px solid #94C9F2;
    border-radius: 10px;
    padding: 20px;
}
</style>