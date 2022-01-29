<template>
    <div class="bg-gray-300  bg-opacity-50 flex justify-center align-stretch items-center absolute top-0 bottom-0 right-0 left-0">
        <div class="bg-white px-14 py-14 rounded-md">
            <h1 class="capitalize text-center text-md mb-4 font-bold text-slate-400">please enter todo details</h1>

            <div class="flex flex-col space-y-3 align-start">
                <input class="h-8 rounded-md text-black font-light border-gray-400 border-double  border-2 focus:border-gray-500" placeholder="todo title" v-model="newTodo.todoTitle" />
                <input class="h-8 rounded-md text-black font-light border-gray-400 border-double  border-2 focus:border-gray-500" placeholder="todo description" v-model="newTodo.todoDescription" />
                <input class="h-8 rounded-md text-black font-light border-gray-400 border-double  border-2 focus:border-gray-500" placeholder="todo priority" v-model="newTodo.todoPriority" />

            </div>
            <button
                    class="mt-10 text-white bg-red-500 font-light w-64 h-12 rounded-md disabled:opacity-50"
                    :disabled="validForm === false"
                    @click="submitForm"
            >submit</button>

        </div>

    </div>
</template>


<script lang="ts">
    import {defineComponent, ref,computed} from 'vue'
    import TodoModel from "../Model/TodoModel";
    export default defineComponent({
        setup(props, { emit }){
            let newTodo = ref<TodoModel>({todoTitle: '', todoDescription: '', todoPriority: ''})
            const submitForm = () => {
                emit('add:todo',newTodo.value)
                emit('close')
            }
            const validForm = computed(() => {
              return newTodo.value.todoTitle != '' && newTodo.value.todoDescription != '' && newTodo.value.todoPriority != ''
            })
            return{newTodo,submitForm,validForm}
        }
    })
</script>

<style scoped>

</style>
