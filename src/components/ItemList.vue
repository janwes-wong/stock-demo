<template>
  <ul class="todo-main">
    <Item
      v-for="itemObj in itemInfos"
      :key="itemObj.id"
      :itemObj="itemObj"
      :checkItem="checkItem"
      :deleteItem="deleteItem"
    />
  </ul>
</template>

<script>
import Item from "./Item.vue";

export default {
  name: "ItemList",
  components: { Item },
  props: ["itemInfos", "checkItem", "deleteItem"],
};
</script>

<style scoped>
/* main */
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
