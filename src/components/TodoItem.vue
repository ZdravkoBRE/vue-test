<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed, 'bla':wMobile}">
        <p>
            <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed" />
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="del">X</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo", "wMobile"],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
            console.log(this.todo);
        }
    }
}
</script>

<style lang="scss" scoped>

.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    &.bla {
        background: #ff0000;
    }
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>