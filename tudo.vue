<template>
  <div id="app">
    <input type="text" v-model="todo">
    <button @click="doAdd()">增加</button>

    <h3>未完成</h3>
    <ul>
      <li v-for="(item,key) in list" :key="key" v-if="!item.checked">
        <input type="checkbox" v-model="item.checked" @change="saveList()">{{item.title}}<button @click="removeDate(key)">删除</button>
      </li>
    </ul>

    <h3>已完成</h3>
    <ul>
      <li v-for="(item,key) in list" :key="key" v-if="item.checked">
        <input type="checkbox" v-model="item.checked" @change="saveList()">{{item.title}}<button @click="removeDate(key)">删除</button>
      </li>
    </ul>


  </div>
</template>

<script>
/** 
 ['jajaj','hfkjd']


 [
   {
     title:'haha',
     checked:true
   },
   {
     title:'enneen',
     checked:false
   }
 ]
 
 
 */

export default {
  data(){
    return{
      todo:'',
      list:[
        {
          title:'haha',
          checked:true
        },
        {
          title:'enneen',
          checked:false
        }
      ]
    }
  },
  methods:{
    doAdd(){
      this.list.push({
        title:this.todo,
        checked:false});

      this.todo = '';
       localStorage.setItem('list',JSON.stringify(this.list))//缓存
    },
    removeDate(key){
      this.list.splice(key,1);
       localStorage.setItem('list',JSON.stringify(this.list))
    },
    saveList(){
      localStorage.setItem('list',JSON.stringify(this.list))
    }
  },
  mounted(){//生命周期函数
    var list = JSON.parse(localStorage.getItem('list'));
    if(list){
      this.list = list; 
    }
  }
}
</script>

<style>

</style>
