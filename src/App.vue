<template>
  <div id="app">
    <Header />
    <add-todos @handleAdd="handleAddTodo"></add-todos>
    <div class="container">
      <Todos :todos="datas" @delItem="delItem"></Todos>
    </div>
  </div>
</template>

<script>
import Todos from "./components/Todos";
import AddTodos from "./components/AddTodo";
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      datas: []
    };
  },
  methods: {
    delItem(id) {
      // 这里也可以用splice,但有时候id不一定是连续的数字
      // this.datas = this.datas.filter(item => item.id != id);

      // 删除对象
      axios
        .delete(`http://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          console.log(res);
          this.datas = this.datas.filter(item => item.id != id);
        })
        .catch(err => console.log(err));
    },
    handleAddTodo(newTodo) {
      // this.datas = [...this.datas,newTodo] --> es6语法，与push方法相同

      // es6语法，与shift方法相同
      // this.datas = [newTodo, ...this.datas];

      // 添加数据
      axios
        .post("http://jsonplaceholder.typicode.com/todos", newTodo)
        .then(res => {
          this.datas = [newTodo, ...this.datas];
        })
        .catch(err => console.log(err));
    }
  },
  components: {
    Todos,
    Header: () => import("./components/layout/Hander"), // 懒加载，按需加载
    AddTodos
  },
  mounted() {
    // 请求数据,?_limit=10 服务端提供的一个查询字符串
    axios
      .get("http://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => {
        // console.log(res)
        // console.log(res.data);

        this.datas = res.data;
      })
      .catch(err => console.log(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  line-height: 1.6;
  background: #e8f7f0;
}
/* .container {
  max-width: 1100px;
  margin: auto;
  overflow: auto;
  padding: 0 2rem;
} */
</style>
