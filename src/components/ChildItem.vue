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
  props: ["items"],
  emits: ["updateitems"],
  setup(props, { emit }) {
    var newItems = ref([...props.items]);
    //console.log("items", newItems.value);

    const sideToggle = (id) => {
      let index = newItems.value.findIndex((i) => i.id === id);
      newItems.value[index].flag = !newItems.value[index].flag;
      //if (newItems.value.id === id) newItems.value.flag = !newItems.value.flag;
      emit("updateitems", id);
    };

    return {
      newItems,
      sideToggle,
    };
  },
};
</script>
