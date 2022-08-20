<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{list.length}}</strong></span>
    <ul class="filters" @click="fn">
      <li>
        <a :class="{selected:isSel === 'all'}" href="javascript:;" @click="isSel='all'">全部</a>
      </li>
      <li>
        <a :class="{selected:isSel === 'no'}" href="javascript:;" @click="isSel='no'">未完成</a>
      </li>
      <li>
        <a :class="{selected:isSel === 'yes'}" href="javascript:;" @click="isSel='yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed"  @click="delYes">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props:["list"],
  data(){
    return{
      isSel:"all",//全部all,已完成yes,未完成no
    }
  },
  methods:{
    fn(){
      //把类型字符串isSel传给父
      this.$emit("changeType",this.isSel)
    },
    delYes(){
      this.$emit('clear')
    }
  }
}
</script>