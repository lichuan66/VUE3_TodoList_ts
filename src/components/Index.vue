<template>
  <div>
    <main-header></main-header>
    <main-todo></main-todo>
  </div>
</template>

<script lang="ts">
import MainHeader from "./content/MainHeader.vue";
import MainTodo from "./content/MainTodo/MainTodo.vue";
import { defineComponent } from "vue";
export default defineComponent({
  name: "Index",
  components: {
    MainHeader,
    MainTodo,
  },
});
</script>
