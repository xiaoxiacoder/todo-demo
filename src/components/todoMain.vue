<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{completed:item.isDone}" v-for="item in list" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone"/>
        <label >{{item.name}}</label>
        <button class="destroy" @click="deleteFn(item.id)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
export default {
    props:["list"],
    methods:{
      deleteFn(itemId){
        this.$emit("deleteContent",itemId)
      }
    }
}
</script>