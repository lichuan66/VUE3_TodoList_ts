<template>
  <header>
    <h1 class="main-header">TodoList</h1>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "MainHeader",
});
</script>

<style lang="less" scoped>
h1.main-header {
  margin: 20px;
  font-size: 100px;
  font-weight: 100;
  color: rgb(252, 157, 154);
  text-align: center;
}
</style>
