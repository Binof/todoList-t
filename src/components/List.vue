<template>
  <ul class="todo-main" v-show="todos.length">
    <item v-for="thing in todos" :key="thing.id" :thing="thing"></item>
  </ul>
</template>

<script>
import Item from './Item.vue'
export default {
  components: { Item },
  name: 'List',
  props:["todos"]
}
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>