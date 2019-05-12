<template>
  <li
    v-bind:class="todo.completed ? 'completed': 'normal'"
    v-on:click="todo.completed = !todo.completed"
  >
    {{ todo.text }}
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: Object
  }
}
</script>

<style scoped>
  .completed {  
    text-decoration: line-through;
  }
</style>
