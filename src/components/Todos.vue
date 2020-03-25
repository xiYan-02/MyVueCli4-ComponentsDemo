<template>
  <div>
    <div v-for="(item, index) in todos" :key="index">
      <TodosItem :todo="item" @delItem="$emit('delItem',item.id)"></TodosItem>
    </div>
    <!-- {{todos}} -->
  </div>
</template>

<script>
import TodosItem from "./TodosItem";

export default {
  props: ["todos"],
  components: {
    TodosItem
  }
};
</script>