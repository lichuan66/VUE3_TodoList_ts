<template>
  <index></index>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Index from "./components/Index.vue";
import "./assets/style/test.less";

export default defineComponent({
  name: "App",
  components: {
    Index,
  },
});
</script>
