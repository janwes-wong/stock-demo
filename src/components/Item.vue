<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="itemObj.complate"
        @change="handleCheck(itemObj.id)"
      />
      <span>{{ itemObj.title }}</span>
    </label>
    <button class="btn btn-warning" @click="handleDelete(itemObj.id)">
      删除
    </button>
  </li>
</template>

<script>
export default {
  name: "Item",
  props: ["itemObj", "checkItem", "deleteItem"],
  methods: {
    // 勾选或取消商品
    handleCheck(id) {
      this.checkItem(id);
    },
    // 删除商品
    handleDelete(id) {
      if (confirm("是否确定删除?")) {
        this.deleteItem(id);
      }
    },
  },
};
</script>

<style scoped>
/* item */
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>
