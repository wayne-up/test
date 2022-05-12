// list组件，item的父组件，作为所有代办的容器
<template>
    <div id="list">
    <transition-group name="test2">
        <Item 
        v-for="todo in todolist" 
        :key="todo.id"
        :todo="todo"
        />
    </transition-group>

    </div>
</template>

<script>
import Item from './Item.vue'
    export default {
        name:'List',
        components:{Item},
        props:['todolist',]
    }
</script>

<style scoped>
    #list{
        width: 580px;
        border: 1px solid rgb(189, 189, 189);
        border-bottom:  none;
        margin: 10px 0;
    }
</style>

