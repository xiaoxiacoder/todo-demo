<template>
  <section class="todoapp">
    <!-- 使用组件 -->
    <todo-header :list="showArr" @addContent="add"></todo-header>
    <todo-main :list="showArr" @deleteContent="del"></todo-main>
    <todo-footer :list="showArr" @changeType="typeFn" @clear="clearFn"></todo-footer>
  </section>
</template>

<script>
//引入组件
import todoHeader from "./components/todoHeader.vue";
import todoMain from "./components/todoMain.vue";
import todoFooter from "./components/todoFooter.vue";
//引入样式
import "./styles/base.css";
import "./styles/index.css";
export default {
  //注册组件
  components: {
    todoHeader,
    todoMain,
    todoFooter
  },
  data() {
    return {
      // list: [
      //   { id: 100, name: "吃饭", isDone: true },
      //   { id: 201, name: "睡觉", isDone: false },
      //   { id: 103, name: "打豆豆", isDone: true }
      // ],
      list:JSON.parse(localStorage.getItem('setList')) || [],//从本地取值
      //默认显示全部
      getSel:'all'
    };
  },
  methods: {
    add(contentName) {
      let id = this.list.length === 0 ? 100 : (this.list.length - 1).id + 1;
      this.list.push({
        id: id,
        name: contentName,
        isDone: false
      });
    },
    del(id){
      let index = this.list.findIndex(item => item.id === id)
      this.list.splice(index,1)
    },
    
    typeFn(isSel){
      this.getSel = isSel //接收子组件传来的值
    },

    clearFn(){
      this.list = this.list.filter(item => item.isDone === false)
    }
  },

  computed:{
    //根据状态来决定显示什么样的数组
    showArr(){
      if(this.getSel === 'yes'){
          //显示完成了的
          return this.list.filter(item => item.isDone === true)
      }else if(this.getSel === 'no'){
        //显示没完成的
        return this.list.filter(item => item.isDone === false)
      }else{
        return this.list //显示全部
      }

    }
  },

  //侦听器
  watch:{
    list:{//侦听数组的变化
      deep:true,//深度侦听
      handler(){//变化后触发该方法
        localStorage.setItem('setList',JSON.stringify(this.list))//存入本地

      }
    }
  }
};
</script>

<style>
</style>