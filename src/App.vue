<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="handleAddTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" 
      @editTodo="handleEditTodo" 
      @removeTodo="handleRemoveTodo"
      @toggleTodo="handleToggleTodo">
      </TodoList>
    <TodoFooter v-on:clearTodo="handleClearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInputVue from './components/TodoInput.vue'
import TodoListVue from './components/TodoList.vue'
import TodoFooterVue from './components/TodoFooter.vue'

export default {
  data() {
    
        return {
            todoItems: [],
        
        }
    },
     methods: {
        handleAddTodo(todo) {
            const todoItem = {todo, 'done': false};
            localStorage.setItem(todo, JSON.stringify(todoItem));
            this.todoItems.push(todoItem);
        },

        handleClearAll() {
          console.log("claer all button clicked!");
          localStorage.clear();
          this.todoItems = [];
        },

        handleRemoveTodo(todoItem, index) {
            console.log("remove Item!");
            
            localStorage.removeItem(todoItem.todo);
            this.todoItems.splice(index,1);
        },

        handleEditTodo(todoItem, index) {
         
          localStorage.setItem(todoItem.todo, JSON.stringify(todoItem));
          this.todoItems[index] = todoItem;
        },

        handleToggleTodo(index) {
          console.log(index);
          //this.todoItems[index] = {...this.todoItems[index], 'done': !this.todoItems[index].done};
          this.todoItems[index].done =  !this.todoItems[index].done;
          const todoItem = this.todoItems[index];
          localStorage.setItem(todoItem.todo, JSON.stringify(todoItem));
        }
       
    },
    created() {
        if(localStorage.length > 0) {
            let key;
            for(let i=0; i< localStorage.length; i++) {
                key = localStorage.key(i);
                this.todoItems.push(JSON.parse(localStorage.getItem(key)));
            }
        }
    },
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInputVue,
    'TodoList': TodoListVue,
    'TodoFooter': TodoFooterVue
  }  
  
}
</script>

<style>
  body {
    text-align: center;
    background: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;

  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
  
</style>
