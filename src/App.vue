<template>
  <div id="app">
    <TransferList
      v-model="activeListItems"
      :list="list"
      @update-List="updateList"
    />
  </div>
</template>

<script>
import TransferList from './components/TransferList.vue';

export default {
  name: 'App',
  components: {
    TransferList,
  },
  data() {
    return {
      activeListItems: ['pear'],
      list: ['apple', 'pear', 'banana'],
    };
  },
  methods: {
    updateList(val) {
      this.list = val;
    },
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
