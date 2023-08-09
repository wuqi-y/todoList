<template>
  <div>
    <TodoHeader
    @todoAdd="add"
    :todoList="todoList"
    ></TodoHeader>

    <TodoMain
    :todoList="showArr"
    @DelList="del"
    ></TodoMain>

    <TodoFooter
    :todoList="showArr"
    @getSel="isSel"
    @getdelDone="delDone"
    ></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoMain from './components/TodoMain.vue';
import TodoFooter from './components/TodoFooter.vue';
// 样式引入
import './styles/base.css'
import './styles/index.css'
export default {
  components: {
    TodoHeader, TodoMain, TodoFooter
  },
  data() {
    return {
      // todoList: [
      //   { id: 100, name: "吃饭", isDone: true },
      //   { id: 101, name: "睡觉", isDone: false },
      //   { id: 102, name: "打豆豆", isDone: true },
      // ],
      todoList: JSON.parse(localStorage.getItem('todoList')) || [],
      getSel :'all'
    }
  },
  methods: {
    // 添加待办
    add(item) {
      console.log('ojojojojo')
      console.log('111')
      let id = this.todoList.length === 0 ? 100 : this.todoList[this.todoList.length - 1].id + 1
      this.todoList.push({
        id:id,
        name: item,
        isDone: false,
        time:new Date()
      })
    },
    // 判断状态
    isSel(str) {
      this.getSel = str
    },
    // 删除待办
    del(theId,isDone) {
      let index = this.todoList.findIndex(obj => obj.id === theId)
      if (!isDone) {
        if (confirm('你还没有完成待办，确认删除？')) {
          this.todoList.splice(index, 1)
       }
      } else {
        this.todoList.splice(index,1)
      }
    },
    // 删除已完成待办
    delDone() {
      this.todoList.forEach((item,i) => {
        if (item.isDone === true) {
          this.todoList.splice(i,1)
        }
     })
    }
  },
  computed: {
    showArr() {
      if (this.getSel === 'no') {
         return this.todoList.filter(item => {
         return item.isDone === false
        })
      }else if (this.getSel === 'yes') {
         return  this.todoList.filter(item => {
         return item.isDone === true
        })
      } else {
        return this.todoList
      }
    }
  },
  watch: {
    todoList: {
      handler() {
        localStorage.setItem('todoList',JSON.stringify(this.todoList))
      },
      deep:true
    }
  }
}
</script>

<style>

</style>
