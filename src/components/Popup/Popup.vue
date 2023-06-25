<template>
	<div class="popup">
		<div class="popup-inner">
            <form @submit.prevent="handlerForm">
                <div class="flex flex-col">
                    <input autocomplete="off" type="text" name="todo" :placeholder="currentTodo.todo"/>
                    
                    <input type="checkbox" :checked="currentTodo.completed" id="react-option" name="finished" value=" " class="hidden peer w-[50px] h-[25px]">
                    <label for="react-option" class="inline-flex mt-2 w-25 items-center justify-between p-5 text-gray-500 bg-white border-2 border-gray-200 rounded-lg cursor-pointer dark:hover:text-gray-300 dark:border-gray-700 peer-checked:border-blue-600 peer-checked:bg-blue-600 peer-checked:text-white hover:text-gray-600 dark:peer-checked:text-gray-300 hover:bg-gray-50 dark:text-gray-400 dark:bg-gray-800 dark:hover:bg-gray-700">                           
                        {{ currentTodo.finished ? 'Sin terminar': 'Terminar' }}
                    </label>
                
                </div>

                <div class="flex justify-around gap-2 m-2">

                    <button name="btnSubmit" type="submit" class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">
                        Save
                    </button>
                    <button 
                    @click="TogglePopup()"
                    name="btnClose"
                    class="bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded">
                        Close
                    </button>
                
                </div>
            </form>
		</div>  
	</div>
</template>


<script>

function handlerForm(e){
    const id = this.currentTodo._id
    const obj = {
        todo: e.target.elements.todo.value ? e.target.elements.todo.value : e.target.elements.todo.getAttribute("placeholder"),
        completed: e.target.elements.finished.checked,
        userId: 5
    }
    
    fetch(`https://crudcrud.com/api/1956116b3a6c44abb7f994481423e217/todos/${id}`,{
        method: "PUT",
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(obj)})
    
    this.$emit('returnTodo', {id, obj} )
}


export default {
	props: ['TogglePopup', 'currentTodo'],
    data(){
        return{
            formData: {}            
        }
    },
    methods:{
        handlerForm,
    }

}


</script>

<style scoped>
.popup {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	z-index: 99;
	background-color: rgba(0, 0, 0, 0.2);
	display: flex;
	align-items: center;
	justify-content: center;
    
}
	.popup-inner {
		background: #FFF;
		padding: 32px;
        width: 300px;
	}

</style>