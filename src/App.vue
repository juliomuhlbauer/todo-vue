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
      });

      e.target.reset();
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

  <ul>
    <li
      v-for="todo in todos"
      :style="{ 'text-decoration': todo.done ? 'line-through' : 'none' }"
      @click="todo.done = !todo.done"
    >
      {{ todo.title }}
    </li>
  </ul>
</template>
