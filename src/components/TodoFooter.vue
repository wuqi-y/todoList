<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>数量值{{ todoList.length }}</strong></span>
    <ul class="filters" @click="getSel">
      <li>
        <a :class=" isSel=='all' ? 'selected' : '' " href="javascript:;" @click="isSel = 'all'" >全部</a>
      </li>
      <li>
        <a :class=" isSel=='no' ? 'selected' : '' "  href="javascript:;" @click="isSel = 'no'" >未完成</a>
      </li>
      <li>
        <a :class=" isSel=='yes' ? 'selected' : '' "  href="javascript:;" @click="isSel = 'yes'"  >已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="delYes">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ['todoList'],
  data() {
    return {
      isSel:'all'
    }
  },
  methods: {
    getSel() {
      this.$emit('getSel',this.isSel)
    },
    delYes() {
      this.$emit('getdelDone')
    }
  }
}
</script>