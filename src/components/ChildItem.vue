<template>
  <div class="child" v-for="item in newItems" :key="item.id">
    <div class="item-left" v-if="item.flag">
      <button
        class="button"
        @click.prevent="sideToggle(item.id)"
      >+</button>
      {{ item.name }} - {{ item.flag ? "Available" : "Selected" }}
    </div>
    <div class="item-right" v-if="!item.flag">
      <button
        class="button btn"
        @click.prevent="sideToggle(item.id)"
      >-</button>
      {{ item.name }} - {{ item.flag ? "Available" : "Selected" }}
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
export default {
  name: "Child",
  props: ["availableItems", "selectedItems"],
  emits: ["updateitems"],
  setup(props, { emit }) {
    var availableItems = ref([...props.availableItems]);
    var selectedItems = ref([...props.selectedItems]);
    var newItems = ref();
    //console.log("items", newItems.value);
    newItems.value = [...availableItems.value, ...selectedItems.value];

    const sideToggle = (id) => {
      let index = newItems.value.findIndex((i) => i.id === id);
      newItems.value[index].flag = !newItems.value[index].flag;
      emit("updateitems", id);
    };

    return {
      newItems,
      sideToggle,
    };
  },
};
</script>
