<template>
  <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/><!-- 14：绑定数据，title为动态展示的属性 ，绑定键盘事件，触发add这个方法-->
      </div>
</template>

<script>
export default {
  //12:props接收从App中传过来的添加的方法，那么在这个组件中就可以用这个方法了
  props:{
    addTodo:{
      type:Function,
      required:true
    }
  },
  data () {//13:一开始title中的数据为空，当按下回车键的时候动态添加到数据中
   return {
     title:'',

   }
  },
  methods:{
    add(){
      const title = this.title.trim()//15:按下回车后触发add，获取到用户输入的信息
      //先判断是否有数据 ①(如果没有数据就直接return)
      if(!title){
        return
      }
      //创建一个todo对象
      const todo = {
        id:Date.now(),
        title,
        isShow:false
      }
      //②：有数据那么就调用addTodo这个方法，把我创建的todo对象传进去   接下来去item做鼠标移入高亮效果
      this.addTodo(todo)
      this.title = ''
    }
  },

  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
