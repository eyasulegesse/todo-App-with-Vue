<template>
  <div class="container">
    <h3>Todo Application</h3>
    <NewTodo @on-addTodo="addTodo($event)" />
    <div>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todoString="todo.todoString"
        :completed="todo.completed"
        @on-delete="deleteTodo(todo)"
        @on-toggle="toggleTodo(todo)"
        @on-edit="editTodo(todo, $event)"
      />
    </div>
  </div>
</template>

<script>
import NewTodo from './NewTodo.vue';
import TodoItem from './TodoItem.vue';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
    NewTodo,
  },
  data() {
    return {
      todos: [
        { todoString: 'Read about Vue', completed: false },
        { todoString: 'Read about React', completed: true },
        { todoString: 'Ready for Interview', completed: false },
      ],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({
        todoString: newTodo,
        completed: false,
      });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    editTodo(todo, todoString) {
      todo.todoString = todoString;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter((t) => t != deletedTodo);
    },
  },
};
</script>
<style>
.container {
  width: 400px;
  margin: auto;

  background-color: #f8f8f8;
  color: rgba(66, 66, 66, 66);
  padding: 5px;
  border-radius: 10px;
}
/* li {
  list-style: none;
} */
</style>
