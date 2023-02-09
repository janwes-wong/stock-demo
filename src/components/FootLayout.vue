<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已出库 {{ complateCount }}</span> / 全部 {{ total }}
    </span>
    <button class="btn btn-warning" @click="clearAll">清除已出库商品</button>
  </div>
</template>

<script>
export default {
  name: "Foot",
  props: ["itemInfos", "checkAllItems", "removeItems"],
  computed: {
    // 全部
    total() {
      return this.itemInfos.length;
    },
    // 已出库的数量
    complateCount() {
      return this.itemInfos.reduce((pre, item) => {
        return pre + (item.complate ? 1 : 0);
      }, 0);
    },
    // 判断是否勾选全部
    isAll: {
      get() {
        return this.complateCount === this.total && this.total > 0;
      },
      set(value) {
        this.checkAllItems(value);
      },
    },
  },
  methods: {
    clearAll() {
      this.removeItems();
    },
  },
};
</script>

<style scoped>
/* footer */
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
