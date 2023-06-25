<template>
    
    <header class="my-5 w-full  flex items-center justify-center">
            <form @submit.prevent="handlerSubmit" action="">
                <input @keypress="hanlderText" 
                required v-model="newtodo" 
                class=" md:w-[500px] w-[200px] h-[60px] bg-[#202124] text-gray-300 border border-gray-300 rounded-[10px] px-3 text-[15px]" 
                type="text" 
                name="todoInput" 
                id="todoInput" 
                placeholder="Dominar el mundo..."
                autocomplete="off">
            </form> 
        </header>
</template>

<script>

async function handlerSubmit(e){
    this.todo = this.newtodo
    this.todo = await addTodo(this.newtodo)
    this.$emit('useTodo', this.todo)
    this.newtodo = '';
}

async function addTodo(todoText){

    const response = await fetch('https://crudcrud.com/api/1956116b3a6c44abb7f994481423e217/todos', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                todo: todoText,
                completed: false,
                userId: 5,
            })
            })
    const todo = await response.json()
    return todo

}


export default{
    name: 'InputTodo',
    data(){
        return{
            newtodo: '',
            todo: {}
        }
    },
    methods: {
        handlerSubmit,
        addTodo,
        
    }
}
</script>