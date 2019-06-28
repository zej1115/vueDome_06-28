<template> <!-- 16：强制绑定style属性动态设置li的背景颜色和字体颜色 -->
    <li :style="{backgroundColor:bgColor, color:fontColor}"
    @mouseenter="HandleMouse(true)"
    @mouseleave="HandleMouse(false)"><!-- 18:绑定鼠标移入移出事件，这个没有冒泡 -->
        <label>                   <!-- 29：为了避免子组件直接操作父组件 -->
        <input type="checkbox" v-model="isCompleted"/><!-- 8:绑定数据，用传过来todo对象中的isShow做默认勾选框显示 在App中做添加的方法 -->
        <span>{{todo.title}}</span><!-- 7：动态显示传过来todo中title的值 -->
        </label>                                         <!-- 25:给删除按钮绑定点击事件 -->
        <button class="btn btn-danger" v-show="isDisplay" @click ="del">删除</button>
    </li>
</template>

<script>
export default {
  // 6：从list传过来一个对象，这里props接参要用对象的形式
  props:{
    todo:Object,
    deleteTodo:Function,// 24:接收下从list传过来删除的方法
    index:Number,// 27:配置下inde是是类型
    toggleTodo:Function //35: 配置被选中的对象的方法
  },// 17：动态设置
  data () {
   return {
     isDisplay:false,
     bgColor:"white",
     fontColor:"red",
     
   }
  },
  methods:{// 19：触发这个函数：判断鼠标移入还是移出
    
    HandleMouse(isEnter){
      if(isEnter){
        this.bgColor = "pink";
        this.fontColor ="green";
        this.isDisplay = true
      }else{
        this.bgColor = "white";
        this.fontColor ="black";
        this.isDisplay = false
      }     
    },
    del(){ //28: 删除
      if(confirm('确定吗')){
        //console.log(index)
        this.deleteTodo(this.index)

      }

    },
     
  },
  computed:{//30:操作属性：是否完成这个方法的读取和设置方法
      isCompleted:{
        get(){
          return this.todo.isShow//返回读取到的数据对象是否被选中的
        },
        set(val){//36：设置是否被选中就需要传val
           this.toggleTodo(this.todo)
        }
      }
    } 
}
</script>


 

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  /* display: none; */
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

</style>
