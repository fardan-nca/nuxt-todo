<template>
    <div>
      <ul class="todo-list">
            <li v-for="(todo, index) in todoData" :key="index">
                {{todo}}
                <button @click="removeTodo(index)" class="todo-delete">Delete</button>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'TodoList',
    props: {
        todoData:Array,
    },
    methods:{
        removeTodo(index) {
            this.$emit('removeItem', index);
        }
    }
}
</script>
<style>
.todo-delete {
    height: 30px;
    background-color: #ff1744;
    color: whitesmoke;
    outline: none;
    font-weight: bold;
}
</style>