<template>
  <div class="home">
    <h1>Home Page</h1>
    <TodoList listName="Vue ToDo Application" />
  </div>
</template>

<script>
import TodoList from "../components/TodoList.vue";
export default {
  name: "Home",
  components: {
    TodoList,
  },
};
</script>
