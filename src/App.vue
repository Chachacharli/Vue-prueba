<script>
import Main from './components/Main/Main.vue';

export default {
  components: {
    Main: Main
  },

  data(){
    return{
      todos: [],
    }
  },

}

</script>

<template>

  <Main></Main>

</template>

<style >

body{
  background-color: #202124;
}

</style>
