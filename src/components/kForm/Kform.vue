<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  provide() {},
  props: {
    rules: Object,
    model: {
      type: Object,
      required: true,
    },
  },
  methods: {
    validate(cb) {
      let task = this.$children.map((item) => {
        item.validate();
      });
      Promise.all(task).then(() => cb(true));
    },
  },
};
</script>

<style lang="scss" scoped>
</style>