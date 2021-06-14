<template>
  <button @click="onClickHandler()" :style="{ background: color }" class="btn">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    label: String,
    color: String,
    // onClickHandler: {
    //   type: Function,
    //   default: () => console.log(`no handler attached ${this.props.label}`),
    // },
  },
  methods: {
    onClickHandler() {
      console.log(`button clicked`);
    },
  },
};
</script>
