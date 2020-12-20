<template>
  <li>
    <p v-if="!isEditing">{{ description }}</p>
    <form v-if="isEditing" @submit.prevent="finishEditing()">
      <input
        type="text"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>

    <div class="btn-flex">
      <button @click="startEditing()">
        <span>Edit</span>
      </button>
      <button class="btn-danger" @click="$emit('onDelete')">
        <span>Delete</span>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      newTodoDescription: "",
    };
  },

  props: {
    description: String,
    completed: Boolean,
  },

  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },

    finishEditing() {
      this.isEditing = false;
      this.$emit("onEdit", this.newTodoDescription);
    },
  },
};
</script>

<style lang="scss" scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  height: 60px;
  align-items: center;
  justify-content: space-between;
  padding: 10px 5px;
  margin-bottom: 12px;
}

.btn-flex {
  display: flex;
  align-items: center;

  button {
    margin-right: 10px;
    border: none;
    border-radius: 5px;
    background-color: blue;
    padding: 5px 10px;
    color: #fff;
    transition: all 0.1s linear;

    &:hover {
      background-color: #070740;
    }

    &:last-child {
      margin-right: 0;
    }
  }

  .btn-danger {
    background-color: #990000;
    &:hover {
      background-color: red;
    }
  }
}
</style>
