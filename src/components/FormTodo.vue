<template>
  <form @submit.prevent="addTodo()">
    <input v-model="newTodo" type="text" placeholder="Create a new ToDo..." />
  </form>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        this.$emit("newTodo", this.newTodo);
      }
      this.newTodo = "";
    },
  },
};
</script>

<style lang="scss" scoped>
form {
  display: flex;
  justify-content: center;
  input {
    width: 400px;
    padding: 5px 10px;
  }
}
</style>
