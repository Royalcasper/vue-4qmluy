<template>
  <div v-for="(item, index) in list">
    <p>{{ item }}</p>
    <input
      type="checkbox"
      :value="item"
      :id="index"
      v-model="internalModelValue"
    />
  </div>
</template>

<script>
export default {
  name: 'SelectList',
  props: {
    list: Array,
    modelValue: Array,
  },
  computed: {
    internalModelValue: {
      get() {
        return this.modelValue;
      },
      set(val) {
        this.$emit('update:modelValue', val);
      },
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
