<script setup>
</script>

//API KEY Mp_uMwm0Rxm91cOheKCgDJ2VELCbiuz2V6ztp1n4pkBURVT-Rw

<template>
    <Nav></Nav>
    <div class="md:container md:mx-auto ">
        <InputTodo @useTodo="newTodo" />
        <TodoList :todos="this.todos"/>

    </div>



</template>

<script>
import TodoList from '../TodoList/TodoList.vue';
import InputTodo from '../InputTodo/InputTodo.vue';
import Nav from '../Nav.vue'



function  fetchTodos() {
       fetch('https://crudcrud.com/api/1956116b3a6c44abb7f994481423e217/todos')
        .then(response => response.json())
        .then(data => {
          this.todos = data; 
        })
        .catch(error => {
          console.error(error);
        });
    }

function newTodo(newTodo){
    this.todos.push(newTodo) 
}


export default { 
    name: "Main",
    components:{
        TodoList: TodoList,
        InputTodo: InputTodo,
        Nav: Nav
    },
    data(){
        return{
            todos: []
        }
    },
    methods: {
        fetchTodos,
        newTodo
    },
    mounted(){
        this.fetchTodos() 
    }
}

</script>