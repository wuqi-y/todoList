<template>
  <header class="header todoapp">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model.trim="todoStr"
      @keydown.enter="TodoAdd"
    />
  </header>
</template>

<script>
export default {
  props:['todoList'],
  data() {
    return {
      todoStr:''
    }
  },
  methods: {
    TodoAdd() {
      if (this.todoStr == '') {
        return alert('请输入有效内容！')
      }
      this.$emit('todoAdd', this.todoStr)
      this.todoStr = ''
    }
  },
  computed: {
    isAll:{
      set(val) {
        this.todoList.forEach(item => item.isDone = val)
      },
       get() {
      return this.todoList.length !== 0 && this.todoList.every(item => item.isDone === true)
      },
    }
 }
}
</script>