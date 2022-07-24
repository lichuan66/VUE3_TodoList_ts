<template>
  <div class="todo-item">
    <span class="total">{{ msg }} Item left</span>
    <div class="tabs">
      <a
        class="a"
        v-for="(item, index) in states"
        :key="index"
        :class="state === item ? 'active' : ''"
        @click="
          state = item;
          changeState();
        "
        >{{ item }}</a
      >
    </div>
    <button class="clear" @click="deleteCom">Clear completed</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "TodoItem",
  props: {
    msg: Number,
  },
  setup(props, ctx) {
    let count = ref(0);
    const states = ref(["all", "active", "completed"]);
    let state = ref("all");

    function changeState(): void {
      ctx.emit("changeState", state.value);
    }

    function deleteCom(): void {
      ctx.emit("deleteCompleted");
    }

    return {
      count,
      states,
      state,
      changeState,
      deleteCom,
    };
  },
});
</script>

<style lang="less" scoped>
.todo-item {
  font-weight: 400;
  display: flex;
  justify-content: space-between;
  padding: 5px 10px;
  line-height: 30px;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  .total {
    color: rgb(254, 67, 101);
  }
  .tabs {
    display: flex;
    justify-content: space-between;
    width: 200px;
    .a {
      border: 1px solid rgb(252, 157, 154);
      border-radius: 5px;
      padding: 0 10px;
      cursor: pointer;
    }
    .active {
      background-color: rgb(252, 157, 154);
      color: #fff;
    }
  }
  .clear {
    background-color: green;
    color: #fff;
    padding: 0 10px;
    border-radius: 5px;
    border: none;
    cursor: pointer;
  }
}
</style>
