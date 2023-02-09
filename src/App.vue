<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <!-- App的方法向下子组件传递 -->
        <HeaderLayout :receive="receive" />
        <ItemList
          :itemInfos="itemInfos"
          :checkItem="checkItem"
          :deleteItem="deleteItem"
        />
        <FootLayout
          :itemInfos="itemInfos"
          :checkAllItems="checkAllItems"
          :removeItems="removeItems"
        />
      </div>
    </div>
  </div>
</template>

<script>
import HeaderLayout from "./components/HeaderLayout.vue";
import ItemList from "./components/ItemList.vue";
import FootLayout from "./components/FootLayout.vue";

export default {
  name: "App",
  components: { HeaderLayout, ItemList, FootLayout },
  data() {
    return {
      // itemInfos: [
      //   { id: "A001", title: "徐福记沙琪玛", complate: false },
      //   { id: "A002", title: "好友酸辣凤爪", complate: true },
      //   { id: "A003", title: "燕塘酸牛奶", complate: false },
      // ],
      itemInfos: JSON.parse(localStorage.getItem("itemInfos")) || [], // 读取浏览器本地存储信息
    };
  },
  methods: {
    // 接收添加的商品信息
    receive(itemObj) {
      this.itemInfos.unshift(itemObj);
    },
    //  勾选或取消商品
    checkItem(id) {
      this.itemInfos.forEach((o) => {
        if (o.id === id) {
          o.complate = !o.complate;
        }
      });
    },
    // 删除商品信息
    deleteItem(id) {
      this.itemInfos = this.itemInfos.filter((o) => {
        return o.id !== id;
      });
    },
    // 勾选或取消全部商品
    checkAllItems(isCheck) {
      this.itemInfos.forEach((o) => {
        o.complate = isCheck;
      });
    },
    // 清除已出库商品
    removeItems() {
      this.itemInfos = this.itemInfos.filter((o) => {
        return !o.complate;
      });
    },
  },
  watch: {
    itemInfos: {
      deep: true,
      handler(value) {
        // 数据存储到浏览器本地
        localStorage.setItem("itemInfos", JSON.stringify(value));
      },
    },
  },
};
</script>

<style>
/* base */
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-right: 0;
  font-size: 14;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-warning {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-warning:hover {
  color: #ffff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
