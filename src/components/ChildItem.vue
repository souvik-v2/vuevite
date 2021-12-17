<template>
  <div class="item-left" v-if="newItems.flag">
    <button class="button" @click.prevent="sideToggle(newItems.id)">+</button>
    {{ newItems.name }}
  </div>
  <div class="item-right" v-if="!newItems.flag">
    <button class="button btn" @click.prevent="sideToggle(newItems.id)">
      -
    </button>
    {{ newItems.name }}
  </div>
</template>
<script>
import { ref } from "vue";
export default {
  name: "Child",
  props: ["items"],
  emits: ["updateitems"],
  setup(props, { emit }) {
    var newItems = ref({ ...props.items });
    //console.log("items", newItems.value);

    const sideToggle = (id) => {
      if (newItems.value.id === id) newItems.value.flag = !newItems.value.flag;
      emit("updateitems", id);
    };

    return {
      newItems,
      sideToggle,
    };
  },
};
</script>
