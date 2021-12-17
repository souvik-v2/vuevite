<template>
  <h3>Items from Child</h3>
  <hr />
  <div class="item-left">
    <h4>Available Item</h4>
    <ul>
      <li v-for="item in availableItem" :key="item.id">
        <button class="button" @click.prevent="sideToggle(item.id)">
          +
        </button>
        {{ item.name }}
      </li>
    </ul>
  </div>
  <div class="item-right">
    <h4>Selected Item</h4>
    <ul>
      <li v-for="item in selectedItem" :key="item.id">
        <button
          class="button btn"
          @click.prevent="sideToggle(item.id, item.flag)"
        >
          -
        </button>
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>
<script>
import { ref } from "vue";
export default {
  name: "Item",
  props: {
    items: {
      type: Array,
    },
  },
  emits: ["updateitems"],
  setup(props, { emit }) {
    var newItems = ref(props.items);
    console.log("items", newItems.value);

    const availableItem = ref([]);
    const selectedItem = ref([]);

    const diffArray = () => {
      availableItem.value = newItems.value.filter((i) => i.flag);
      selectedItem.value = newItems.value.filter((i) => !i.flag);
    };
    diffArray();

    const sideToggle = (id) => {
      let index = newItems.value.findIndex((item) => item.id === id);
      //console.log(index);
      newItems.value[index].flag = !newItems.value[index].flag;
      diffArray();
      emit("updateitems", id);
    };

    return {
      newItems,
      sideToggle,
      availableItem,
      selectedItem,
    };
  },
};
</script>
