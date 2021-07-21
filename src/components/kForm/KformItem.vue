<template>
  <div>
    <label v-if="label"></label>
    <slot></slot>
  </div>
</template>

<script>
import Schema from "async-validator";
export default {
  invide: ["form"],
  props: {
    label: {
      type: String,
      default: "",
    },
    prop: {
      type: String,
      default: "",
    },
  },
  mounted() {
    this.$on("validated", () => {
      this.validated();
    });
  },
  methods: {
    validated() {
      let rules = this.form.rules[this.prop];
      let value = this.form.model[this.prop];

      let validator = new Schema({ [this.prop]: rules });
      return new Promise((resolve, reject) => {
        validator.validate({ [this.prop]: rules }, (errors) => {
          if (errors) {
            this.errors = errors[0].message;
            reject();
          } else {
            this.errors = "";
            resolve();
          }
        });
      });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>