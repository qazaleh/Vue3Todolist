<template>
    <div class=" todo-item  hover:shadow-md ">
        <ul   class="list-disc  pl-3">
            <li class="todo-title">{{todoItem.todoTitle}} ({{shorterDesc}})</li>
            <p class="todo-subtitle">{{todoItem.todoPriority}}</p>
        </ul>
        <div class="flex justify-end">
            <button class="rounded-full h-6 w-6" @click="removeTodo" >
                <XCircleIcon class="h-6 w-6 text-red-500"></XCircleIcon>
            </button>
        </div>
    </div>
</template>
<script lang="ts">
    import { XCircleIcon } from '@heroicons/vue/solid'
    import TodoModel from "../Model/TodoModel";
    import {computed, defineComponent, PropType} from "vue";
    export default defineComponent({
        name: 'TodoItem',
        components: { XCircleIcon },
        props:{
          todoItem :{
              required:true,
              type: Object as PropType<TodoModel>
          }
        },

        setup(props,{emit}){
            const removeTodo = () => {
                emit('remove:todo',props.todoItem)
            }
            const shorterDesc = computed(() => {
                return props.todoItem.todoDescription.substring(0,20) + "...."
            })
            return {removeTodo,shorterDesc}
        }

    })
</script>


<style scoped>

</style>
