<template>
  <li>
    <div class="todoItem">
      <div>
        <button
          v-if="!isEditing"
          :class="{ completed }"
          @click="$emit('on-toggle')"
          class="todoItemButton"
        >
          {{ todoString }}
        </button>
        <form v-else @submit:prevent="endEditing()">
          <input @blur="startEditing()" type="text" v-model="newTodoString" />
        </form>
      </div>
      <div>
        <button @click="startEditing()" class="editButton">Edit</button>
        <button @click="$emit('on-delete')" class="deleteButton">Delete</button>
      </div>
    </div>
  </li>
</template>
<script>
export default {
  name: 'TodoList',
  props: {
    todoString: String,
    completed: Boolean,
  },
  data() {
    return {
      isEditing: false,
      newTodoString: '',
    };
  },
  methods: {
    startEditing() {
      if (!this.isEditing) {
        this.newTodoString = this.todoString;
        this.isEditing = true;
      } else {
        this.endEditing();
      }
    },

    endEditing() {
      this.isEditing = false;
      this.$emit('on-edit', this.newTodoString);
    },
  },
};
</script>
<style scoped>
.completed {
  text-decoration: line-through;
}
li {
  list-style: none;
}
.todoItem {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  border: 1px solid #a8a39d;
  padding: 7px;
}
.todoItemButton {
  background-color: transparent;
  border: 0;
  text-align: left;
}
input {
  background-color: transparent;
  border-radius: 6px;
  margin: 5px;
}
.editButton {
  color: #028f76;
  border-radius: 3px;
  border: 1px solid #028f76;
  margin-right: 3px;
  padding: 4px;
}
.editButton:hover {
  background-color: #028f76;
  color: aliceblue;
}
.deleteButton {
  color: #d14334;
  border-radius: 3px;
  border: 1px solid #d14334;
  background: transparent;
  padding: 4px;
}
.deleteButton:hover {
  background-color: #d14334;
  color: aliceblue;
}
</style>
