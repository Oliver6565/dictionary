<template>
    <div class="h3" v-if="!wordValue==''"><h3>{{wordValue}}</h3></div>
    <div class="search_box">
      <div class="group">      
        <input type="text" required v-model="wordValue"
        @keydown.enter="sendmsg">
        <span class="bar"></span>
        <label>type A word</label>
      </div>
    </div>
</template>

<script>
import { reactive, toRefs,defineEmits } from 'vue'
export default {
    emits:['sendMsg'],
    setup (props,{emit}) {
        const state = reactive({
            wordValue :''
          
        })
        const sendmsg = ()=>{
          emit("sendMsg",state.wordValue)
        }
        return {
            ...toRefs(state),
            sendmsg
        }
    }
}
</script>

<style lang="less" scoped>
.h3{
  color: #fff;
  opacity: 0.9;
  text-align: center;
  padding-top: 20px ;
}

.search_box{
    padding: 40px 0 40px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}
/* form starting stylings ------------------------------- */
.group{ 
  position:relative; 
}
input{
  color: white;
  opacity: 0.9;
  background: transparent;
  font-size:18px;
  padding:10px 10px 10px 5px;
  display:block;
  width:300px;
  border:none;
  border-bottom:2px solid #94C9F2;
}
input:focus{ outline:none; }

/* LABEL ======================================= */
label{
  color:#ccc; 
  font-size:18px;
  font-weight:normal;
  position:absolute;
  pointer-events:none;
  left:5px;
  top:10px;
  transition:0.2s ease all; 
  -moz-transition:0.2s ease all; 
  -webkit-transition:0.2s ease all;
}

/* active state */
input:focus ~ label, input:valid ~ label{
  top:-20px;
  font-size:14px;
  color:#5264AE;
}

/* BOTTOM BARS ================================= */
.bar{ position:relative; display:block; width:300px; }
.bar:before, .bar:after{
  content:'';
  height:2px; 
  width:0;
  bottom:0px; 
  position:absolute;
  background:#5264AE; 
  transition:0.2s ease all; 
  -moz-transition:0.2s ease all; 
  -webkit-transition:0.2s ease all;
}
.bar:before {
  left:50%;
}
.bar:after {
  right:50%; 
}

/* active state */
input:focus ~ .bar:before, input:focus ~ .bar:after {
  width:50%;
}
</style>