<template>
  <TodoHeader :appTitle="title"></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
import { ref } from 'vue'
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'


export default {
  components: { TodoHeader, TodoInput, TodoList },
  data(){
    return{
      title : '할일 앱'
    }
  },
  setup(){
    const todoItems = ref([]);

    function fetchTodos(){
      const result = [];
        for (let i = 0; i < localStorage.length; i++) {
            const todoItem = localStorage.key(i);
            // items.value.push(todoItem);
            result.push(todoItem);
        }
        return result;
    }

    function addTodoItem(todo){
      todoItems.value.push(todo);
      localStorage.setItem(todo,todo);
    }

    function removeTodoItem(item, index){
      todoItems.value.splice(index, 1);
      localStorage.removeItem(item, item);
    }

    todoItems.value = fetchTodos();

    return { todoItems, addTodoItem, removeTodoItem };

  }
}
</script>

<style lang="scss" scoped>

</style>