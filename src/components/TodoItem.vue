<template>
    <li> <input type="checkbox" 
            v-on:change="this.$emit('set-completed' , !this.todo.completed)"
            v-bind:checked="todo.completed"
        >
        <span v-bind:class="{done: todo.completed}">
           

            <strong class="item-title">{{todo.id}}.</strong>
            {{todo.title.toUpperCase()}}
        </span>
        <button
        v-on:click="$emit('remove-item', todo.id)"
        >x</button>
    </li>
</template>

<script>

export default {
    name: 'TodoItem',
    props:{
        todo:{},
        index:{}
    }, 
}
</script>

<style scoped>
    li{
        text-decoration: none;
        margin-bottom: 20px;
        display: flex;
        justify-content: space-between;
        padding: 0 20px;
        max-width: 100%;
    }
    button{
        background: white;
        width:20px;
        height: 20px;
        border: 1px solid black;
        border-radius: 50%;
        color:blue;
        cursor:pointer;
    }
    .item-title{
        margin-left: 20px;
    }
    .done{
        text-decoration:line-through
    }
    span{
        min-width: 90%;
        text-align: left;
        margin-left: 10px;
    }
</style>