<template>
  <transition name="todo" appear>
    <li>
    <label>
      <input type="checkbox" :checked="thing.done" @change="changedone(thing.id)"/>   
      <span>{{thing.name}}</span>
      
    </label>
    <button class="btn btn-danger" @click="del(thing.id)">删除</button>
    <button class="btn btn-edit">编辑</button>
  </li>
  </transition>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
  name: 'Item',
  //声明接收thing 对象
  props: ['thing',"checkthing","deletething"],
  methods: {
    //勾选或取消勾选
    changedone(id) {
      // 通知App组件将对应todo的done取反
      this.checkthing(id)
    },
    del(id){
      if(confirm('确定删除吗？')){
        //通知App删除对应项
        this.deletething(id)
      }
    },
    // handleEdit(todo) {
    //   if(todo.hasOwnProperty('isEidt')) {
    //     todo.isEdit = true
    //   }else {
    //     this.$set(todo, 'isEdit', true)
    //   }
    //   this.$nextTick(() => {
    //     this.$refs.inputTitle.focus()
    //   })
    // },
    // handleBlur(todo, e) {
    //   let id = todo.id
    //   let title = e.target.value
    //   todo.isEdit = false
    //   if(!e.target.value.trim()) return alert('输入不能为空')
    //   pubsub.publish('updateTodo', {id, title} )
    // }
  },
}
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover{
  background-color: #ddd;
}

li:hover button{
  display: block;
}

.todo-enter-active{
  animation: todo 0.5s linear;
}

.todo-leave-active{
  animation: todo 0.5s linear reverse;
}

@keyframes todo {
  from{
    transform: translateX(100%);
  }
  to{
    transform: translateX(0px);
  }
}
</style>