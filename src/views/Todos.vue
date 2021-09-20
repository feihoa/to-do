<template>
  <div class="todos-container">
      <router-link class="to-home__link" to="/">Главная</router-link>
    <h2 class="app__header">Список</h2>
    <AddTodo
      @add-item="handleAdd"
    />
    <select v-model="filter"> 
        <option value="all">Все</option>
        <option value="completed">Только завершенные</option>
        <option value="not-completed">Только незаверенные</option>
    </select>
      <hr>      
      <Loader v-if="loading"/>

      <TodoList
      v-else-if="filterTodos.length"
      v-bind:todos="filterTodos"
      @remove-item="handleRemove"
      :key='toDoListKey'
      />
      <p v-else>Дел не осталось!</p>
  </div>
</template>


<script>
import TodoList from '../components/TodoList.vue'
import AddTodo from "../components/AddTodo.vue"
import Loader from "../components/Loader.vue"

export default {
  name:'Todos', 
  components: {
    TodoList,
    AddTodo,
    Loader

  },
  data(){
    return{
      todos:[],
      loading:true,
      filter:'all',

    }
  },
  computed:{
      filterTodos(){
          if(this.filter == 'all'){
              return this.todos
          }else if(this.filter==='completed'){
            return this.todos.filter(todo => todo.completed)
          }else{
            return this.todos.filter(todo => !todo.completed)

          }
      }
  },
  methods:{

    handleRemove(id){
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    handleAdd(item){      
      this.todos.push(item)
    },
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=30')
    .then(response => response.json())
    .then(json => {
    this.todos = json;
    this.loading=false
    }
    )
    
  }
}
</script>

<style>
    select{
        margin-top:10px;
        display: flex;
        justify-self: start;
        margin-bottom:20px

    }
    .app__header{
        margin-top:20px;
    }
    .to-home__link{
        text-decoration: none;
        font-weight: bold;
        border: 1px solid black;
        color:black;
        align-items: left;
        padding:6px;
        margin-top:20px;
    }
    .todos-container{
        margin-top:20px

    }
</style>