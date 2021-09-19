<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" 
            v-on:change="this.$emit('set-completed' , !this.todo.completed)"
            v-bind:checked="todo.completed"
        >

            <strong class="item-title">{{index+1}}.</strong>
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
    }
    button{
        background: white;
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
</style>