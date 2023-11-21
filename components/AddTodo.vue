<template>
  <div>
    <form class="todo-form" @submit.prevent="todoData">
      <input
        type="text"
        v-model="newTodo"
        placeholder="What you will to do today"
        class="todo-input"
      />
      <button type="submit" class="add-button">Add Todo</button>
    </form>
    <TodoList :todoData="todos" @removeItem="removeList($event)"></TodoList>
  </div>
</template>
<script>
import TodoList from "./TodoLIst.vue";
export default {
  name: "AddTodo",
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  components: {
    TodoList,
  },
  mounted() {
    const cacheData = JSON.parse(localStorage.getItem("addedTodos"));
    if (cacheData && cacheData.length > 0) {
      this.todos = cacheData;
    }
  },
  watch: {
    todos: {
      handler(val) {
        localStorage.setItem("addedTodos", JSON.stringify(val));
      },
      deep: true,
    },
  },
  methods: {
    todoData() {
      // console.log(this.newTodo);
      if (this.newTodo) {
        this.todos.push(this.newTodo?.trim());
        this.newTodo = "";
      }
    },
    removeList(index) {
      this.todos.splice(index, 1);
      // console.log(index)
    },
  },
};
</script>
<style>
.todo-form {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
.todo-input {
  width: 300px;
  height: 50px;
}
.todo-input::placeholder {
  text-align: center;
}
.todo-list {
  display: flex;
  list-style: none;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 30px;
  margin-top: 1rem;
}
.todo-list > li {
  font-size: 1rem;
  border: 1px solid;
  padding: 10px;
  width: 50vh;
  text-align: center;
}
.add-button {
  width: 100px;
  height: 50px;
  background-color: #2196f3;
  color: whitesmoke;
  cursor: pointer;
  font-weight: bold;
}
</style>