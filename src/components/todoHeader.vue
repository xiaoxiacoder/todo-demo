<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox"  v-model="isAll">
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="enterFn"
      v-model="content"
    />
  </header>
</template>

<script>
export default {
    props:["list"],
    data(){
        return{
            content:""
        }
    },

    methods:{
        enterFn(){
            //判断是否为空
            if(this.content.trim().length === 0){
                alert('请输入内容')
                return
            }
            //不为空，执行父组件的自定义事件
            this.$emit('addContent',this.content)  
            //添加后把输入框清空
            this.content =""
        },

        
    },

    computed:{
        isAll:{
            set(checked){
                // console.log(checked);
                this.list.forEach(item => item.isDone =checked)
            },
            get(){
                return this.list.length !== 0 && this.list.every(item => item.isDone ===true)
            }
        }
    }
 
}
</script>