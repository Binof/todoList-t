<template>
  <transition name="todo" appear>
    <li>
    <label>
      <input type="checkbox" :checked="thing.done" @change="changedone(thing.id)"/>   
       <span v-show="!thing.isEdit">{{thing.name}}</span>
      <input type="text" :value="thing.name" v-show="thing.isEdit"  @blur="handleBlur(thing,$event)" ref="inputThing">
    </label>
    <button class="btn btn-danger" @click="del(thing.id)">删除</button>
    <button class="btn btn-edit"  
    v-show="!thing.isEdit"
     @click="handleEdit(thing)" 
     >编辑</button>
  </li>
  </transition>
</template>

<script>
export default {
  name: 'Item',
  //声明接收thing 对象
  props: ['thing'],
  methods: {
    //勾选或取消勾选
    changedone(id) {
      // 通知App组件将对应todo的done取反
      // this.checkthing(id)
      //总线事件找到App创建的checkThing事件触发返回数据
      this.$bus.$emit('checkThing',id)
    },
    del(id){
      if(confirm('确定删除吗？')){
        //通知App删除对应项
        // this.deletething(id)
        //总线事件找到App创建的deleteThing事件触发返回数据
        this.$bus.$emit('deleteThing',id)
      }
<<<<<<< HEAD
    }
  },
=======
    },
    //编辑按钮功能实现
    handleEdit(thing) {
      // 判断要编辑的事件是否存在isEdit属性
      if (thing.hasOwnProperty('isEdit')) {
        thing.isEdit = true
      } else {
        this.$set(thing, "isEdit", true)
      }
      this.$nextTick(function () {
        this.$refs.inputThing.focus()
      })
    },
  //失去焦点回调（执行修改）
    handleBlur(thing,e) {
      //更改isEdit属性来控制输入框、文本、编辑按钮状态
    thing.isEdit = false
    //判断一下
    if(!e.target.value.trim()) return alert('输入不能为空！')
    this.$bus.$emit('updateThing',thing.id,e.target.value)
    }
}
>>>>>>> 7bc8949 (bin update function)
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
