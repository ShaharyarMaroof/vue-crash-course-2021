<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-show="isOnHomePage"
      @btn-click="$emit('toggle-add-task')"
      :label="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  emits: ["toggle-add-task"],
  computed: {
    isOnHomePage() {
      return this.$route.path === "/" ? true : false;
    },
  },
};
</script>

<style scoped lang='scss'>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
