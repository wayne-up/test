// item组件，展示每一条代办
<template>
  <div class="Item">
      <label>
          <input type="checkbox" 
            @change="changeTodo(todo.id)"
            :checked="todo.done"
         >
      <span>{{todo.value}}</span>
      </label>
      <button @click="deleteTodo(todo.id)">删除</button>
  </div>
</template>

<script>
import pubsub from 'pubsub-js'

    export default {
        name:'Item',
        props:['todo'],
        methods: {
            // 将选中的代办设为已完成
            changeTodo(id){
                //
                this.$bus.$emit('checkTodo',id)
            },
            // 删除选中的代办
            deleteTodo(id){
                //
                // this.$bus.$emit('deleteTodoApp',id)
                pubsub.publish('deleteTodoApp',id)

            }
        },
    }
</script>

<style scoped>
    .Item{
        line-height: 32px;
        width: 576px;
        border-bottom: 1px solid rgb(189, 189, 189);
        font-size: 14px;
        padding-left: 6px;
        position: relative;
    }
    .Item:hover{
        background-color: rgb(192, 192, 192);
    }
    
    button{
        position: absolute;
        top: 3px;
        right: 6px;
        display: none;
    }
    .Item:hover button{
        display: block;
    }
    span{
        margin-left: 2px;
    }
</style>