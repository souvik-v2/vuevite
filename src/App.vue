<template>
<div class="main">
  <h3>List of Items From Parent</h3>
  <ul>
      <li v-for="item in items" :key="item.id">
        {{ item.id }}# {{ item.name }} - [{{item.flag ? 'Avilable' : 'Selected'}}]
      </li>
    </ul>
</div>
<h3>Items From Child</h3>
<hr>
<div class="head">
  <div class="left">Available Item</div>
  <div class="right">Selected Item</div>
</div>
  <div class="grid-container">
    <div v-for="item in items" :key="item.id" class="dynamic">
      <Child :items="item" @updateitems="updateitems" />
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
import Child from "./components/ChildItem.vue";
export default {
  name: "App",
  components: {
    Child
  },
  setup() {
    var items = ref([
      { id: 1, name: "Item1", flag: true },
      { id: 2, name: "Item2", flag: false },
      { id: 3, name: "Item3", flag: true },
      { id: 4, name: "Item4", flag: false },
      { id: 5, name: "Item5", flag: true },
      { id: 6, name: "Item6", flag: false },
      { id: 7, name: "Item7", flag: false },
    ]);

    const updateitems = (childItems) => {
      let index = items.value.find((item) => item.id === childItems);
      index.flag = !index.flag;
      console.log('Parent Items Updated:', items.value);
    };

    return {
      items,
      updateitems,
    };
  },
};
</script>
<style>
li {
    list-style: none;
    border-bottom: 1px solid #4caf50;
    padding: 2px 0;
}
.head {
  display: grid;
  grid-template-columns: auto auto;
  text-align: center;
  font-size: 16px;
  font-weight: 700;
}
h3 {
  text-align: center;
}
.grid-container {
  display: block;
}
.item-right {
  float: right;
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  font-size: 30px;
  text-align: center;
  width: 50%;
  margin-bottom: 10px;
  clear: right;
}
.item-left {
  float: left;
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  font-size: 30px;
  text-align: center;
  width: 47%;
  margin-bottom: 10px;
  clear: left;
}
.button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 0 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 25px;
  cursor: pointer;
}
.btn {
  background-color: #f44336;
}
</style>
