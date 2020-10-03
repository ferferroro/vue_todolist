<template>
    <div>
        <div v-bind:key="todo" v-for="todo in todos">
            <h3>
                <!-- <TodoItem v-bind:todo="todo" /> -->
                <TodoItem v-bind:todo="todo" 
                    @set-completed="$value => { todo.completed = $value }"
                    v-on:del-todo="$emit('del-todo', todo.id)"
                     />
                

            </h3>
        </div>
    </div> 
</template>

<script>

import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"]
}
</script>

<style scoped>

</style>