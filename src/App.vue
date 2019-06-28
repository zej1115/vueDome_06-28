<template>
<div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo = "addTodo"/><!-- 11:把添加的方法强制绑定到addTodo这个属性上，Header组件props接数据 -->
      <List :todos = "todos" :deleteTodo="deleteTodo" :toggleTodo="toggleTodo"/><!-- 2: 把todos数据强制绑定给list，然后去list组件中用props接一下 -->
      <Footer :todos="todos"/>      <!-- 21:给list绑定删除的方法，再传给item -->      <!-- 32被选中的对象的方法传给list -->
    </div><!-- 37:todo选中的状态传给footer -->
  </div>
  
</template>

<script>
import Header from './components/Header'
import List from './components/List'
import Footer from './components/Footer'

export default {

  components: {
    Header,
    List,
    Footer
  },
  data () {
   return {
     //1：静态显示数据，isShow为布尔值，此时item需要这个数据，那么app要通过list传给item
     todos:[
       {id:1,title:"奔驰",isShow:false },
       {id:2,title:"宝马",isShow:true },
       {id:3,title:"奥拓",isShow:false },
       {id:4,title:"帕萨特",isShow:false },
     ]

   }
  },// 9: 分析按下回车添加数据到什么位置，最终添加到了todos这个数据中，所以方法也要写在App中
  methods:{
    addTodo (todo){
      this.todos.unshift(todo);// 10: 把传过来的todo对象插入到todos这个数据数组中，这个数据header需要，又涉及到了通信
    },
    deleteTodo(index){//利用index删除当前的一个数据。给list绑定这个方法，传给list
    this.todos.splice(index,1);
  },
  toggleTodo(todo){// 31 切换这个被选中的对象的方法
    todo.isShow = !todo.isShow//传给list再传给item
  }
  },// 20: 所有数据都在App中，在这里定义删除的函数，通过list传给item

  
}
</script>

<style scoped>



.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

</style>
