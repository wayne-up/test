<template>
  <div id="MyHeader">
      <input 
      class="headerInput"
      type="text" 
      placeholder="请输入你的任务名称，按回车键确认"
      @keyup.enter="add"
      v-model="todoValue"
      >
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
    export default {
        name:'MyHeader',
        // props:['addTodo'],
        data() {
            return {
                todoValue:''
            }
        },
        methods:{
            //添加一个代办事项
            add(e){
                this.$emit('addTodo',{id:nanoid(),value:e.target.value,done:false})
                this.todoValue =''
            }
        }
    }
</script>

<style scoped>
    .headerInput{
        height: 32px;
        width: 578px;
        border: 1px solid rgb(189, 189, 189);
        border-radius: 6px;
        font-size: 14px;
        padding-left: 5px;
    }
    .headerInput:focus{
        outline:  none;
        background: #FFFFFF;
        border:1px solid #2DA7E0;
        box-shadow: inset 0px 0 20px 1000px #FFFFFF !important;
    }

</style>