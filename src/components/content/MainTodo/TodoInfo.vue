<template>
  <div :class="['todo-info', completed ? 'completed' : '']">
    <input
      type="checkbox"
      class="input"
      v-model="completed"
      @click="changeCom"
    />
    <label for="content" class="content">{{ props.msg.content }}</label>
    <button class="delete" @click="delItem">X</button>
  </div>
</template>


<script setup lang="ts">
import { arrData, bodyData } from "../../../type/index";
import { ref, defineProps, defineEmits } from "vue";
interface Props {
  msg: arrData;
}

const props = defineProps<Props>();
console.log(props);

const emit = defineEmits(["del", "chanCom"]);
let completed = ref(props.msg.completed);

function delItem(): void {
  emit("del", props.msg.id);
}

function changeCom(): void {
  const body: bodyData = {
    id: props.msg.id,
    completed: !completed.value,
  };
  emit("chanCom", body);
}
</script>

<style lang="less" scoped>
.todo-info {
  font-size: 24px;
  padding: 10px;
  display: flex;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  .input {
    width: 50px;
    height: 30px;
  }
  .content {
    flex: 1;
  }
  .delete {
    width: 40px;
    border: none;
    background-color: #fff;
    color: rgb(252, 157, 154);
    font-size: 24px;
    cursor: pointer;
    display: none;
  }
}
.todo-info:hover .delete {
  display: block;
}
.completed .content {
  text-decoration: line-through;
}
</style>