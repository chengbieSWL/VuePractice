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
 import storage from './model/storage.js';

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
       storage.set('list',this.list);//缓存
    },
    removeDate(key){
      this.list.splice(key,1);
       storage.set('list',this.list);
    },
    saveList(){
       storage.set('list',this.list);
    }
  },
  mounted(){//生命周期函数
    var list = storage.get('list');
    if(list){
      this.list = list; 
    }
  }
}
</script>

<style>

</style>
