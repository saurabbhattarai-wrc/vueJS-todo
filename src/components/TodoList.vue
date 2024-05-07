<template>
  <div class="bg-gray-100 min-h-screen flex items-center justify-center">
    <div class="max-w-md w-full bg-white p-8 rounded-lg shadow-md">
      <h1 class="text-3xl font-semibold text-center mb-8">TODO APP</h1>
      
      <div class="mb-6">
        <input type="text" class="w-full border border-gray-300 rounded-md px-4 py-2" v-model="newTodo" placeholder="Add a new todo">
        <button class="mt-2 w-full bg-blue-500 text-white rounded-md px-4 py-2 font-semibold hover:bg-blue-600" @click="addTodo">Add Todo</button>
      </div>
      
      <div>
        <ul>
          <li v-for="(todo, index) in todos" :key="index" class="flex justify-between items-center py-2 border-b border-gray-300">
            <div :class="{ 'line-through': todo.completed }">{{ todo.todoString }}</div>
            <div>
              <button class="text-blue-500 hover:text-blue-700 mr-2" @click="toggleTodo(todo)">{{ todo.completed ? 'Undo' : 'Complete' }}</button>
              <button class="text-red-500 hover:text-red-700" @click="deleteTodo(todo)">Delete</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {                                              // data initialization // 
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  mounted() {                                                       // mounted hook "local storage vata saved todos herna ko laage" // 
    
    const savedTodos = JSON.parse(localStorage.getItem('todos'));    // JSON.parse() is used to parse the string retrieved from local storage into a JavaScript object//
    if (savedTodos) {
      this.todos = savedTodos;
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {                         // adding new todo trim ley white spaces yeta uti haru hatauxa// 
        this.todos.push({
          todoString: this.newTodo,                               // constructor ma value pass gareko, naya string ko//
          completed: false
        });
                                                                // Save todos to local storage
        localStorage.setItem('todos', JSON.stringify(this.todos));
        this.newTodo = '';
      }
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;                           // suru ma todo.completed false xa teslai check garni ani local storage ma add garnii//
                                                                    // Save todos to local storage after toggling(changing state) todo completion
      localStorage.setItem('todos', JSON.stringify(this.todos));     // jahela pani stringfy ley javascript value lai JSON ma convert garxa // 
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter(t => t !== todo);
                                                                        // Save todos to local storage after deleting todo
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  }
}
</script>

<style>
.line-through {
  text-decoration: line-through;
}
</style>

// v-for : used for rendering li items based on array, 
           loop ko laage use garinxa basically. 

// v-model : two way binding, 
    jaba user ley kei type garesi, v-model ko karan ley newTodo update hunxa


// yo sabai dynamic rendering ko laage use garinxa