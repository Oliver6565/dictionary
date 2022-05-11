<template>
    <div class="container">
        <div v-if="Msg==''">Start to type. to draw A dream ...</div>
        <div v-else>
            <span>{{tip}}</span>
            <div class="definition" v-for="(item,index) in wordlist" :key="index">
                <div class="top">
                    <!-- 音标 -->
                    <div class="phonetic" @click="handleplay(index)">{{item.phonetic}}</div>
                    <!--喇叭图片-->
                    <div>
                        <img  @click="handleplay(index)" src="../assets/喇叭.svg"/>
                    </div>
                    <audio :src="item.phonetics[0].audio" ref="audioRef"></audio>
                </div>
                <div class="meaning" v-for="(item2,index) in item.meanings" :key="index">
                    <!-- 词性 +-->
                    <div class="partOfSpeech">{{item2.partOfSpeech}}</div>
                    <div class="wordMeaning">
                        {{item2.definitions.map(item=>item.definition).join(' ')}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import {ref, reactive, toRefs,watch,watchEffect } from 'vue'
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
                // console.log(res)    // 返回的是一个数组
                state.tip='搜索结果如下:'
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
     
        const audioRef = ref();
        const handleplay = (index) =>{
            audioRef.value[index].play()
            // audio.value[index].play()
        }

        // function handleplay(){
        //     console.log(audioRef)
        // }

        return {
            ...toRefs(state),
            handleplay,
            audioRef
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
    margin-bottom: 20px;
}
.definition{
    padding: 20px 0 10px;
    border-bottom: 2px solid #94C9F2;
    .top{
        display: flex;
        div:first-child{
            margin-right: 10px;
        }
        img{
            width: 25px;
        }
    }
    .meaning{
        display: flex;
        margin:10px 0;
        .partOfSpeech{
            height: 20px;
            font-size: 12px;
            border-radius: 5px;
            margin-right: 10px;
            padding: 0 5px;
            color: #fff;
            background-color: #587baf;
        }
    }

}
</style>