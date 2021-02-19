<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>
    <input v-model="todoText" 
    type="text" class="w-100 p-2" placeholder="Type todo" @keyup.enter="addTodo"  >
  </div>
  <Todo v-for="todo in todos" :key="todo.id" :todo="todo"  @toggle-checkbox="toggleCheckBox"  @click-delete="deletetodo" />
  
  {{ todos }}
  <br>
  {{ msg }}
</template>

<script>

import Todo from '@/components/Todo';

export default {
  components:{
    Todo
  },
  data(){
    return {
      todoText: '',
      todos: [
        {id: 1, text: 'buy a car', checked:false},
        {id: 2, text: 'study vue', checked:false}
      ],
      msg: 'helloworld'
    }
  },

  methods: {
    addTodo(e) {
      this.todos.push({
        id: Math.random(),
        text: e.target.value,
        checked: false
      });
      this.todoText = '';
    },
    
    toggleCheckBox({id,checked}){
      const index = this.todos.findIndex(todo =>{
        return todo.id ===id;
      });
      this.todos[index].checked = checked;
    },
    
    deletetodo(id){
      const index = this.todos.findIndex(todo =>{
        return todo.id ===id;
      });
      //console.log(index);
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style>

</style>