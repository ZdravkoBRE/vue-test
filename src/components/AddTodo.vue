<template>
  <form @submit.prevent="addTodo">
    <input type="text" name="title" v-model="title" placeholder="Add Todo...">
    <input type="submit" value="Submit" class="btn">
  </form>
</template>

<script>

export default {
  name: 'AddTodo',
  data () {
    return {
      title: ''
    }
  },
  methods: {
    addTodo() {
      const newTodo = {
        title: this.title,
        completed: false
      }

      // Send up to parent
      this.$emit('add-todo', newTodo);

      this.title = '';
    }
  }
}
</script>

<style lang="scss" scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
    &:hover{
      background: #666;
    }
  }
</style>