<template>  
  <div>
  <TodoList /> 
  </div> 
</template> 


<script>  
import TodoList from './components/TodoList.vue'
export default {
  components: { TodoList },      
  name : "App" ,                 // main.js ma yeslai render garnu xa, tehi vayera// 
  comments : { 
    TodoList
  }                              // mention props,components// 

}

</script>  

<style scoped> 

</style>