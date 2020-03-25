<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="text" placeholder="请输入代办事项。。。" v-model="title" />
      <input type="submit" value="提交" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      //   e.preventDefault();
      const newTodo = {
        // id: uuidv4(),
        title: this.title,
        completed: false
      };
      console.log(newTodo);

      this.$emit("handleAdd", newTodo);
    }
  }
};
</script>

<style scoped>
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
  background-color: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background-color: #666;
}
</style>