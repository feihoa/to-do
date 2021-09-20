<template>
    <div class="todo__list">
        <ul>
            <TodoItem
            v-for="(todo) of paginatedTodos"
            :index="todo.id"
            :key="todo.id"
            :todo="todo"
            @set-completed="val => { todo.completed = val }"
            @remove-item="handleRemove"
            
            />
        </ul> 
        <div class="todo__pagination" >
            <div class="page"
                :class="{page_selected: page===pageNum}"
                v-for="page in pages"
                :key="page"
                @click="handleClick(page)"
                >{{page}}
            </div>
        </div>
    </div>
</template>

<script>
import TodoItem from "./TodoItem.vue"
export default {
    name: 'TodoList',
    props: ['todos'],
    methods:{
        handleRemove(id){
            this.$emit('remove-item', id)
        },
        handleClick(page){
             this.pageNum = page
        },   
    },
    data(){
        return{
            itemsPerPage:10,
            pageNum:1,
            selectState:'all',

        }
    },
    components:{
        TodoItem,
    },
    computed:{
        pages(){
            return Math.ceil(this.todos.length/this.itemsPerPage)
        },
        paginatedTodos(){     
                let from = (this.pageNum-1)*this.itemsPerPage
                let to = from+this.itemsPerPage
                return this.todos.slice(from,to)
        },
    },
}
</script>

<style scoped>
ul{
      list-style: none;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 0;
}
    .todo__list{
        margin: 0;
        display: flex;
        flex-direction: column;
        max-width: 100%;
    }
    .todo__pagination{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .page{
        padding: 8px;
        border:1px solid #e7e7e7;
        margin-left: 5px;
        cursor: pointer;
    }
    .page:hover{
        background: rgba(0, 63, 253, 0.299);
    }
    .page_selected{
        background: rgba(0, 63, 253, 0.299);
    }
</style>