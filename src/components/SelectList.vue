<template>
  <div class="checkboxList">
    <div class="totalItems">
      <input
        type="checkbox"
        :value="list"
        id="selectAll"
        v-model="allSelected"
      />
      <label> {{ list.length }} items</label>
    </div>
    <div v-for="(item, index) in list">
      <input
        type="checkbox"
        :value="item"
        :id="index"
        v-model="internalModelValue"
      />
      <label>{{ item }}</label>
    </div>
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
    allSelected: {
      get() {},
      set(val) {},
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  margin-top: 8px;
}
.checkboxList {
  width: 150px;
  height: 80px;
  overflow: scroll;
  overflow-x: hidden;
  border: 2px solid black;
}
.totalItems {
  border-bottom: 2px solid black;
}
</style>
