<script>
export default {
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    add(e) {
      e.preventDefault();

      const formData = new FormData(e.target);

      this.todos.push({
        title: formData.get("title"),
        id: Math.random().toString(),
        done: false,
      });

      e.target.reset();
    },

    remove(id) {
      this.todos.splice(
        this.todos.findIndex((todo) => todo.id === id),
        1
      );
    },
  },
  mounted() {
    const localTodos = localStorage.getItem("todos");

    if (localTodos) {
      this.todos = JSON.parse(localTodos);
    }
  },
  watch: {
    todos: {
      handler(newTodos) {
        localStorage.setItem("todos", JSON.stringify(newTodos));
      },
      deep: true,
    },
  },
};
</script>

<template>
  <h1>Tasks</h1>
  <form @submit="add">
    <input name="title" placeholder="Add a task" />
    <button>add</button>
  </form>

  <div
    :style="{
      display: 'flex',
      margin: '24px 0',
      flexDirection: 'column',
      maxWidth: '200px',
    }"
  >
    <div
      v-for="todo in todos"
      :key="todo.id"
      :style="{
        display: 'flex',
        alignItems: 'center',
      }"
    >
      <input type="checkbox" v-model="todo.done" />
      <input
        :style="{
          textDecoration: todo.done ? 'line-through' : 'none',
          margin: '8px 0',
        }"
        v-model="todo.title"
      />
      <button
        :style="{
          height: '24px',
        }"
        @click="remove(todo.id)"
      >
        x
      </button>
    </div>
  </div>
</template>
