<template>
  <div id="app">
    <SelectList v-model="selectedListItems" :list="list" />
    <p>{{ selectedListItems }}</p>
  </div>
</template>

<script>
import SelectList from './components/SelectList.vue';

export default {
  name: 'App',
  components: {
    SelectList,
  },
  data() {
    return {
      selectedListItems: [],
      list: ['apple', 'apple', 'pear', 'banana'],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
