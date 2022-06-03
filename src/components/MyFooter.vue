<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- 全选按钮的功能实现：让todos里面的thing属性跟着我这个按钮相同即可 -->
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
      <span>已完成{{doneTotal}}件</span> / 全部{{total}}
    </span>
    <button class="btn btn-danger" @click="clearThing">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'MyFooter',
  props:['todos'],
  computed:{
    total(){
      return this.todos.length
    },
    //计算列表事件的完成数量,判断的是thing对象的done属性
    doneTotal(){
      // let i = 0
      // this.todos.forEach((thing) => {
      //   if(thing.done) i++ 
      // });
      // return i
      //reduce数组方法实现:reduce 方法：pre 初始值，current 数组元素
      const x = this.todos.reduce((pre,current)=>{return pre + (current.done ? 1:0)},0)
      return x
    },
    isAll:{
      get(){
        return this.doneTotal === this.total && this.total > 0
      },
      set(value){
         this.$emit("checkAllthings",value) 
      }

    }
  },
  methods: {
    //没有使用v-model时配置的选框改变时调用的方法
   /*   checkedAll(e){
       this.checkAllthings(e.target.checked) 
     } */
     //清除按钮功能的实现
     clearThing(){
       this.$emit('clearDoneThing')
     }
  },
 
}
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>