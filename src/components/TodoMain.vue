<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{completed:item.isDone}" v-for="(item,i) in todoList" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox"  v-model="item.isDone" />
        <label>{{ item.name }}
          <span id="time">{{ item.time | formatDate }}</span>
        </label>
        <button class="destroy" @click="btnDel(item.id,item.isDone)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
  import moment from 'moment'
export default {
  props: ['todoList'],
  data() {
    return {
      checke: [],
      active:false
    }
  },
  methods: {
    btnDel(theId, isDone) {
      this.$emit('DelList',theId,isDone)
    }
  },
  filters: {
    formatDate(val) {
    return moment(val).format('YYYY-MM-DD HH:mm:ss')
  }
 }
}
</script>
<style scoped lang="less">
#time {
  font-size: 12px;
  float: right;
  margin-top: 20px;
  color: #ccc;
}
</style>