<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <my-header ></my-header>
        <list :todos="todos"></list>
        <my-footer :todos="todos" @checkAllthings="checkAllthings" @clearDoneThing="clearDoneThing"></my-footer>
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
<<<<<<< HEAD
      //事情储存为对象集合成数组，储存在list中
      todos:JSON.parse(localStorage.gerItem('todos'))||[]
      
=======
      //事情对象存储在浏览器内存中，下次刷新不会丢失数据
      //JSON.parse(解析的数据)将JSON数据解析成js对象
      //JSON.stringify(value)将js对象转换为JSON格式
      todos: JSON.parse(localStorage.getItem("todos")) || []
    }
  },
  watch: {
    //开启深度监视
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
>>>>>>> 7bc8949 (bin update function)
    }
  },
  methods: {
    //添加事情到列表
    addThing(thing) {
      this.todos.unshift(thing)
    },
    //通过复选框改变事情的状态
    checkThing(id) {
      this.todos.forEach((thing) => {
        if (thing.id === id) thing.done = !thing.done
      });
    },
    //删除对应事件thing
    deleteThing(id) {
      this.todos = this.todos.filter((thing) => {
        return thing.id !== id
      })
    },
    //根据footer里面的全选按钮来决定事件的勾选
    checkAllthings(done) {
      this.todos.forEach((thing) => {
        thing.done = done
      })
    },
    //清除已经完成的事情
    clearDoneThing() {
      this.todos = this.todos.filter((thing) => {
        return !thing.done
      })
    },
    //编辑事件回调
     updateThing(id, name) {
      this.todos.forEach((thing) => {
        if (thing.id === id) thing.name = name
      });
    },
  },
<<<<<<< HEAD
  //事情存入浏览器内存，实现本地记事本效果
  watch:{
    todos(value){
      localStorage.setItem('todos',JSON.stringify(value))
=======
  //监视：将事情都加入浏览器本地缓存
  mounted() {
    this.$bus.$on('addThing',this.addThing)
    this.$bus.$on('checkThing', this.checkThing)
    this.$bus.$on('deleteThing', this.deleteThing)
     this.$bus.$on('updateThing',this.updateThing)
  },
  beforeDestroy() {
     this.$bus.$off('addThing')
    this.$bus.$off('cherkedThing')
    this.$bus.$off('deleteThing')
    this.$bus.$off('updateThing')
>>>>>>> 7bc8949 (bin update function)
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
