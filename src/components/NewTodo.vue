<template>
  <form @submit.prevent="addTodo()">
    <input type="text" v-model="newTodo" />
  </form>
</template>
<script>
export default {
  name: 'NewTodo',
  data() {
    return {
      newTodo: '',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 1) {
        this.$emit('on-addTodo', this.newTodo);
      }
      this.newTodo = '';
    },
  },
};
</script>
<style scoped>
input {
  background-color: transparent;
  border-radius: 6px;
  margin: 5px;
  border: 1px solid #000;
  width: 350px;
  padding: 4px;
}
</style>
