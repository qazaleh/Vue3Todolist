<template>
   <div class="content min-h-full mx-h-full bg-gray-200 m-2 md:m-6 lg:m-8 rounded-xl">
      <div class="flex justify-start  items-center">
         <img src="../assets/todo.ico"
              alt=""
              class="w-20 h-20 rounded-full  m-3"
         >
         <p class="text-left text-red-500  m-3">Todo list</p>
      </div>
      <add-todo-form v-if="showAddForm"
                     @add:todo="addTodo"
                     @close="showAddForm = false"
      />
      <div class="flex justify-end  items-center">
         <button class="bg-blue-800 text-white font-light w-28 h-9 rounded-md  m-3"
                 @click="triggerAddButton"
         >create todo</button>
      </div>
      <div class="flex flex-col space-y-5  py-3 ">
         <todo-item
                 v-for="(item, index) in todoList" :key="index"
                    :todoItem = item
                    @remove:todo="removeTodo"
         >
         </todo-item>
      </div>
   </div>

</template>
<script lang="ts">
   import { defineComponent,ref } from 'vue'
   import  TodoModel from "../Model/TodoModel"
   import AddTodoForm from "./AddTodoForm.vue";
   import TodoItem from "./TodoItem.vue";
   export default defineComponent({
      name:"TodoMain",
      components:{AddTodoForm,TodoItem},
      setup() {
         let showAddForm = ref(false)
         let todoList = ref<TodoModel[]>([])
         const createTodoList = () => {
            todoList.value = [
             { todoTitle: 'meditation',todoDescription:"use mobile app",todoPriority:"hight"},
             { todoTitle: 'exercise',todoDescription:"workout",todoPriority:"medium"},
             { todoTitle: 'learn vue3',todoDescription:"youtube",todoPriority:"hight"},
         ]
         }
         const triggerAddButton = () =>{
            showAddForm.value = true
         }
         function addTodo(todo:TodoModel) {
            todoList.value.push(todo)
         }
         function removeTodo(todo:TodoModel) {
            todoList.value = todoList.value.filter(obj  => obj.todoTitle !== todo.todoTitle);
         }
         createTodoList()
         return{showAddForm, todoList, triggerAddButton,addTodo,removeTodo}
      }
   })

</script>

