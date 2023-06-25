

<template>

    <article @click="showDetails" v-if="completed" class="max-w-[350px] h-auto rounded my-5 p-3 bg-[#1E3A5F] cursor-pointer duration-300 ease-out hover:shadow-2xl">    
        <h3 class="py-2 text-2xl text-slate-200"> {{title}} </h3>
        <p class="text-slate-200"> {{ text }}</p>
        <p class="mt-2 text-slate-200"> {{ completed ? 'Completed' : 'In process' }}  </p>   
        <div class="flex gap-5">
        </div>
    </article>

    <article @click="showDetails" v-if="!completed" class="max-w-[350px] h-auto rounded my-5 p-3 bg-[#5C2B29] cursor-pointer duration-300 ease-out hover:shadow-2xl">    
        <h3 class="py-2 text-2xl text-slate-200"> {{title}} </h3>
        <p class="text-slate-200"> {{ text }}</p>
        <p class="mt-2 text-slate-200"> {{ completed ? 'Completed' : 'In process' }} </p>        
    </article>    

</template>

<script>
import { boolean } from 'mathjs';

function showDetails(){
    console.log(this.te)
    this.showDetailModal = true
}

export default{
    name: 'TodoCard',
    props: {
        title: {
            default: '',
            type: String,
        },
        text:{
            default: 'Carta vacia',
            type: String,
        },
        completed: {
            default: false,
            type: boolean,
        }
    } ,
    data(){
        this.title,
        this.text,
        this.completed,
        this.current = 'asdf',
        this.showDetailModal = false
    },
    methods: {
        showDetails,
    }
}
</script>

