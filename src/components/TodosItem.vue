<template>
  <div class="todo-item" :class="{'is-complete':todo.completed}">
    <input type="checkbox" @change="changeline" :checked="todo.completed" />
    {{todo.title}}
    <!-- 这里是调用爸爸的爸爸的方法 -->
    <p class="del" @click="$emit('delItem')">x</p>
  </div>
</template>

<script>
export default {
  props: ["todo"],
  methods: {
    changeline() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background-color: #f00;
  color: #fff;
  border: none;
  padding: 5px 12px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>