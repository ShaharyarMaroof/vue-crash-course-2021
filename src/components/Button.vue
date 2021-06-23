<template>
  <button
    @click="$emit('btn-click')"
    :style="{ background: color }"
    class="btn"
  >
    {{ label }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    label: String,
    color: String,
  },
  emits: ["btn-click"],
};
</script>
