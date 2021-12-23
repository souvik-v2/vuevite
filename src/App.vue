<template>
  <div class="grid-container">
    <h3>Item List</h3>
    <hr>
    <Child
      availableItemsLabel="Available"
      selectedItemsLabel="Selected"
      :availableItems="availableItems"
      :selectedItems="selectedItems"
      @updateAvailableItems="updateAvailableItems"
      @updateSelectedItems="updateSelectedItems"
    />
  </div>
</template>
<script>
import { ref } from "vue";
import Child from "./components/ChildItem.vue";
export default {
  name: "App",
  components: {
    Child,
  },
  setup() {

    var availableItems = ref([
      { id: 1, name: "Item1" },
      { id: 2, name: "Item2" },
      { id: 3, name: "Item3" },
    ]);
    var selectedItems = ref([
      { id: 4, name: "Item4" },
      { id: 5, name: "Item5" },
      { id: 6, name: "Item6" },
      { id: 7, name: "Item7" },
    ]);

    const updateAvailableItems = (childItems) => {
      console.log(childItems, "Parent AvailableItems:", childItems);
    };
    const updateSelectedItems = (childItems) => {
      console.log(childItems, "Parent SelectedItems:", childItems);
    };

    return {
      availableItems,
      selectedItems,
      updateAvailableItems,
      updateSelectedItems,
    };
  },
};
</script>
<style>
.cns {
  width: 40%;
  height: 50px;
  margin: 0 25%;
  float: left;
  clear: both;
}
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
