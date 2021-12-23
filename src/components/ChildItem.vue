<template>
  <div class="head">
    <div class="left">{{ availableItemsLabel }}</div>
    <div class="right">{{ selectedItemsLabel }}</div>
  </div>
  <div class="item-left">
    <ul>
      <li v-for="item in availableItems" :key="item.id">
        <button
          class="button"
          @click.prevent="sideToggle(item.id, 'available')"
        >
          +
        </button>
        {{ item.name }}
      </li>
    </ul>
  </div>
  <div class="item-right">
    <ul>
      <li v-for="item in selectedItems" :key="item.id">
        <button
          class="button btn"
          @click.prevent="sideToggle(item.id, 'selected')"
        >
          -
        </button>
        {{ item.name }}
      </li>
    </ul>
  </div>
  <button class="cns" @click="updateParent">Console in Parent</button>
</template>
<script>
import { ref } from "vue";
export default {
  name: "Child",
  props: ["availableItemsLabel", "selectedItemsLabel", "availableItems", "selectedItems"],
  emits: ["updateAvailableItems", "updateSelectedItems"],
  setup(props, { emit }) {
    var availableItemsLabel = ref(props.availableItemsLabel);
    var selectedItemsLabel = ref(props.selectedItemsLabel);
    var availableItems = ref(props.availableItems);
    var selectedItems = ref(props.selectedItems);

    const sideToggle = (id, name) => {
      if (name === "available") {
        selectedItems.value.push(availableItems.value.find((i) => i.id === id));
        availableItems.value = availableItems.value.filter((i) => i.id !== id);
      } else {
        availableItems.value.push(selectedItems.value.find((i) => i.id === id));
        selectedItems.value = selectedItems.value.filter((i) => i.id !== id);
      }
    };

    const updateParent = () => {
      emit("updateAvailableItems", availableItems.value);
      emit("updateSelectedItems", selectedItems.value);
    };

    return {
      availableItemsLabel,
      selectedItemsLabel,
      availableItems,
      selectedItems,
      sideToggle,
      updateParent,
    };
  },
};
</script>
