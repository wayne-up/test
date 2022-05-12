<template>
  <div id="app">
    <MyHeader @addTodo="addTodo"/>
    <List 
    :todolist="todolist"
    
    />
    <MyFooter :todolist='todolist'
    @checkAll='checkAll'
    @clearDoneApp='clearDoneApp'/>
  </div>
</template>

<script>
import 'animate.css'
import pubsub from 'pubsub-js'
import MyHeader from './components/MyHeader.vue'
import List from './components/List.vue'
import MyFooter from './components/MyFooter.vue'
export default {
  name: 'App',
  components: {
    MyHeader,List,MyFooter
  },
  data() {
            return {
                //待办事项数组（存入localstorage）
                todolist:JSON.parse(localStorage.getItem('todo')) ||[],
            }
        },
  methods:{
    //添加一个todo
    addTodo(todo){
      this.todolist.unshift(todo)
    },
    //修改done状态
    checkTodo(id){
      this.todolist.forEach(todo =>{
        if(todo.id == id )
          {todo.done = !todo.done
          console.log(todo.value)
          }
      })
    },
    //删除一个todo
    deleteTodoApp(_,id){
      // console.log('订阅成功',id)

      this.todolist= this.todolist.filter(todo=>todo.id!=id)
    },
    //全选或全部选
    checkAll(val){
      this.todolist.forEach(todo =>{
        todo.done=val
      })
    },
    //清除所有已完成
    clearDoneApp(){
      this.todolist= this.todolist.filter(todo=>!todo.done)
    }
  },
  watch:{
    todolist:{
      //将todolist的每一次改变都存入localStorage
      deep:true,
      handler(val){
        localStorage.setItem('todo',JSON.stringify(val))
      }
    }
  },
  mounted(){
    //全局事件总线
    this.$bus.$on('checkTodo',this.checkTodo)
    //利用订阅与发布
    pubsub.subscribe('deleteTodoApp',this.deleteTodoApp)
    // this.$bus.$on('deleteTodoApp',this.deleteTodoApp)
  },
  beforeDestroy(){
    this.$bus.$off(['checkTodo','deleteTodoApp'])
  }
}
</script>
<style>
  *{
    padding: 0;
    margin: 0;
  }
  #app{
    width: 580px;
    border: 1px rgb(222, 222, 222) solid;
    border-radius: 5px;
    margin:5px auto;
    padding: 10px;
  }
  button{
    background-color: #bd362f;
    border-radius: 5px;
    color: rgb(251, 251, 251);
    padding: 3px 8px;
    font-size: 14px;
    border: none;
  }
  button:hover{
    background-color: #902923;
    cursor: pointer;
  }
  span{
    font-size: 11px;
  }
  h1{
    height: 50px;
    /* width: 500px; */
    background-color: orange;
    margin-top: 5px;
    text-align: center;
  }
  .test2-enter-active{
    animation: test1 .5s linear ;
  }
  .test2-leave-active{
    animation: test1 .5s linear reverse;
  }
  @keyframes test1{
    from{
      transform:translateX(100%)
    }
    to{
      transform:translateX(0px)
    }
  }
</style>
