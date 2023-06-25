
<template>
        <main class="" >
            <h2 class="text-gray-300 text-2xl w-full justify-center items-center text-center md:text-start">To do's</h2>
            <div class="grid grid-cols-1 content-center	 md:content-normal  md:grid-cols-4 gap-4">
                
                <div class="w-full flex justify-center grid-cols-2 md:grid-cols-4 gap-2" v-for="todo in todos" :key="todo.id">      
                        <article v-if="todo.completed" class="w-[300px]  break-inside-avoid h-auto group rounded my-5 p-3 bg-[#1E3A5F]  duration-300 ease-out hover:shadow-2xl">    
                            <p class="text-slate-200"> {{ todo.todo }}</p>
                            <p class="mt-2 text-slate-200 mb-2"> {{ todo.completed ? 'Completed' : 'In process' }}  </p>
                            <div class="duration-200 opacity-0 group-hover:opacity-100 flex  gap-1 m-0 [&>div]:cursor-pointer">
                                <div @click="modifyTodo(todo)" id="edit-btn" class=" flex items-center justify-center w-[30px] p-1 hover:bg-neutral-500 hover:bg-opacity-50 duration-150 rounded-full" >
                                    <i class=" text-white bi bi-clipboard"></i>
                                </div>
                                <div @click="deteleTodo(todo._id)" id="edit-btn" class=" flex items-center justify-center w-[30px] p-1 hover:bg-neutral-500 hover:bg-opacity-50 duration-150 rounded-full" >
                                    <i class="text-white bi bi-trash"></i>
                                </div>                                
                            </div>
                        </article>

                        <article  v-if="!todo.completed" class="w-[300px] group h-auto rounded my-5 p-3 bg-[#5C2B29]  duration-300 ease-out hover:shadow-2xl">    
                            <p class="text-slate-200"> {{ todo.todo }}</p>
                            <p class="mt-2 text-slate-200  mb-2"> {{ todo.completed ? 'Completed' : 'In process' }} </p>        
                            
                            <div class="duration-200 opacity-0 group-hover:opacity-100 flex [&>div]:cursor-pointer gap-1 m-0">
                                <div id="edit-btn" class=" flex items-center justify-center w-[30px] p-1 hover:bg-neutral-500 hover:bg-opacity-50 duration-150 rounded-full" >
                                    <i @click="modifyTodo(todo)" class=" text-white bi bi-clipboard"></i>
                                </div>
                                <div @click="deteleTodo(todo._id)" id="edit-btn" class=" flex items-center justify-center w-[30px] p-1 hover:bg-neutral-500 hover:bg-opacity-50 duration-150 rounded-full" >
                                    <i class="text-white bi bi-trash"></i>
                                </div>                                
                            </div>                            
                        </article>                           
                    
                    </div>
            </div>
        </main>        

        <Popup 
        v-if="popupTriggers.btnTrigger"
        :TogglePopup="()=>TogglePopup('btnTrigger')"
        :currentTodo="this.currentTodo">            
        </Popup>
        

</template>


<script>
import TodoCard from '../TodoCard/TodoCard.vue';
import Popup from '../Popup/Popup.vue';
import { ref } from 'vue';
import { isProxy, toRaw } from 'vue';


function modifyTodo(e){
    this.$data.currentTodo = toRaw(e)
    this.popupTriggers.btnTrigger = true
}

function deteleTodo(e){
    fetch(`https://crudcrud.com/api/1956116b3a6c44abb7f994481423e217/todos/${e}`, {
        method: 'DELETE',
        })
    const index = this.todos.findIndex(obj => obj._id === e)
    this.todos.splice(index, 1);

}

function selectCurrentTodo(e){
    console.log(e)
}


export default{
    name: 'TodoList',
    components:{
    TodoCard: TodoCard,
    Popup: Popup

    },
  methods: {
    modifyTodo,
    deteleTodo,
  },
  props:{
    todos: [],
  },

  data(){
    return{
        currentTodo: {}
    }

 }, 

  setup () {
		const popupTriggers = ref({
			btnTrigger: false,
			timedTrigger: false
		});

		const TogglePopup = (trigger) => {
			popupTriggers.value[trigger] = !popupTriggers.value[trigger]
		}

		setTimeout(() => {
			popupTriggers.value.timedTrigger = true;
		}, 3000);

		return {
			popupTriggers,
			TogglePopup
		}
	}
}


</script>