<template>
  <div class="todo-header">
    <!--  -->
    <input
      type="text"
      placeholder="请输入您的商品信息，按回车键确认"
      @keyup.enter="addItem"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";

export default {
  name: "HeaderLayout",
  props: ["receive"],
  methods: {
    // 添加商品信息
    addItem(event) {
      if (!event.target.value.trim()) return alert("请输入正确名称!");
      // 生成商品对象
      const itemObj = {
        id: nanoid(),
        title: event.target.value,
        complate: false,
      };
      // 将商品信息向App组件receive方法发送数据
      this.receive(itemObj);
      // 清空输入框数据
      event.target.value = "";
    },
  },
};
</script>

<style scoped>
/* header */
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px rgba(0, 0, 0blue, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
