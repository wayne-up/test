
<template>
  <div id="MyFooter" v-show="todoTotal">
      <input type="checkbox" v-model="isAll" >
      <span>已完成{{doneTotal}} / 全部{{todoTotal}}</span>
      <button @click="clearDone">清除已完成任务</button>
  </div>
</template>

<script>
    export default {
        name:'MyFooter',
        props:['todolist'],
        // props:['todolist','checkAll','clearDoneApp'],
        computed:{
            //所有代办数量
            todoTotal(){
                return this.todolist.length
            },
            //已完成的数量
            doneTotal(){
                return this.todolist.reduce((pre,cur)=>{
                    return pre + (cur.done? 1:0)
                },0)
            },
            //全选按钮的状态（是否勾选
            isAll:{
                get(){
                    return this.todoTotal == this.doneTotal
                },
                set(val){
                    this.$emit('checkAll',val)
                }
            }

        },
        methods:{
            //清楚所有已完成
            clearDone(){
                this.$emit('clearDoneApp')
            }
        }
    }
</script>

<style scoped>
    #MyFooter{
        line-height: 42px;
        width: 576px;
        position: relative;
        padding: 3px 8px;
    }
    span{
        margin-left: 10px;
    }
    button{
        line-height: 23px;
        position: absolute;
        margin-top: 4px;
        right: 8px;
    }
</style>