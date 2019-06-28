<template>
    <ul class="todo-main">                                                                 <!-- 23:把删除方法帮给item -->       <!-- 34：给item绑定被选中的对象的方法 -->
        <Item v-for="(todo,index) in todos" :key = "todo.id" :index = "index" :todo="todo" :deleteTodo="deleteTodo" :toggleTodo="toggleTodo"/><!-- 4:todos传过来了，就可以在此组件中使用了，因为要动态生成多个item，所以要用遍历，最好给每一个todo加上key -->
        <!-- 5: todo是每一个item的数据，需要在item组件中显示，那么又涉及到了传参，此时吧todo这个数据强制绑定给todo这个属性上，然后再去item组件中用props接参 -->
      </ul>
</template>

<script>
import Item from './Item.vue'
export default {
  //3: props负责通信:只要在当前的组件中,使用props:['todos']--此时这个组件中就可以直接使用todos这个属性了
    props:["todos","deleteTodo","toggleTodo"],// 22:接收一下删除的方法，再绑定到item传给item
    components:{                  // 33:接收被选中的对象的方法，再传给item
        Item
    }
}
</script>


<style scoped>
    .todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>

