<template>
  <div id="shopping-list">
    <div>
      <h1>{{header || 'Welcome'}}</h1>
      <button v-if="editing" class="btn btn-cancel" @click="doEdit(false)">Cancel</button>
      <button v-else class="btn btn-primry" @click="doEdit(true)">Add</button>
    </div>
    <div class="add-item-form" v-if="editing">
      <input 
      @keyup.enter="saveItem"
      type="text" v-model="newItem" placeholder="Add an Item">
      <label>
        <p>{{characterCount}}{{"/200"}}</p>
        <input 
        type="checkbox" v-model="newItemHighPriority">
        High Priority
      </label>
      <button 
          v-bind:disabled="newItem.length === 0"
          @click="saveItem"
          class="btn btn-primary">
          Save Item
      </button>
    </div>
    <p v-if="items.length === 0">Nice job! You bought all your items</p>
    <ul v-else>
      <li 
      @click="togglePurchased(item)"
      v-for="item in items" :key="item.id" :class="{strikeout: item.purchased}">{{item.value}}</li>
    </ul>
  </div>
</template>

<script>
import $ from "jquery";
window.jQuery = window.$ = $;
require('bootstrap');
export default {
  name: 'HelloWorld',
  data(){
    return {
    header: 'Shopping List App',
    editing: false,
    newItemHighPriority: false,
    iceCreamFlavor:['Vanilla', 'Strawberries','Shinkurt'],
    chosenOnes:[],
    items: [
      {id:0, value:'Hallo und tshuss', purchased: true, highPriority: true},
      {id:1, value:'mitbewohner', purchased: true, highPriority: false},
      {id:2, value:'milch mit kase', purchased: false, highPriority: true}
    ],
    newItem:''
    };
  },
  props: {
    msg: String
  },
  methods:{
    saveItem(){
      this.items.push({id: this.items.length + 1, value: this.newItem,highPriority: this.newItemHighPriority});
      this.newItem='';
    },
    doEdit(editing){
      this.editing= editing;
      this.newItem="";
    },
    togglePurchased(item){
      item.purchased= !item.purchased;
    }
  },
  computed:{
    characterCount(){
      return this.newItem.length;
    },
    reversedItems(){
      return [...this.items].reverse();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
