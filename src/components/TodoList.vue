<template>
  <div class="container">
    <h1>{{ listName }}</h1>
    <CreateTodo @newTodo="addTodo($event)" />
    <ul>
      <Todo
        v-for="(todo, index) in todos"
        :key="index"
        :description="todo.description"
        :completed="todo.completed"
        @onDelete="deleteTodo(todo.id)"
        @onEdit="editTodo(todo, $event)"
      />
    </ul>
  </div>
</template>

<script>
import Todo from "@/components/TodoListItem";
import CreateTodo from "@/components/FormTodo";
import shortid from "shortid";
export default {
  props: {
    listName: String,
  },
  data() {
    return {
      todos: [
        { description: "Task 1", completed: false, id: 1 },
        { description: "Task 2", completed: false, id: 2 },
        { description: "Task 3", completed: false, id: 3 },
      ],
    };
  },
  components: { Todo, CreateTodo },
  methods: {
    addTodo(newTodo) {
      this.todos.push({
        description: newTodo,
        completed: false,
        id: shortid(),
      });
    },

    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },

    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    },
  },
};
</script>

<style lang="scss" scoped>
ul {
  list-style: none;
  padding: 0;
}

.container {
  margin: 0 auto;
  width: 900px;
  display: flex;
  flex-direction: column;
}
</style>
