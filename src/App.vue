<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <my-header :addthing="addthing"></my-header>
        <list :todos="todos" :checkthing="checkthing" :deletething="deletething"></list>
        <my-footer :todos="todos" :checkAllthings="checkAllthings" :clearDoneThing="clearDoneThing"></my-footer>
      </div>
    </div>
  </div>
</template>

<script>
import List from './components/List.vue'
import MyFooter from './components/MyFooter.vue'
import MyHeader from './components/MyHeader.vue'

export default {
  components: { MyHeader, List, MyFooter },
  name: 'App',
  data() {
    return {
      //事情储存为对象集合成数组，储存在list中
      todos:JSON.parse(localStorage.gerItem('todos'))||[]
      
    }
  },
  methods: {
    //添加事情到列表
    addthing(thing){
      this.todos.unshift(thing)
    },
    //通过复选框改变事情的状态
    checkthing(id){
  this.todos.forEach((thing) => {
      if(thing.id === id) thing.done = !thing.done
  });
    },
    //删除对应事件thing
    deletething(id){
      this.todos = this.todos.filter((thing)=>{
        return thing.id !==id
      })
    },
    //根据footer里面的全选按钮来决定事件的勾选
    checkAllthings(done){
      this.todos.forEach((thing)=>{
        thing.done = done
      })
    },
    //清除已经完成的事情
    clearDoneThing(){
     this.todos = this.todos.filter((thing)=>{
        return !thing.done
      })
    }
  },
  //事情存入浏览器内存，实现本地记事本效果
  watch:{
    todos(value){
      localStorage.setItem('todos',JSON.stringify(value))
  }
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-edit {
  color: #fff;
  background-color: lightgreen;
  border: 1px solid green;
  margin-right: 5px;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn-edit:hover {
  color: #fff;
  background-color: green;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
