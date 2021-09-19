<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type="submit">Добавить</button>
    </form>
</template>

<script>
export default {
    data(){
        return{
            title: ''
        }
    },
    methods:{
        onSubmit(){
            if(this.title.trim()){
                const newTodo ={
                    id:Date.now(),
                    title:this.title,
                    completed:false
                }
                this.$emit('add-item', newTodo)
                this.title=''
            }
        }
    }
}
</script>


<style scoped>
    
    input{
        width: 400px;
    }
    button{
        background: white;
        border:1px solid black;
        margin-left:10px;
        padding: 2px 6px;
        border-radius: 8%;
    }
</style>