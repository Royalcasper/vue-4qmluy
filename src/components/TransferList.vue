<template>
  <div class="transferListContainer">
    <SelectList v-model="selectedInactiveListItems" :list="list" />
    <div>
      <div>
        <button type="button" @click="addToActiveList()">></button>
      </div>
      <div>
        <button type="button" @click="removeFromActiveList()"><</button>
      </div>
    </div>
    <SelectList v-model="selectedActiveListItems" :list="internalModelValue" />
  </div>
  <p>selectedInactiveListItems {{ selectedInactiveListItems }}</p>
  <p>selectedActiveListItems {{ selectedActiveListItems }}</p>
</template>

<script>
import SelectList from './SelectList.vue';

export default {
  name: 'TransferList',
  emits: ['updateList', 'update:modelValue'],
  components: {
    SelectList,
  },
  props: {
    list: Array,
    modelValue: Array,
  },
  mounted() {
    removeDuplicatesFromInactiveList();
  },
  data() {
    return {
      selectedInactiveListItems: [],
      selectedActiveListItems: [],
    };
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
  methods: {
    addToActiveList() {
      //Checks for duplicates
      const found = this.internalModelValue.some((r) =>
        this.selectedInactiveListItems.includes(r)
      );
      //Do not continue if duplicates are found in the activelist
      if (!found) {
        //Update ActiveList
        this.internalModelValue = this.internalModelValue.concat(
          this.selectedInactiveListItems
        );

        //Remove items from inactiveList
        const newInactiveList = this.list.filter(
          (val) => !this.selectedInactiveListItems.includes(val)
        );

        //empty selected items in selectedInactiveListItems
        this.selectedInactiveListItems = [];
        this.$emit('updateList', newInactiveList);
      }
    },
    removeFromActiveList() {
      //Checks for duplicates
      const found = this.selectedActiveListItems.some((r) =>
        this.list.includes(r)
      );
      //Do not continue if duplicates are found in the inactiveList
      if (!found) {
        //Update inactiveList
        const newInactiveList = this.list.concat(this.selectedActiveListItems);

        //Remove items from activeList
        this.internalModelValue = this.internalModelValue.filter(
          (val) => !this.selectedActiveListItems.includes(val)
        );

        //empty selected items in selectedInactiveListItems
        this.selectedActiveListItems = [];
        this.$emit('updateList', newInactiveList);
      }
    },
  },
  removeDuplicatesFromInactiveList() {
    //Remove items from inactiveList
    const newInactiveList = this.list.filter(
      (val) => !this.internalModelValue.includes(val)
    );

    this.$emit('updateList', newInactiveList);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.transferListContainer {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
