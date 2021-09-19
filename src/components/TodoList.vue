<template>
    <div class="todo__list">
        
        <ul>
            <TodoItem
            v-for="(todo, i) of todos"
            :index="i"
            :key="todo.id"
            :todo="todo"
            @set-completed="val => { todo.completed = val }"
            @remove-item="handleRemove"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from "./TodoItem.vue"
export default {
    name: 'TodoList',
    methods:{
        handleRemove(id){
            this.$emit('remove-item', id)
            console.log(this.todos)
        }
    },
    components:{
        TodoItem,
    },
    props: ['todos']
}
</script>

<style scoped>
ul{
      list-style: none;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      width: 100%;
      padding: 0;
}
    .todo__list{
        margin: 0;
        display: flex;
    }
</style>