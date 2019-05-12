<template>
  <div>
    <button v-on:click="$emit('change-visible-todos', 'all')">all</button>
    <button v-on:click="$emit('change-visible-todos', 'active')">active</button>
    <button v-on:click="$emit('change-visible-todos', 'completed')">completed</button>
  </div>
</template>

<script>
export default {
  name: 'Toolbar',
}
</script>
