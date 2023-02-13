<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="itemObj.complate"
        @change="handleCheck(itemObj.id)"
      />
      <span v-show="!itemObj.editFlag">{{ itemObj.title }}</span>
      <input
        type="text"
        v-show="itemObj.editFlag"
        :value="itemObj.title"
        @blur="handleBlur(itemObj, $event)"
      />
    </label>
    <button class="btn btn-warning" @click="handleDelete(itemObj.id)">
      删除
    </button>
    <button class="btn btn-edit" @click="handleEdit(itemObj)">编辑</button>
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
    // 编辑商品信息
    handleEdit(itemObj) {
      if (itemObj.editFlag === undefined) {
        itemObj.editFlag = true;
        console.log(itemObj);
      } else {
        this.$set(itemObj, "editFlag", true);
      }
    },
    // 失去焦点
    handleBlur(itemObj, event) {
      itemObj.editFlag = false;
      this.$bus.$emit("updateItem", itemObj.id, event.target.value);
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
