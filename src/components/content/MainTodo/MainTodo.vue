<template>
  <div class="main-todo">
    <input
      type="text"
      class="add-todo"
      placeholder="what to do?"
      @keyup.enter="saveData"
      v-model="tempData"
    />
    <todo-info
      v-for="item in filterData"
      :key="item.id"
      :msg="item"
      @del="deleteItem"
      @chanCom="changeCom"
    ></todo-info>
    <todo-item
      :msg="filterData.length"
      @changeState="changeState"
      @deleteCompleted="deleteCompleted"
    ></todo-item>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import { arrData, bodyData } from "../../../type/index";
import TodoItem from "./TodoItem.vue";
import TodoInfo from "./TodoInfo.vue";
export default defineComponent({
  name: "MainTodo",
  components: {
    TodoItem,
    TodoInfo,
  },
  setup() {
    const filData = ref<arrData[]>([]);
    let tempData = ref("");
    let total = ref(0);
    let stateTodo = ref("all");

    function saveData(): void {
      total.value += 1;
      filData.value.push({
        content: `${tempData.value}`,
        id: `${total.value}`,
        completed: false,
      });
      tempData.value = "";
    }

    function deleteItem(id: string): void {
      filData.value.splice(
        filData.value.findIndex((item) => item.id === id),
        1
      );
    }

    function changeCom(body: bodyData): void {
      const index = filData.value.findIndex((item) => item.id === body.id);
      filData.value[index].completed = body.completed;
    }

    let filterData = computed(() => {
      switch (stateTodo.value) {
        case "all":
          return filData.value.filter((item) => item);
        case "active":
          return filData.value.filter((item) => item.completed == false);
        case "completed":
          return filData.value.filter((item) => item.completed == true);
        default:
          return [];
      }
    });

    function changeState(state: string): void {
      stateTodo.value = state;
    }

    function deleteCompleted(): void {
      filData.value = filData.value.filter((item) => item.completed === false);
    }

    return {
      filData,
      tempData,
      total,
      stateTodo,
      filterData,
      saveData,
      deleteItem,
      changeCom,
      changeState,
      deleteCompleted,
    };
  },
});
</script>

<style lang="less" scoped>
.main-todo {
  width: 600px;
  margin: 0 auto;
  background-color: #fff;
  box-shadow: 0 0 5px #666;
  .add-todo {
    width: 100%;
    font-size: 24px;
    padding: 16px 16px 16px 36px;
    box-sizing: border-box;
    border: none;
  }
}
</style>
