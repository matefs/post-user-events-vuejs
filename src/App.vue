<template>
  <div id='shopping-list'>
    <h1>{{ header.toUpperCase() ?? 'Welcome' }}</h1>
  


  <div class='add-item-form'>
 

<input type='text' v-model='newItem' placeholder="Add an item" @keyup.enter="addItemToItemsList(newItem)">
  
  <button
  @click="addItemToItemsList(newItem)"
  class="btn btn-primary"
  >Add item
  </button>

  </div>
  
  <ul>
    <li v-for="item in itemsList" :key='item.id'>{{item.label}}</li>
  </ul>


  <button @click='postItemsListObjectAsJson'>Update List</button>
  
  </div>
</template>

<script>
import axios from 'axios';
 

export default {
  name: 'App',
  data(){
    return {
      header: 'Shopping item list ',
      newItem: '',
      itemsList: [
      {id:1 , label: 'Milk'},
      {id:2 , label: 'Rice'},
      {id:3 , label: 'Beans'},
      ]
    }
  },
  methods:{
      addItemToItemsList: function(newItem){
        this.itemsList.push({id: this.itemsList.length + 1 , label: newItem})
        console.table(this.itemsList)
      },
      postItemsList : function(ItemsListJson){
        axios.post('https://mateus.requestcatcher.com/',ItemsListJson).then(response => console.log(response))
      },
      postItemsListObjectAsJson : function(){
        return this.postItemsList(JSON.stringify(this.itemsList))
      }
    }
   
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
