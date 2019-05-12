<template>
  <div>
    <input type="text" v-model="currentText" v-on:focus="hideErrorMessage" />
    <button v-on:click="addTodo">add</button>
    <div class="error" v-if="isError">Please enter a text</div>
    <ol>
      <li
        is="todo-item"
        v-for="todo in visibleTodos"
        v-bind:todo="todo"
        v-bind:key="todo.id"
      ></li>
    </ol>
    <toolbar v-on:change-visible-todos="whatToShow = $event" />
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
import Toolbar from './Toolbar.vue';

export default {
  name: 'Main',
  components: {
    'todo-item': TodoItem,
    toolbar: Toolbar,
  },
  data: () => ({
    isError: false,
    whatToShow: 'all',
    currentText: '',
    nextId: 3,
    todos: [
      { id: 0, text: 'Learn JavaScript', completed: false},
      { id: 1, text: 'Learn Vue', completed: false},
      { id: 2, text: 'Build something awesome', completed: false},
    ],
  }),
  computed: {
    visibleTodos: function() {
      switch(this.whatToShow) {
        case 'all':
          return this.todos;
        case 'active':
          return this.todos.filter(todo => !todo.completed);
        case 'completed':
          return this.todos.filter(todo => todo.completed);
        default:
          return this.todos;
      }
    },
  },
  methods: {
    addTodo: function() {
      if (this.currentText.trim().length === 0) {
        this.isError = true;
        return;
      }
      this.todos.push({id: this.nextId, text: this.currentText, completed: false});
      this.nextId++;
      this.currentText = '';
    },

    hideErrorMessage: function() {
      this.isError = false;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ol {
  list-style-type: none;
  padding: 0;
}
</style>
